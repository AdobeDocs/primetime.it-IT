---
description: Puoi utilizzare TVSDK per inviare dati arbitrari nelle intestazioni dei cookie per la gestione delle sessioni, l'accesso ai gate e così via.
title: Utilizzare i cookie
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '236'
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

Crea un `cookieManager` e aggiungi i cookie per gli URI al tuo cookieStore.

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

L&#39;evento MediaPlayerEvent.COOKIES_UPDATED viene chiamato quando i cookie C++ vengono aggiornati. Questo cookiesUpdatedEvent dispone di un metodo getCookieString() che restituisce un valore stringa per il cookie.

Di seguito è riportato un frammento di codice di esempio:

```
private final CookiesUpdatedEventListener cookiesUpdatedEventListener = new CookiesUpdatedEventListener()  
{ 
@Override 
public void onCookiesUpdated(CookiesUpdatedEvent cookiesUpdatedEvent) 
 { 
 String cookieStr = cookiesUpdatedEvent.getCookieString();  
 logger.i(LOG_TAG + "::MediaPlayer.CookiesUpdatedEventListener#onCookiesUpdated()", "cookieStr " + cookieStr);  
 }  
};
```

