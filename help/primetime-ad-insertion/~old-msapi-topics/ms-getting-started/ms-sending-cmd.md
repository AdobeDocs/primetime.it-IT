---
description: Usa il comando HTTP GET per interagire con il server manifest.
title: Invia un comando al server manifesto
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# Invia un comando al server manifesto {#send-a-command-to-the-manifest-server}

Usa il comando HTTP GET per interagire con il server manifest.

1. Invia una richiesta `HTTP GET` per un URL di bootstrap costruito utilizzando il seguente pattern:

   ```
   https://{manifest-server:port}/auditude/variant/
    {PublisherAssetID}/{Content URL (base64)}.m3u8
    ?{query parameters}
   ```

* **** PublisherAssetIDRrequired. ID univoco dell&#39;editore per il contenuto specifico.

* **Contenuto** URLRobbligatorio. URL del contenuto file M3U8, codificato Base64 per essere sicuro all&#39;interno dell&#39;URL del server manifesto. L’URL del contenuto deve puntare a un file M3U8 variante, anche se è presente un solo flusso di bit rate.

* **Parametri di queryAlcuni sono obbligatori, altri facoltativi.** Questi costituiscono la parte più variegata della richiesta. Essi dicono al server manifest quale tipo di client sta facendo la richiesta e cosa vuole che il server manifest faccia.

   Ad esempio:

   ```
   https://manifest.auditude.com/auditude/variant/
    {publisherAssetID}/{Content URL (base64)}.m3u8?
   u={Asset ID}&z={zone}&_sid_=0&pttrackingmode=simple
   &pttrackingversion=v2&live=false
   ```

   **Richieste HTTP e HTTPS**

   Il server manifesto crea gli URL utilizzando lo stesso protocollo HTTP della richiesta del client. Se un lettore effettua una richiesta HTTP (http) non sicura, il server manifesto restituisce gli URL manifest e gli URL di tracciamento di Auditude con il protocollo http. Se un lettore effettua una connessione HTTP (https) sicura, un server manifest, restituisce gli URL manifest e gli URL di tracciamento Auditude con il protocollo https.

   >[!NOTE]
   >
   >Il server manifesto non può modificare il protocollo (HTTP o HTTPS) dei segmenti di contenuto (.ts) e dei beacon di tracciamento di terze parti. Per configurare i protocolli desiderati, contatta il contenuto e i provider di annunci di terze parti.