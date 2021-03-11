---
description: Puoi utilizzare TVSDK per inviare dati arbitrari nelle intestazioni dei cookie per la gestione delle sessioni, l'accesso ai gate e così via.
title: Utilizzare i cookie
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '246'
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

1. Crea un `cookieManager` e aggiungi i cookie per gli URI al tuo `cookieStore`.

   Ad esempio:

   >[!IMPORTANT]
   >
   >Quando è abilitato il reindirizzamento 302, la richiesta di annuncio può essere reindirizzata a un dominio diverso da quello a cui appartiene il cookie.

   ```java
   CookieManager cookieManager= new CookieManager(); 
   CookieHandler.setDefault(cookieManager);  
   HttpCookie cookie=new HttpCookie("lang","fr"); 
   cookie.setDomain("twitter.com");  
   cookie.setPath("/"); 
   cookie.setVersion(0); 
   cookieManager.getCookieStore().add(newURI("https://twitter.com/"),cookie);
   ```

   TVSDK invia una query a questo cookieManager in fase di runtime, verifica se sono presenti cookie associati all’URL e li utilizza automaticamente.

   Un’altra opzione consiste nell’utilizzare `cookieHeaders` in `NetworkConfiguration` per impostare una stringa di intestazione di cookie arbitraria da utilizzare per le richieste. Per impostazione predefinita, questa intestazione di cookie viene inviata solo con richieste di chiave. Per inviare l’intestazione del cookie con tutte le richieste, utilizza il metodo `NetworkConfiguration` `setUseCookieHeadersForAllRequests` :

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
