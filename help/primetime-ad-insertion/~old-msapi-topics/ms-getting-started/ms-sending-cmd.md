---
description: Utilizza il comando HTTP GET per interagire con il server manifesto.
title: Invia un comando al server manifesto
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# Invia un comando al server manifesto {#send-a-command-to-the-manifest-server}

Utilizza il comando HTTP GET per interagire con il server manifesto.

1. Invia un `HTTP GET` richiesta di un URL di avvio costruito utilizzando il seguente pattern:

   ```
   https://{manifest-server:port}/auditude/variant/
    {PublisherAssetID}/{Content URL (base64)}.m3u8
    ?{query parameters}
   ```

* **PublisherAssetID** Obbligatorio. ID univoco dell’editore per il contenuto specifico.

* **URL contenuto** Obbligatorio. URL del file di contenuto M3U8, con codifica Base64 per essere sicuro nell’URL del server manifesto. L’URL del contenuto deve puntare a un file M3U8 variante, anche se è presente un solo flusso di velocità in bit.

* **Parametri di query** Alcune sono obbligatorie, altre facoltative. Questi costituiscono la parte più variegata della richiesta. Indicano al server manifesto il tipo di client che effettua la richiesta e cosa desidera che faccia il server manifesto.

   Ad esempio:

   ```
   https://manifest.auditude.com/auditude/variant/
    {publisherAssetID}/{Content URL (base64)}.m3u8?
   u={Asset ID}&z={zone}&_sid_=0&pttrackingmode=simple
   &pttrackingversion=v2&live=false
   ```

   **Richieste HTTP e HTTPS**

   Il server manifesto crea URL utilizzando lo stesso protocollo HTTP della richiesta del client. Se un lettore effettua una richiesta HTTP (http) non sicura, il server manifesto restituisce gli URL del manifesto e gli URL di tracciamento di Auditude con il protocollo http. Se un lettore effettua una connessione HTTP sicura (https), il server manifest, restituisce gli URL manifest e gli URL di tracciamento Auditude con il protocollo https.

   >[!NOTE]
   >
   >Il server manifesto non può modificare il protocollo (HTTP o HTTPS) dei segmenti di contenuto (.ts) e dei beacon di tracciamento di terze parti. Contatta i contenuti e i provider di annunci di terze parti per richiedere la configurazione dei protocolli desiderati.