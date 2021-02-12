---
title: API di pretranscodifica
description: Potete utilizzare l'API di ricompilazione "just-in-time" per transcodificare anticipatamente annunci pubblicitari, in modo da disporre di versioni compatibili con i contenuti quando necessario, eliminando il ritardo di 2-4 minuti associato al package "just-in-time" (JIT).
seo-description: Potete utilizzare l'API di ricompilazione "just-in-time" per transcodificare anticipatamente annunci pubblicitari, in modo da disporre di versioni compatibili con i contenuti quando necessario, eliminando il ritardo di 2-4 minuti associato al package "just-in-time" (JIT).
seo-title: API di pretranscodifica
uuid: 03cd2428-510a-4b99-8496-059a48d5abba
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---


# API di pretranscodifica e ricompilazione {#pre-transcoding-api}

Primetime  Ad Insertion offre un&#39;API di pretranscodifica per le situazioni in cui gli URL creativi sono noti in anticipo, ad esempio per grandi eventi a vendita diretta.  Questo elimina il ritardo di 2-4 minuti associato alla transcodifica &quot;just-in-time&quot;.

## Richiesta HTTP {#section_F616F5722F0B4AB7939EE2ECBEDDB297}

Inviate un comando POST HTTP all’URL specificato per indicare a CRS quale annuncio pubblicitario desiderate transcodificare e quali opzioni desiderate utilizzare. Il codice di risposta indica l’esito positivo o negativo e altre informazioni.

Questa richiesta richiede un nome utente e una password. Puoi ottenerli dal tuo responsabile commerciale  Adobe. Per informazioni sull&#39;autenticazione, contattate il rappresentante  di abilitazione Adobe Primetime.

Per inviare una richiesta di transcodifica a CRS, inviate un messaggio HTTP nel modo seguente:

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

Il blocco `RepackageList` nel corpo può contenere da 1 a 300 `Repackage` blocchi. Se il numero di blocchi `Repackage` nel corpo supera 300, la richiesta HTTP non riesce con il seguente errore:

```
<codeph>
 HTTP 413 Request Entity Too Large: Validation fail: Too many
     requests. Max limit is 300
</codeph>.
```


I parametri obbligatori e facoltativi in un blocco `Repackage` sono i seguenti:

* **`AdSystem`** (Obbligatorio) - L&#39;origine e il server, ad esempio  `Auditude`,  `FreeWheel`,  `Apad.tv`. Si tratta di un valore di stringa che corrisponde all&#39;elemento VAST `AdSystem`.

* **`AdId`** (Obbligatorio) - Identificatore per il server di annunci di terze parti specificato nella richiesta. Corrisponde all&#39;attributo `id` dell&#39;elemento `Ad` in una risposta VAST.

* **`CreativeURL`** (Obbligatorio) - La posizione (URI) dell&#39;annuncio creativo da transcodificare. Questo corrisponde all&#39;elemento VAST `MediaFile`.

* `CreativeID` (facoltativo) - Identificatore per l&#39;annuncio creativo da includere come parte dell&#39;esperienza pubblicitaria.
* **`Zone`** (Obbligatorio) - ID zona per l&#39;account (richiedi il tuo account manager tecnico). Si tratta di un valore numerico che corrisponde all&#39;impostazione della piattaforma Auditude `publisher_site_id`.

* **`Format`** (facoltativo) - Parametri per controllare il modo in cui CRS transcodifica l&#39;annuncio creativo:

   * `clientside` - Genera output compatibile con l’URL utilizzato da TVSDK per comunicare con la CDN.
   >[!IMPORTANT]
   >
   >Dovete fornire questo parametro se desiderate che l&#39;annuncio reinserito sia compatibile con il Ad Insertion  lato client. In caso contrario, l&#39;annuncio reinserito sarà compatibile solo con il Ad Insertion  lato server.

   * `hls` - Generare annunci transcodificati e creativi compatibili con HLS.
   * `dash` - Generare annunci transcodificati e creativi compatibili con DASH.
   * `id3` - Iniettate i tag metadati temporizzati ID3 nei tag transcodificati e creativi.
   * `targetdur` - Durata del segmento (in secondi) per l’annuncio pubblicitario transcodificato. Il valore predefinito è `targetdur=4`. Questo valore deve corrispondere al valore specificato nel manifesto per `<s>` nel tag della durata di destinazione: `#EXT-X-TARGETDURATION:<s>`.

   >[!NOTE]
   >
   >Le risorse compatibili con DASH non sono compatibili con  inserimento di annunci Adobe Primetime.

>[!IMPORTANT]
>
>Per garantire una riproduzione ottimale, impostate `targetdur` in modo che corrisponda alla durata del blocco del contenuto.

## Risposta HTTP {#section_B30D27E4A6AC4AAD9E758162EFF7D963}

Il CRS risponde alla richiesta con uno dei seguenti codici di stato:

* **HTTP 202** - Accettato (con corpo vuoto). Indica il successo. CRS carica l’annuncio transcodificato nel server CDN.
* **HTTP 400**  - Richiesta non valida. Il codice XML registrato non è valido.
* **HTTP 500**  - Errore interno del server. Il server ha rilevato un problema interno (ad esempio, il server non è stato in grado di connettersi a un database).

## Pre-transcodifica delle risorse per SSAI o CSAI {#section_098888BB74FD4DC1AD0BD507B2A48318}

Mediante l&#39;API di ricompilazione, potete precodificare eventi SSAI o CSAI futuri. Se le risorse verranno utilizzate con SSAI in futuro, accertatevi che tutti i parametri delle chiamate POST siano univoci. I parametri sono: AdSystem, AdId, CreativeURL, Zone, Format. Eventuali differenze in questo insieme di parametri determinano una nuova richiesta di transcodifica per SSAI.

Per le risorse utilizzate in futuro con CSAI, l’univocità delle risorse dipende da Zone e CreativeURL. AdSystem e AdId non generano risorse transcodificate diverse e sono disponibili per i client.
