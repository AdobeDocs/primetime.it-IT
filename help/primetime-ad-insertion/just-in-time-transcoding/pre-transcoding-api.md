---
title: API di pre-transcodifica
description: Puoi utilizzare l’API di riconfezionamento just-in-time per transcodificare in anticipo le creatività degli annunci, in modo da rendere disponibili, se necessario, versioni compatibili con i contenuti, eliminando il ritardo di 2-4 minuti associato al riconfezionamento just-in-time (JIT).
exl-id: d45668e0-ec8a-4e5a-a56b-cffff27561f2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 0%

---

# API di pre-transcodifica e re-packaging {#pre-transcoding-api}

Primetime Ad Insertion offre un’API di pre-transcodifica per le situazioni in cui gli URL creativi sono noti in anticipo, ad esempio per grandi eventi di vendita diretta.  Questo elimina il ritardo di 2-4 minuti associato alla transcodifica just-in-time.

## Richiesta HTTP {#section_F616F5722F0B4AB7939EE2ECBEDDB297}

Invia un comando HTTP POST all’URL specificato per indicare a CRS quale annuncio creativo desideri trascodificare e quali opzioni desideri utilizzare. Il codice di risposta segnala l’esito positivo o negativo e altre informazioni.

Questa richiesta richiede un nome utente e una password. Puoi ottenerli dal tuo account manager tecnico Adobe. Per informazioni sull’autenticazione, contatta il rappresentante Adobe Primetime Enablement.

Per inviare una richiesta di transcodifica a CRS, invia un messaggio HTTP come segue:

* **URL -** [https://id3.auditude.com/repackage](https://id3.auditude.com/repackage)

* **Metodo -** `POST`

* **Autenticazione -** `Digest`

* **Intestazione** `Content-Type: text/xml`

* **Corpo -** XML come nell&#39;esempio seguente:

   ```xml
   <RepackageList>
       <Repackage>
           <AdSystem>Auditude</AdSystem>
           <AdID>AUD1</AdID>
           <CreativeID>AUD-CR1</CreativeID>
           <CreativeURL>https://cdn.auditude.com/assets/ip/starbucks2.mp4</CreativeURL>
           <Zone>3</Zone>
       </Repackage>
       <Repackage>
           <AdSystem>Auditude</AdSystem>
           <AdID>AUD2</AdID>
           <CreativeID>AUD-CR1</CreativeID>
           <CreativeURL>https://cdn.auditude.com/assets/ip/starbucks2.mp4</CreativeURL>
           <Format>id3 targetdur=5</Format>
           <Zone>3</Zone>
       </Repackage>
   </RepackageList>
   ```

Il `RepackageList` Il blocco nel corpo può contenere da 1 a 300 `Repackage` blocchi. Se il numero di `Repackage` I blocchi nel corpo superano i 300, quindi la richiesta HTTP non riuscirà e restituirà il seguente errore:

```
<codeph>
 HTTP 413 Request Entity Too Large: Validation fail: Too many
     requests. Max limit is 300
</codeph>.
```


I parametri obbligatori e facoltativi in una `Repackage` i blocchi sono i seguenti:

* **`AdSystem`** (Obbligatorio): l’ad server di origine, ad esempio, `Auditude`, `FreeWheel`, `Apad.tv`. Si tratta di un valore stringa che corrisponde all&#39;elemento VAST `AdSystem`.

* **`AdId`** (Obbligatorio) - Identificatore del server di annunci di terze parti specificato nella richiesta. Corrisponde al `id` attributo del `Ad` in una risposta VAST.

* **`CreativeURL`** (Obbligatorio): posizione (URI) della creatività dell’annuncio da transcodificare. Questo corrisponde al VAST `MediaFile` elemento.

* `CreativeID` (facoltativo): identificatore della creatività dell’annuncio da includere nell’esperienza dell’annuncio.
* **`Zone`** (Obbligatorio) - ID zona per il tuo account (ottieni dal tuo account manager tecnico). Questo è un valore numerico che corrisponde alla piattaforma Auditude `publisher_site_id` impostazione.

* **`Format`** (facoltativo) - Parametri per controllare il modo in cui CRS transcodifica la creatività dell’annuncio:

   * `clientside` : genera un output compatibile con l’URL utilizzato da TVSDK per comunicare con la rete CDN.
   >[!IMPORTANT]
   >
   >Devi fornire questo parametro se desideri che l’annuncio ricompilato sia compatibile con l’Ad Insertion lato client. In caso contrario, l’annuncio riconfezionato sarà compatibile solo con Server Side Ad Insertion.

   * `hls` : genera un annuncio transcodificato e creativo compatibile con HLS.
   * `dash` : genera un annuncio transcodificato e creativo compatibile con DASH.
   * `id3` : inserisci i tag di metadati temporizzati ID3 nella creatività dell’annuncio transcodificato.
   * `targetdur` - Durata del segmento (in secondi) per l’annuncio transcodificato e creativo. Il valore predefinito è `targetdur=4`. Questo valore deve corrispondere al valore specificato nel manifesto per `<s>` nel tag durata target: `#EXT-X-TARGETDURATION:<s>`.

   >[!NOTE]
   >
   >Le risorse compatibili con DASH non sono compatibili con l’inserimento di annunci Adobe Primetime.

>[!IMPORTANT]
>
>Per garantire una riproduzione ottimale, impostare `targetdur` affinché corrisponda alla durata del blocco di contenuto.

## Risposta HTTP {#section_B30D27E4A6AC4AAD9E758162EFF7D963}

CRS risponde alla richiesta con uno dei seguenti codici di stato:

* **HTTP 202** - Accettato (con corpo vuoto). Questo indica il successo. CRS carica l’annuncio transcodificato sul server CDN.
* **HTTP 400** - Richiesta non valida. XML inviato non valido.
* **HTTP 500** - Errore interno del server. Si è verificato un problema interno del server, ad esempio non è stato possibile connettersi a un database.

## Risorse pre-transcodifica per SSAI o CSAI {#section_098888BB74FD4DC1AD0BD507B2A48318}

Utilizzando l’API di riconfezionamento, puoi pre-trascodificare eventi SSAI o CSAI futuri. Se le risorse devono essere utilizzate con SSAI in futuro, assicurati che tutti i parametri nelle chiamate POST siano univoci. I parametri sono: AdSystem, AdId, CreativeURL, Zone, Format. Eventuali differenze in questo set di parametri determinano una nuova richiesta di transcodifica per SSAI.

Per le risorse utilizzate in futuro con CSAI, l’univocità delle risorse dipende da Zone e CreativeURL. AdSystem e AdId non generano risorse transcodificate diverse, disponibili per i client.
