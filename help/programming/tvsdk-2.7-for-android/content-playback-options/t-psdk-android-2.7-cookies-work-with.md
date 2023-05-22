---
description: Puoi utilizzare TVSDK per inviare dati arbitrari nelle intestazioni dei cookie per la gestione delle sessioni, l’accesso ai gate e così via.
title: Utilizzare i cookie
exl-id: ea9d83f9-a047-4e24-98e5-f565b8a31a89
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '236'
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

Creare un `cookieManager` e aggiungi i cookie per gli URI al tuo cookieStore.

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

L&#39;evento MediaPlayerEvent.COOKIES_UPDATED viene chiamato quando vengono aggiornati i cookie C++. Questo cookiesUpdatedEvent ha un metodo getCookieString() che restituisce un valore stringa per il cookie.

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
