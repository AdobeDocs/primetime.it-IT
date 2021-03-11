---
description: È possibile utilizzare l'API di ricompilazione CRS per transcodificare in anticipo i contenuti non HLS e creativi, in modo che una versione HLS sia disponibile quando è necessario eseguirla, eliminando il ritardo di 2-4 minuti associato al riconfezionamento just-in-time (JIT).
title: API di repackaging
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 0%

---


# API di repackaging {#repackaging-api}

È possibile utilizzare l&#39;API di ricompilazione CRS per transcodificare in anticipo i contenuti non HLS e creativi, in modo che una versione HLS sia disponibile quando è necessario eseguirla, eliminando il ritardo di 2-4 minuti associato al riconfezionamento just-in-time (JIT).

## Richiesta HTTP {#section_F616F5722F0B4AB7939EE2ECBEDDB297}

Invia un comando HTTP POST all&#39;URL specificato per indicare a CRS quale annuncio creativo desideri transcodificare e quali opzioni desideri utilizzare. Il codice di risposta segnala il successo o l’errore e altre informazioni.

Questa richiesta richiede un nome utente e una password. Puoi ottenerli dal tuo account manager tecnico Adobe. Se hai bisogno di informazioni sull’autenticazione, contatta il tuo rappresentante di abilitazione Adobe Primetime.

Per inviare una richiesta di transcodifica a CRS, invia un messaggio HTTP come segue:

* **URL -** [https://id3.auditude.com/repackage](https://id3.auditude.com/repackage)

* **Metodo -** `POST`

* **Auth -** `Digest`

* **Intestazione -** `Content-Type: text/xml`

* **Body -** XML come nell&#39;esempio seguente:

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

Il blocco `RepackageList` nel corpo può contenere da 1 a 300 blocchi `Repackage`. Se il numero di blocchi `Repackage` nel corpo supera 300, la richiesta HTTP avrà esito negativo con il seguente errore:

```
<codeph>
 HTTP 413 Request Entity Too Large: Validation fail: Too many
     requests. Max limit is 300
</codeph>.
```


I parametri richiesti e facoltativi in un blocco `Repackage` sono i seguenti:

* **`AdSystem`** (Obbligatorio) - Il server dell&#39;annuncio sorgente, ad esempio  `Auditude`,  `FreeWheel`,  `Apad.tv`. Si tratta di un valore stringa che corrisponde all’elemento VAST `AdSystem`.

* **`AdId`** (Obbligatorio) - Questo è un identificatore per il server di annunci di terze parti specificato nella richiesta. Corrisponde all&#39;attributo `id` dell&#39;elemento `Ad` in una risposta VAST.

* **`CreativeURL`** (Obbligatorio) - La posizione (URI) dell’annuncio creativo da transcodificare. Questo corrisponde all’elemento VAST `MediaFile` .

* `CreativeID` (facoltativo) - Identificatore dell&#39;annuncio creativo da includere come parte dell&#39;esperienza pubblicitaria.
* **`Zone`** (Obbligatorio) - ID zona per il tuo account (ottieni dal tuo account manager tecnico). Si tratta di un valore numerico che corrisponde all’impostazione della piattaforma Auditude `publisher_site_id` .

* **`Format`** (facoltativo) - Parametri per controllare il modo in cui CRS transcodifica l&#39;annuncio creativo:

   * `clientside` - Genera un output compatibile con l’URL utilizzato da TVSDK per comunicare con la CDN.
   >[!IMPORTANT]
   >
   >È necessario fornire questo parametro se si desidera che l’annuncio ricalcolato sia compatibile con Client Side Ad Insertion. Se non fornisci questo, l&#39;annuncio reinserito nel pacchetto sarà compatibile solo con Server Side Ad Insertion.

   * `hls` - Genera un annuncio pubblicitario transcodificato compatibile con HLS.
   * `dash` - Genera un annuncio pubblicitario transcodificato compatibile con DASH.
   * `id3` - Inserisci i tag dei metadati temporizzati ID3 nei contenuti creativi e transcodificati.
   * `targetdur` - Durata del segmento (in secondi) per l’annuncio creativo transcodificato. Il valore predefinito è `targetdur=4`. Questo valore deve corrispondere al valore specificato nel manifesto per `<s>` nel tag di durata target: `#EXT-X-TARGETDURATION:<s>`.

   >[!NOTE]
   >
   >Le risorse compatibili con DASH non sono compatibili con l’inserimento di annunci in Adobe Primetime.

>[!IMPORTANT]
>
>Per garantire una riproduzione più fluida, impostare `targetdur` in modo che corrisponda alla durata del blocco del contenuto.

## Risposta HTTP {#section_B30D27E4A6AC4AAD9E758162EFF7D963}

CRS risponde alla richiesta con uno dei seguenti codici di stato:

* **HTTP 202**  - Accettato (con corpo vuoto). Indica il successo. CRS carica l&#39;annuncio transcodificato nel server CDN.
* **HTTP 400**  - Richiesta non valida. XML inviato non valido.
* **HTTP 500**  - Errore interno del server. Problema interno del server (ad esempio, impossibile connettersi a un database).

## Pretranscodifica delle risorse per SSAI o CSAI {#section_098888BB74FD4DC1AD0BD507B2A48318}

Utilizzando l’API di ricompilazione, puoi precodificare i futuri eventi SSAI o CSAI. Se le risorse saranno destinate in futuro a essere utilizzate con SSAI, assicurati che tutti i parametri nelle chiamate POST siano univoci. I parametri sono: AdSystem, AdId, CreativeURL, Zone, Format. Qualsiasi differenza in questo insieme di parametri, si traduce in una nuova richiesta di transcodifica per SSAI.

Per le risorse utilizzate in futuro con CSAI, l’univocità della risorsa dipende da Zone e CreativeURL. AdSystem e AdId non si traducono in risorse transcodificate diverse e sono disponibili per i client.
