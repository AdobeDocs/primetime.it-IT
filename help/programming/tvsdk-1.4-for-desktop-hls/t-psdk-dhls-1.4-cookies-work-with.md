---
description: Puoi utilizzare TVSDK per inviare dati arbitrari nelle intestazioni dei cookie per la gestione delle sessioni, l'accesso ai gate e così via.
title: Utilizzare i cookie
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---


# Lavora con i cookie{#work-with-cookies}

Puoi utilizzare TVSDK per inviare dati arbitrari nelle intestazioni dei cookie per la gestione delle sessioni, l&#39;accesso ai gate e così via.

Di seguito è riportato un esempio con alcuni tipi di autenticazione quando si eseguono richieste al server chiave:

1. Il tuo cliente accede al tuo sito web in un browser e il suo accesso mostra che gli è consentito visualizzare il contenuto.
1. L’applicazione genera un token di autenticazione in base a quanto previsto dal server licenze. Passa quel valore a TVSDK.
1. TVSDK imposta tale valore nell’intestazione del cookie.
1. Quando TVSDK effettua una richiesta al server chiavi per ottenere una chiave per decrittografare il contenuto, tale richiesta contiene il valore di autenticazione nell’intestazione del cookie, in modo che il server chiavi sappia che la richiesta è valida.

Per lavorare con i cookie:

1. Utilizza la proprietà `cookieHeaders` in `NetworkConfiguration` per impostare un cookie. La proprietà `cookieHeaders` è un oggetto Metadata ed è possibile aggiungere coppie di valori chiave a questo oggetto da includere nell&#39;intestazione del cookie.

   Ad esempio:

   ```
   var metadata:Metadata = new Metadata(); 
   metadata.setValue(“val1”, “12345”); 
   metadata.setValue(“val2”, “abcd”); 
   
   networkConfiguration.cookieHeaders = metadata;
   ```

   Per impostazione predefinita, le intestazioni dei cookie vengono inviate solo con richieste di chiave. Per inviare intestazioni dei cookie con tutte le richieste, imposta la proprietà `NetworkConfiguration` `useCookieHeadersForAllRequests` su true.

1. Per garantire il funzionamento di `NetworkConfiguration`, impostalo come metadati:

   ```
   var networkConfiguration:NetworkConfiguration = new NetworkConfiguration(); 
   networkConfiguration.forceNativeNetworking = true; 
   var resourceMetadata:Metadata = new Metadata(); 
   resourceMetadata.setMetadata(DefaultMetadataKeys.NETWORK_CONFIGURATION_KEY,  
                                networkConfiguration);
   ```

1. Fornisci i metadati del passaggio precedente quando crei un `MediaResource`.

   Ad esempio, se utilizzi il metodo `createFromURL`, immetti le seguenti informazioni:

   ```
   var resource:MediaResource = MediaResource.createFromURL(url, resourceMetadata);
   ```

