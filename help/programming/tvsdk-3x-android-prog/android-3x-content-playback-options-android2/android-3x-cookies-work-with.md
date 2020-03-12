---
description: Potete utilizzare TVSDK per inviare dati arbitrari nelle intestazioni dei cookie per la gestione delle sessioni, l'accesso ai gate e così via.
seo-description: Potete utilizzare TVSDK per inviare dati arbitrari nelle intestazioni dei cookie per la gestione delle sessioni, l'accesso ai gate e così via.
seo-title: Operazioni con i cookie
title: Operazioni con i cookie
uuid: 618bc59a-032d-445e-a867-ed2bf260570d
translation-type: tm+mt
source-git-commit: ad58732842eb651514a47dd565e31e3d98a84c46

---


# Operazioni con i cookie {#work-with-cookies}

Potete utilizzare TVSDK per inviare dati arbitrari nelle intestazioni dei cookie per la gestione delle sessioni, l&#39;accesso ai gate e così via.

Esempio di richiesta al server chiavi con autenticazione:

1. Il cliente effettua l’accesso al sito Web in un browser e il suo accesso mostra che il cliente è autorizzato a visualizzare il contenuto.
1. In base a quanto previsto dal server licenze, l&#39;applicazione genera un token di autenticazione.

   Questo valore viene passato a TVSDK.
1. TVSDK imposta questo valore nell’intestazione del cookie.
1. Quando TVSDK richiede al server di chiavi di ottenere una chiave per decifrare il contenuto, la richiesta contiene il valore di autenticazione nell&#39;intestazione del cookie.

   Il server chiavi è a conoscenza della validità della richiesta.

Per lavorare con i cookie:

1. Create un cookie `cookieManager` e aggiungete i cookie per gli URI al cookieStore.

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
   >Quando il reindirizzamento 302 è abilitato, la richiesta di annuncio può essere reindirizzata a un dominio diverso da quello al quale il cookie appartiene.

   TVSDK esegue una query `cookieManager` in fase di runtime, verifica se sono presenti cookie associati all&#39;URL e utilizza automaticamente tali cookie.

   Se i cookie devono essere aggiornati nell’applicazione durante la riproduzione, non utilizzate `networkConfiguration.setCookieHeaders` API in quanto l’aggiornamento si verificherà nello store di cookie JAVA.

   `networkConfiguration.setCookieHeaders` L&#39;API imposta i cookie su C++ CookieStore di TVSDK.

   Quando utilizzate i cookie JAVA e li condividete tra Application e TVSDK, utilizzate JAVA CookieStore per gestire i cookie esclusivamente.

   Prima che la riproduzione venga inizializzata, impostate i cookie su CookieStore utilizzando Cookie Manager come indicato sopra.

   Il cookie memorizzato in CookieStore verrà prelevato automaticamente da TVSDK.

   Se è necessario aggiornare il valore di un cookie in un secondo momento durante la riproduzione, chiamare lo stesso metodo add di CookieStore con la stessa chiave e un nuovo campo valore.

   Anche impostato
   `networkConfiguration.setReadSetCookieHeader`(false) prima della chiamata
   `config.setNetworkConfiguration(networkConfiguration)`

   >[!NOTE]
   Dopo aver impostato &#39;setReadSetCookieHeader&#39; su false, impostate i cookie per le richieste di chiave utilizzando il gestore di cookie JAVA.
   >
   `onCookiesUpdated(CookiesUpdatedEvent cookiesUpdatedEvent)`
Questa API di callback verrà attivata ogni volta che si verifica un aggiornamento nei cookie C++ (cookie provenienti dalla risposta http). L&#39;applicazione deve ascoltare questo callback e può aggiornare il loro JAVA CookieStore di conseguenza in modo che le chiamate di rete in JAVA possano utilizzare i cookie come segue:

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
