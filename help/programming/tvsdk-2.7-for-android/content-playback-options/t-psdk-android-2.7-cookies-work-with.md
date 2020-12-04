---
description: Potete utilizzare TVSDK per inviare dati arbitrari nelle intestazioni dei cookie per la gestione delle sessioni, l'accesso ai gate e così via.
seo-description: Potete utilizzare TVSDK per inviare dati arbitrari nelle intestazioni dei cookie per la gestione delle sessioni, l'accesso ai gate e così via.
seo-title: Operazioni con i cookie
title: Operazioni con i cookie
uuid: a3b966fd-1263-458d-8303-b4e898372ee1
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---


# Utilizzare i cookie {#work-with-cookies}

Potete utilizzare TVSDK per inviare dati arbitrari nelle intestazioni dei cookie per la gestione delle sessioni, l&#39;accesso ai gate e così via.

Esempio di richiesta al server chiavi con autenticazione:

1. Il cliente effettua l’accesso al sito Web in un browser e il suo accesso mostra che il cliente è autorizzato a visualizzare il contenuto.
1. In base a quanto previsto dal server licenze, l&#39;applicazione genera un token di autenticazione.

   Questo valore viene passato a TVSDK.
1. TVSDK imposta questo valore nell’intestazione del cookie.
1. Quando TVSDK richiede al server di chiavi di ottenere una chiave per decifrare il contenuto, la richiesta contiene il valore di autenticazione nell&#39;intestazione del cookie.

   Il server chiavi è a conoscenza della validità della richiesta.

Per lavorare con i cookie:

Create un `cookieManager` e aggiungete i cookie per gli URI al cookieStore.

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

TVSDK esegue una query su questo `cookieManager` in fase di esecuzione, verifica se sono presenti cookie associati all&#39;URL e utilizza automaticamente tali cookie.

L’evento MediaPlayerEvent.COOKIES_UPDATED viene chiamato quando i cookie C++ vengono aggiornati. Questo cookiesUpdatedEvent dispone di un metodo getCookieString() che restituisce un valore di stringa per il cookie.

Segue un frammento di codice di esempio:

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

