---
description: Potete utilizzare TVSDK per inviare dati arbitrari nelle intestazioni dei cookie per la gestione delle sessioni, l'accesso ai gate e così via.
seo-description: Potete utilizzare TVSDK per inviare dati arbitrari nelle intestazioni dei cookie per la gestione delle sessioni, l'accesso ai gate e così via.
seo-title: Operazioni con i cookie
title: Operazioni con i cookie
uuid: f060b520-ceec-48ca-929f-683566fe6ae7
translation-type: tm+mt
source-git-commit: 6da7d597503d98875735c54e9a794f8171ad408b
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---


# Operazioni con i cookie{#work-with-cookies}

Potete utilizzare TVSDK per inviare dati arbitrari nelle intestazioni dei cookie per la gestione delle sessioni, l&#39;accesso ai gate e così via.

Di seguito è riportato un esempio con alcuni tipi di autenticazione durante l&#39;esecuzione di richieste al server chiave:

1. Il cliente accede al sito Web in un browser e il suo accesso mostra che è autorizzato a visualizzare il contenuto.
1. L&#39;applicazione genera un token di autenticazione, in base a quanto previsto dal server licenze. Trasmettere tale valore a TVSDK.
1. TVSDK imposta tale valore nell’intestazione del cookie.
1. Quando TVSDK richiede al server di chiavi di ottenere una chiave per decifrare il contenuto, la richiesta contiene il valore di autenticazione nell&#39;intestazione del cookie, in modo che il server di chiavi sappia che la richiesta è valida.

Per lavorare con i cookie:

1. Create un cookie `cookieManager` e aggiungete i cookie per gli URI al vostro `cookieStore`.

   Ad esempio:

   >[!IMPORTANT]
   >
   >Quando il reindirizzamento 302 è abilitato, la richiesta di annuncio può essere reindirizzata a un dominio diverso da quello al quale il cookie appartiene.

   ```java
   CookieManager cookieManager= new CookieManager(); 
   CookieHandler.setDefault(cookieManager);  
   HttpCookie cookie=new HttpCookie("lang","fr"); 
   cookie.setDomain("twitter.com");  
   cookie.setPath("/"); 
   cookie.setVersion(0); 
   cookieManager.getCookieStore().add(newURI("https://twitter.com/"),cookie);
   ```

   TVSDK esegue una query a questo cookieManager in fase di esecuzione, verifica se sono presenti cookie associati all&#39;URL e li utilizza automaticamente.

   Un&#39;altra opzione consiste nell&#39;utilizzare `cookieHeaders` in `NetworkConfiguration` per impostare una stringa di intestazione cookie arbitraria da utilizzare per le richieste. Per impostazione predefinita, questa intestazione del cookie viene inviata solo con richieste di chiave. Per inviare l’intestazione del cookie a tutte le richieste, utilizzate il `NetworkConfiguration` metodo `setUseCookieHeadersForAllRequests`:

```java
   NetworkConfiguration networkConfiguration = new NetworkConfiguration(); 
    
   Metadata cookie = new MetadataNode(); 
   cookie.setValue("reqPayload", “1234567”); 
   networkConfiguration.setCookieHeaders(cookie); 
   networkConfiguration.setUseCookieHeadersForAllRequests( true ); 
    
   // Set NetworkConfiguration as Metadata:                                                                   
   MetadataNode resourceMetadata = new MetadataNode(); 
   resourceMetadata.setNode(DefaultMetadataKeys.NETWORK_CONFIGURATION.getValue(),  
                            networkConfiguration); 
    
   // Call MediaResource.createFromURL to set the metadata: 
   MediaResource resource = MediaResource.createFromURL(url, resourceMetadata); 
   // Load the resource 
   mediaPlayer.replaceCurrentItem(resource);
```
