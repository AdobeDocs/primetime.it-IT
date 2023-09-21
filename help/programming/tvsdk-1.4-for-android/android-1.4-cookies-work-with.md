---
description: Puoi utilizzare TVSDK per inviare dati arbitrari nelle intestazioni dei cookie per la gestione delle sessioni, l’accesso ai gate e così via.
title: Utilizzare i cookie
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '246'
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

1. Creare un `cookieManager` e aggiungere i cookie per gli URI al tuo `cookieStore`.

   Ad esempio:

   >[!IMPORTANT]
   >
   >Quando è abilitato il reindirizzamento 302, la richiesta dell’annuncio può essere reindirizzata a un dominio diverso da quello a cui appartiene il cookie.

   ```java
   CookieManager cookieManager= new CookieManager(); 
   CookieHandler.setDefault(cookieManager);  
   HttpCookie cookie=new HttpCookie("lang","fr"); 
   cookie.setDomain("twitter.com");  
   cookie.setPath("/"); 
   cookie.setVersion(0); 
   cookieManager.getCookieStore().add(newURI("https://twitter.com/"),cookie);
   ```

   TVSDK esegue una query su questo cookieManager in fase di esecuzione, controlla se all’URL sono associati dei cookie e li utilizza automaticamente.

   Un’altra opzione consiste nell’utilizzare `cookieHeaders` in `NetworkConfiguration` per impostare una stringa arbitraria di intestazione del cookie da utilizzare per le richieste. Per impostazione predefinita, questa intestazione cookie viene inviata solo con richieste chiave. Per inviare l’intestazione del cookie con tutte le richieste, utilizza `NetworkConfiguration` metodo `setUseCookieHeadersForAllRequests`:

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
