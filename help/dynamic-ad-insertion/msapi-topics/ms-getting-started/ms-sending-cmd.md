---
description: Utilizzare il comando GET HTTP per interagire con il server manifesto.
seo-description: Utilizzare il comando GET HTTP per interagire con il server manifesto.
seo-title: Invio di un comando al server manifesto
title: Invio di un comando al server manifesto
uuid: e9680563-d268-406d-87ce-1521a677e9ec
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# Inviare un comando al server manifesto {#send-a-command-to-the-manifest-server}

Utilizzare il comando GET HTTP per interagire con il server manifesto.

1. Inviate una richiesta `HTTP GET` per un URL del programma di avvio automatico creato con il seguente pattern:

   ```
   https://{manifest-server:port}/auditude/variant/
    {PublisherAssetID}/{Content URL (base64)}.m3u8
    ?{query parameters}
   ```

* **** PublisherAssetIDRequred. ID univoco dell&#39;editore per il contenuto specifico.

* **Content** URLRequred. URL del contenuto del file M3U8, con codifica Base64 per garantire la sicurezza all&#39;interno dell&#39;URL del server manifesto. L&#39;URL del contenuto deve puntare a una variante del file M3U8, anche se è presente un solo flusso di bit rate.

* **Parametri** di query: alcuni sono obbligatori, altri facoltativi. Queste costituiscono la parte più variegata della richiesta. Indica al server di manifesto quale tipo di client sta effettuando la richiesta e cosa desidera che esegua il server di manifesto.

   Ad esempio:

   ```
   https://manifest.auditude.com/auditude/variant/
    {publisherAssetID}/{Content URL (base64)}.m3u8?
   u={Asset ID}&z={zone}&_sid_=0&pttrackingmode=simple
   &pttrackingversion=v2&live=false
   ```

   **Richieste HTTP e HTTPS**

   Il server manifesto crea URL utilizzando lo stesso protocollo HTTP della richiesta del client. Se un lettore effettua una richiesta HTTP non sicura (http), il server manifesto restituisce gli URL manifest e gli URL di tracciamento Auditude con il protocollo http. Se un lettore crea una connessione HTTP (https) protetta, un server manifesto, restituisce gli URL manifest e gli URL di tracciamento Auditude con il protocollo https.

   >[!NOTE]
   >
   >Il server manifesto non può modificare il protocollo (HTTP o HTTPS) dei segmenti di contenuto (.ts) e dei beacon di tracciamento di terze parti. È necessario contattare il contenuto e i fornitori di annunci di terze parti per fare in modo che configurino i protocolli desiderati.