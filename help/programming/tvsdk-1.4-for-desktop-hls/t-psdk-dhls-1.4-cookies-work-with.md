---
description: Potete utilizzare TVSDK per inviare dati arbitrari nelle intestazioni dei cookie per la gestione delle sessioni, l'accesso ai gate e così via.
seo-description: Potete utilizzare TVSDK per inviare dati arbitrari nelle intestazioni dei cookie per la gestione delle sessioni, l'accesso ai gate e così via.
seo-title: Operazioni con i cookie
title: Operazioni con i cookie
uuid: 7586a5a7-9914-403b-86a9-fbdd28664b07
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# Utilizzare i cookie{#work-with-cookies}

Potete utilizzare TVSDK per inviare dati arbitrari nelle intestazioni dei cookie per la gestione delle sessioni, l&#39;accesso ai gate e così via.

Di seguito è riportato un esempio con alcuni tipi di autenticazione durante l&#39;esecuzione di richieste al server chiave:

1. Il cliente accede al sito Web in un browser e il suo accesso mostra che è autorizzato a visualizzare il contenuto.
1. L&#39;applicazione genera un token di autenticazione, in base a quanto previsto dal server licenze. Trasmettere tale valore a TVSDK.
1. TVSDK imposta tale valore nell’intestazione del cookie.
1. Quando TVSDK richiede al server di chiavi di ottenere una chiave per decifrare il contenuto, la richiesta contiene il valore di autenticazione nell&#39;intestazione del cookie, in modo che il server di chiavi sappia che la richiesta è valida.

Per lavorare con i cookie:

1. Utilizzare la proprietà `cookieHeaders` in `NetworkConfiguration` per impostare un cookie. La proprietà `cookieHeaders` è un oggetto Metadata ed è possibile aggiungere coppie di valori chiave a questo oggetto da includere nell&#39;intestazione del cookie.

   Ad esempio:

   ```
   var metadata:Metadata = new Metadata(); 
   metadata.setValue(“val1”, “12345”); 
   metadata.setValue(“val2”, “abcd”); 
   
   networkConfiguration.cookieHeaders = metadata;
   ```

   Per impostazione predefinita, le intestazioni dei cookie vengono inviate solo con richieste di chiave. Per inviare le intestazioni dei cookie con tutte le richieste, impostare la proprietà `NetworkConfiguration` `useCookieHeadersForAllRequests` su true.

1. Per assicurarsi che `NetworkConfiguration` funzioni, impostatelo come metadati:

   ```
   var networkConfiguration:NetworkConfiguration = new NetworkConfiguration(); 
   networkConfiguration.forceNativeNetworking = true; 
   var resourceMetadata:Metadata = new Metadata(); 
   resourceMetadata.setMetadata(DefaultMetadataKeys.NETWORK_CONFIGURATION_KEY,  
                                networkConfiguration);
   ```

1. Fornite i metadati del passaggio precedente quando create un `MediaResource`.

   Ad esempio, se utilizzate il metodo `createFromURL`, immettete le informazioni seguenti:

   ```
   var resource:MediaResource = MediaResource.createFromURL(url, resourceMetadata);
   ```

