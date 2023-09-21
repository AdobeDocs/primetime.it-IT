---
description: Puoi utilizzare TVSDK per inviare dati arbitrari nelle intestazioni dei cookie per la gestione delle sessioni, l’accesso ai gate e così via.
title: Utilizzare i cookie
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# Utilizzare i cookie {#work-with-cookies}

Puoi utilizzare TVSDK per inviare dati arbitrari nelle intestazioni dei cookie per la gestione delle sessioni, l’accesso ai gate e così via.

Di seguito è riportato un esempio di richiesta al server chiave con alcune autenticazioni:

1. Il cliente accede al sito web in un browser e, quando accede, il cliente può visualizzare il contenuto.
1. In base a quanto previsto dal server licenze, l&#39;applicazione genera un token di autenticazione.

   Questo valore viene passato a TVSDK.
1. TVSDK imposta questo valore nell’intestazione del cookie.
1. Quando TVSDK invia una richiesta al server chiavi per ottenere una chiave per decrittografare il contenuto, la richiesta contiene il valore di autenticazione nell’intestazione del cookie.

   Il server chiavi è a conoscenza del fatto che la richiesta è valida.

Per utilizzare i cookie:

1. Creare un `cookieManager` e aggiungi i cookie per gli URI al tuo cookieStore.

   Ad esempio:

   ```java
   CookieManager cookieManager=new CookieManager(); 
   CookieHandler.setDefault(cookieManager);  
   HttpCookie cookie=new HttpCookie("lang","fr"); 
   cookie.setDomain("twitter.com");  
   cookie.setPath("/"); 
   cookie.setVersion(0); 
   cookieManager.getCookieStore().add(newURI("https://twitter.com/"),cookie);
   ```

   >[!TIP]
   >
   >Quando è abilitato il reindirizzamento 302, la richiesta dell’annuncio può essere reindirizzata a un dominio diverso da quello a cui appartiene il cookie.

   TVSDK esegue query su questo `cookieManager` in fase di runtime, controlla se sono presenti cookie associati all’URL e li utilizza automaticamente.

   Se è necessario aggiornare i cookie nell’applicazione durante la riproduzione, non utilizzare `networkConfiguration.setCookieHeaders` API come aggiornamento avverrà nell’archivio dei cookie JAVA.

   `networkConfiguration.setCookieHeaders` API imposta i cookie su C++ CookieStore di TVSDK.

   Quando utilizzi i cookie JAVA e li condividi tra Application e TVSDK, utilizza JAVA CookieStore per gestire i cookie esclusivamente.

   Prima di inizializzare la riproduzione, imposta i cookie su CookieStore utilizzando Cookie Manager come indicato sopra.

   Il cookie memorizzato in CookieStore verrà automaticamente raccolto da TVSDK.

   Se un valore di cookie deve essere aggiornato in un secondo momento durante la riproduzione, chiama lo stesso metodo add di CookieStore con la stessa chiave e un nuovo campo valore.

   Impostato anche
   `networkConfiguration.setReadSetCookieHeader`(false) prima di richiamare
   `config.setNetworkConfiguration(networkConfiguration)`

   >[!NOTE]
   >
   >Dopo aver impostato questa &quot;setReadSetCookieHeader&quot; su false, imposta i cookie per le richieste chiave utilizzando JAVA Cookie Manager.

   `onCookiesUpdated(CookiesUpdatedEvent cookiesUpdatedEvent)`
Questa API di callback verrà attivata ogni volta che si verifica un aggiornamento nei cookie C++ (cookie provenienti dalla risposta http). L’applicazione deve ascoltare questo callback e può aggiornare di conseguenza il proprio JAVA CookieStore in modo che le chiamate di rete in JAVA possano utilizzare i cookie come segue:

   ```
   private final CookiesUpdatedEventListener cookiesUpdatedEventListener = new CookiesUpdatedEventListener() {
   @Override
   public void onCookiesUpdated(CookiesUpdatedEvent cookiesUpdatedEvent) {
   List<HttpCookie> cookies = cookiesUpdatedEvent.getHttpCookies();
   for(int i = 0; i < cookies.size(); i++)
   { HttpCookie c = cookies.get(i); // To set this cookie on to the cookie store //c.setValue("newValue"); //If you want to modify the value of the cookie URI myuri = URI.create(cookiesUpdatedEvent.getDomainString()); cookieManager.getCookieStore().add(myuri,c); }
   }
   }
   ```
