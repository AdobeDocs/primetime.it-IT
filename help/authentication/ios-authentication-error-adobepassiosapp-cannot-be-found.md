---
title: Errore Di Autenticazione iOS - Impossibile Trovare adobepass.ios.app
description: Errore Di Autenticazione iOS - Impossibile Trovare adobepass.ios.app
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# Errore Di Autenticazione iOS - Impossibile Trovare adobepass.ios.app {#ios-authentication-error-adobepass.ios.app-cannot-be-found}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Problema {#issue}

L&#39;utente sta attraversando il flusso di autenticazione e dopo aver immesso le proprie credenziali con il proprio provider viene reindirizzato a una pagina di errore, a una pagina di ricerca o a un&#39;altra pagina personalizzata per informarli che `adobepass.ios.app` impossibile trovare/risolvere.

## Spiegazione {#explanation}

Su iOS, `adobepass.ios.app` viene utilizzato come URL di reindirizzamento finale per indicare che il flusso AuthN è completo. A questo punto l’app deve effettuare una richiesta ad AccessEnabler per ottenere il token AuthN e finalizzare il flusso AuthN.

Il problema è che `adobepass.ios.app` in realtà non esiste e verrà attivato un messaggio di errore nel `webView`. Le versioni precedenti di iOS DemoApp presupponevano che questo errore sarebbe sempre stato attivato alla fine del flusso AuthN ed era configurato per gestirlo di conseguenza (`indidFailLoadWithError`).

**Nota:** Questo problema è stato risolto nelle versioni successive di DemoApp (incluso nel download dell&#39;SDK di iOS).

Sfortunatamente, questo presupposto NON è corretto. Esistono alcuni dei cosiddetti server DNS o Proxy &quot;intelligenti&quot; che non passano semplicemente l&#39;errore generato, ma eseguono invece una delle seguenti operazioni: 

- Creare una pagina di errore personalizzata
- Consente di inoltrare a una pagina di ricerca o a un altro tipo di pagina o portale del cliente.

In questi casi, la risposta che ritorna ad iOS webView sarà una risposta perfettamente valida per quanto riguarda webView e NON attiverà l&#39;errore a cui dipendeva la vecchia DemoApp.

## Soluzione {#solution}

NON fare la stessa supposizione di DemoApp. Invece, intercetta la richiesta prima che venga eseguita (in `shouldStartLoadWithRequest`) e gestirla in modo appropriato.

Esempio di come intercettare la richiesta prima che venga eseguita:

```obj-c
- (BOOL)webView:(UIWebView*)localWebView shouldStartLoadWithRequest:(NSURLRequest*)request navigationType:(UIWebViewNavigationType)navigationType {

NSString *absolutePath = [[request URL] absoluteString]; 
if ([absolutePath isEqualToString:ADOBEPASS_REDIRECT_URL] && ![APP_DELEGATE getAuthenticationWasCalled]) {

// user was logged ok => call getAuthenticationToken() 
[APP_DELEGATE setGetAuthenticationWasCalled:YES]; 
[[APP_DELEGATE accessEnabler] getAuthenticationToken];
return NO;

}

return YES;

}
```

Alcuni aspetti da tenere presente:

- NON utilizzare mai `adobepass.ios.app` direttamente in qualsiasi punto del codice. Utilizza invece la costante `ADOBEPASS_REDIRECT_URL`
- La `return NO;` impedirà il caricamento della pagina
- Assicurati che il `getAuthenticationToken` La chiamata viene chiamata una volta e solo una volta nel codice. Chiamate multiple a `getAuthenticationToken` produrrà risultati non definiti.

