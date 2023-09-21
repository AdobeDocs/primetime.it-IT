---
title: Registrazione client dinamici
description: Registrazione client dinamici
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# Registrazione client dinamici {#dynamic-client-registration}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente di Adobe. Non è consentito alcun uso non autorizzato.

## Contesto {#context}

Per allinearsi alle moderne procedure di sicurezza, ai requisiti più avanzati per l’interfaccia utente e i proprietari della piattaforma, l’SDK Android per l’autenticazione di Adobe Primetime e l’SDK di iOS si stanno muovendo nella direzione dell’adozione [Schede personalizzate Android Chrome](https://developer.chrome.com/multidevice/android/customtabs){target=_blank} and [Apple Safari view controller](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller){target=_blank}.

L’attuale implementazione di AdobePass utilizza visualizzazioni web specifiche per piattaforma, al fine di fornire l’ambiente web per visualizzare la pagina di accesso MVPD. Queste visualizzazioni Web non condividono la gestione delle credenziali con i browser della piattaforma, pertanto l’utente non può utilizzare una password salvata dal browser quando utilizza un’applicazione di autenticazione Adobe Primetime. Inoltre, per motivi di sicurezza, alcune piattaforme stanno per rendere obsoleti i controller WebView per le attività di autenticazione. Sia Google che Apple forniscono opzioni alternative, ad esempio &quot;Chrome Custom Tabs&quot; e &quot;Safari View Controller&quot;. Si tratta fondamentalmente di schede monouso dei rispettivi browser. L’autenticazione Adobe Primetime adotterà questi nuovi componenti nel 2018.

## Dettagli {#details}

Attualmente, l’autenticazione Adobe Pass identifica e registra le applicazioni in due modi:

* i client basati su browser vengono registrati tramite l’elenco dei domini consentiti
* i client delle applicazioni native, come le applicazioni iOS e Android, vengono registrati tramite il meccanismo del richiedente firmato

Per gestire i nuovi flussi per le schede personalizzate di Chrome e il controller di visualizzazione Safari, Adobe Pass propone un nuovo meccanismo di registrazione client per la registrazione di nuove applicazioni. Questo meccanismo consentirà un controllo più sicuro e granulare delle applicazioni e può essere utilizzato per registrare le applicazioni su tutte le piattaforme.

<!--
## Related Information

- [Dynamic Client Registration API](/help/authentication/dynamic-client-registration-api.md)
- [Dynamic Client Registration Management](/help/authentication/dynamic-client-registration-management.md)
-->
