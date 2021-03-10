---
description: Puoi utilizzare TVSDK per inviare dati arbitrari nelle intestazioni dei cookie per la gestione delle sessioni, l'accesso ai gate e così via.
title: Utilizzare i cookie
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---


# Utilizzare i cookie {#work-with-cookies}

Puoi utilizzare TVSDK per inviare dati arbitrari nelle intestazioni dei cookie per la gestione delle sessioni, l&#39;accesso ai gate e così via.

Di seguito è riportato un esempio di richiesta al server chiave con alcune autenticazioni:

1. Il tuo cliente accede al tuo sito web in un browser e il suo accesso mostra che il cliente è autorizzato a visualizzare il contenuto.
1. In base a quanto previsto dal server licenze, l’applicazione genera un token di autenticazione.

   Questo valore viene passato a TVSDK.
1. TVSDK imposta questo valore nell’intestazione del cookie.
1. Quando TVSDK effettua una richiesta al server chiavi per ottenere una chiave per decrittografare il contenuto, la richiesta contiene il valore di autenticazione nell’intestazione del cookie.

   Il server chiavi sa che la richiesta è valida.

Per lavorare con i cookie:

1. Crea un `cookieManager` e aggiungi i cookie per gli URI al tuo cookieStore.

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
   >Quando è abilitato il reindirizzamento 302, la richiesta di annuncio può essere reindirizzata a un dominio diverso da quello a cui appartiene il cookie.

   TVSDK invia query a questo `cookieManager` in fase di runtime, verifica se sono presenti cookie associati all’URL e utilizza automaticamente tali cookie.

   Se è necessario aggiornare i cookie nell’applicazione durante la riproduzione, non utilizzare l’API `networkConfiguration.setCookieHeaders` in quanto l’aggiornamento verrà eseguito nell’archivio dei cookie JAVA.

   `networkConfiguration.setCookieHeaders` API imposta i cookie su C++ CookieStore di TVSDK.

   Quando utilizzi i cookie JAVA e li condividi tra Application e TVSDK, utilizza JAVA CookieStore per gestire solo i cookie.

   Prima di inizializzare la riproduzione, impostare i cookie su CookieStore utilizzando Cookie Manager come indicato sopra.

   Il cookie memorizzato in CookieStore verrà automaticamente raccolto da TVSDK.

   Se è necessario aggiornare un valore cookie in un secondo momento durante la riproduzione, invoca lo stesso metodo di aggiunta di CookieStore con la stessa chiave e un nuovo campo valore.

   Anche impostato
   `networkConfiguration.setReadSetCookieHeader`(false) prima della chiamata
   `config.setNetworkConfiguration(networkConfiguration)`

   >[!NOTE]
   >
   >Dopo aver impostato su false &#39;setReadSetCookieHeader&#39;, imposta i cookie per le richieste di chiave utilizzando il gestore di cookie JAVA.

   `onCookiesUpdated(CookiesUpdatedEvent cookiesUpdatedEvent)`
Questa API di callback verrà attivata ogni volta che si verifica un aggiornamento nei cookie C++ (cookie provenienti dalla risposta http). L&#39;applicazione deve ascoltare questo callback e può aggiornare di conseguenza il proprio JAVA CookieStore in modo che le loro chiamate di rete in JAVA possano utilizzare i cookie come segue:

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
