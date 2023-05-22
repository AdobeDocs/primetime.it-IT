---
description: Puoi utilizzare TVSDK per inviare dati arbitrari nelle intestazioni dei cookie per la gestione delle sessioni, l’accesso ai gate e così via.
title: Utilizzare i cookie
exl-id: f7a64c77-7db6-4bae-b299-69267fedc673
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---

# Utilizzare i cookie{#work-with-cookies}

Puoi utilizzare TVSDK per inviare dati arbitrari nelle intestazioni dei cookie per la gestione delle sessioni, l’accesso ai gate e così via.

Di seguito è riportato un esempio con un certo tipo di autenticazione quando si effettuano richieste al server chiave:

1. Il cliente accede al sito web in un browser e il suo accesso mostra che può visualizzare il contenuto.
1. L&#39;applicazione genera un token di autenticazione, in base a quanto previsto dal server licenze. Passa tale valore a TVSDK.
1. TVSDK imposta tale valore nell’intestazione del cookie.
1. Quando TVSDK invia una richiesta al server chiavi per ottenere una chiave per decrittografare il contenuto, tale richiesta contiene il valore di autenticazione nell’intestazione del cookie, in modo che il server chiavi sappia che la richiesta è valida.

Per utilizzare i cookie:

1. Utilizza il `cookieHeaders` proprietà in `NetworkConfiguration` per impostare un cookie. Il `cookieHeaders` proprietà è un oggetto Metadata ed è possibile aggiungere coppie chiave-valore a questo oggetto da includere nell&#39;intestazione del cookie.

   Ad esempio:

   ```
   var metadata:Metadata = new Metadata(); 
   metadata.setValue(“val1”, “12345”); 
   metadata.setValue(“val2”, “abcd”); 
   
   networkConfiguration.cookieHeaders = metadata;
   ```

   Per impostazione predefinita, le intestazioni dei cookie vengono inviate solo con richieste chiave. Per inviare intestazioni cookie con tutte le richieste, imposta `NetworkConfiguration` proprietà `useCookieHeadersForAllRequests` su true.

1. Per garantire che `NetworkConfiguration` funziona, impostalo come metadati:

   ```
   var networkConfiguration:NetworkConfiguration = new NetworkConfiguration(); 
   networkConfiguration.forceNativeNetworking = true; 
   var resourceMetadata:Metadata = new Metadata(); 
   resourceMetadata.setMetadata(DefaultMetadataKeys.NETWORK_CONFIGURATION_KEY,  
                                networkConfiguration);
   ```

1. Fornisci i metadati del passaggio precedente quando crei un `MediaResource`.

   Ad esempio, se utilizzi il `createFromURL` immettere le informazioni seguenti:

   ```
   var resource:MediaResource = MediaResource.createFromURL(url, resourceMetadata);
   ```
