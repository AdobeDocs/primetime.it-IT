---
title: Come testare i flussi di autenticazione e autorizzazione utilizzando il sito di test API di Adobe
description: Come testare i flussi di autenticazione e autorizzazione utilizzando il sito di test API di Adobe
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---


# Come testare i flussi di autenticazione e autorizzazione utilizzando il sito di test API di Adobe {#How-to-test-auth-flows}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

Per testare i flussi AuthN e AuthZ, abbiamo preparato un **Sito di test API** che è a vostra disposizione. Il nostro team di supporto sarà lieto di fornirvi le credenziali. Puoi contattarci all&#39;indirizzo **support@tve.zendesk.com**.


## Parte I {#part-I}

Per eseguire test sull’ambiente RELEASE, passa direttamente alla parte II.  Per eseguire il test nell’ambiente di pre-qualificazione, vedi [Impostazione dell&#39;ambiente e test in Pre-Qual](/help/authentication/setting-up-your-environment-and-testing-in-prequal.md).

## Parte II

Dopo aver completato la parte I, effettua le seguenti operazioni:


1. Apri pagina Web: [Test API per staging](https://sp.auth-staging.adobe.com/apitest/api.html).
1. Carica l&#39;enabler di accesso dal seguente URL:
   * [Javascript per l&#39;abilitazione dell&#39;accesso per la gestione temporanea](https://entitlement.auth-staging.adobe.com/entitlement/js/AccessEnabler.js).
   * O
   * [Accesso enabler javascript per la produzione](https://entitlement.auth.adobe.com/entitlement/js/AccessEnabler.js).
   * Quindi fai clic su &quot;**Load Access Enabler**&quot; pulsante.
1. Ora imposta il valore id del richiedente su &quot;**requestorID**&quot; e fare clic sul pulsante &quot;setRequestor&quot;.
1. Dopo di che premere sul pulsante &quot;getAuthentication&quot; e attendere che il selettore di visualizzazione venga visualizzato.
1. Seleziona il &quot;**MVPD**&quot; dal picker.
1. Immetti le tue credenziali sul &quot;**MVPD**&quot; pagina di accesso.
1. Dopo essere stato reindirizzato indietro, ripristina i passaggi da 1 a 3
1. Dopo aver ripristinato il passaggio 3 di &quot;setAuthenticationStatus&quot;, dovresti visualizzare il valore &quot;1&quot;. Se l&#39;autenticazione non funziona, verrà visualizzata la finestra di dialogo MVPD.
1. Per verificare l’autorizzazione, nel campo di immissione della risorsa immetti &quot;**requestorID**&quot; e fare clic sul pulsante &quot;getAuthorization&quot;.
1. Di conseguenza, nella casella di testo &quot;setToken&quot;-\>&quot;resource id&quot; la risorsa verrà visualizzata e nella casella di testo &quot;setToken&quot;-\>&quot;token&quot; verrà visualizzato shortAuthorizationToken che significa che authZ ha avuto successo.
1. Ora puoi fare clic sul pulsante &quot;logout&quot; per eliminare i token.

