---
title: Registrazione client dinamica
description: Registrazione client dinamica
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---


# Registrazione client dinamica {#dynamic-client-registration}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Contesto {#context}

Per allinearsi alle moderne pratiche di sicurezza, ai requisiti migliorati per i proprietari di UX e piattaforme, l’SDK per Android per autenticazione di Adobe Primetime e l’SDK per iOS si stanno muovendo nella direzione dell’adozione [Schede personalizzate Android Chrome](https://developer.chrome.com/multidevice/android/customtabs){target=_blank} and [Apple Safari view controller](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller){target=_blank}.

L’implementazione corrente di AdobePass utilizza visualizzazioni web specifiche per la piattaforma, al fine di fornire l’ambiente web per la visualizzazione della pagina di accesso MVPD. Queste visualizzazioni web non condividono la gestione delle credenziali con i browser della piattaforma, pertanto l&#39;utente non può utilizzare una password salvata dal browser quando si utilizza un&#39;applicazione di autenticazione Adobe Primetime. Inoltre, per motivi di sicurezza, alcune piattaforme si stanno spostando per rendere obsoleti i controller WebView per le attività di autenticazione. Sia Google che Apple forniscono opzioni alternative come &quot;Schede personalizzate Chrome&quot; e &quot;Controller visualizzazione Safari&quot;. Si tratta fondamentalmente di schede monouso dei rispettivi browser. L’autenticazione di Adobe Primetime adotterà questi nuovi componenti nel 2018.

## Dettagli {#details}

Al momento, sono disponibili due modi in cui Adobe Pass Authentication identifica e registra le applicazioni:

* i client basati su browser vengono registrati tramite l’elenco di domini consentiti
* i client delle applicazioni native, come le applicazioni iOS e Android, vengono registrati tramite il meccanismo di richiesta firmato.

Al fine di risolvere i nuovi flussi per Chrome Custom Tabs &amp; Safari View Controller, Adobe Pass propone un nuovo meccanismo di registrazione client per la registrazione di nuove applicazioni. Questo meccanismo consente un controllo più sicuro e granulare delle applicazioni e può essere utilizzato per registrare le applicazioni su tutte le piattaforme.

<!--
## Related Information

- [Dynamic Client Registration API](/help/authentication/dynamic-client-registration-api.md)
- [Dynamic Client Registration Management](/help/authentication/dynamic-client-registration-management.md)
-->