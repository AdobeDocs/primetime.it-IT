---
title: Supporto WKWebView su iOS SDK 3.1+
description: Supporto WKWebView su iOS SDK 3.1+
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---


# Supporto WKWebView su iOS SDK 3.1+ {#wkwebview-support-on-ios-sdk-3.1}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

</br>

**A causa della deprecazione di UIWebView da parte di Apple su iOS, abbiamo aggiornato iOS SDK 3.1 con il supporto per WKWebView.**

## Compatibilità {#compatibility}

A partire dalla versione 3.1 dell&#39;SDK per iOS, le implementazioni possono ora utilizzare WKWebView o UIWebView in modo intercambiabile. Poiché UIWebView è obsoleto per Apple, le app devono migrare a WKWebView, per evitare problemi con le versioni future di iOS.

Nota che la migrazione implicherebbe semplicemente il passaggio della classe UIWebView con WKWebView, non c&#39;è lavoro specifico da fare per quanto riguarda AccessEnabler di Adobe.

## Problemi noti {#known-issues}

AccessEnabler di Adobe ha utilizzato un&#39;istanza UIWebView interna nascosta per eseguire &quot;[autenticazione passiva](/help/authentication/sso-passive-authn.md)&quot; per alcuni MVPD. Il flusso &quot;passivo&quot; è stato utile per gli MVPD che richiedono l’autenticazione per ogni requestor id e da questo flusso hanno beneficiato i programmatori che hanno utilizzato lo stesso ID team in più applicazioni iOS al fine di simulare un’esperienza SSO (Adobe SSO). Questa funzione è attualmente utilizzata da un numero limitato di MVPD.

La funzione utilizzava un comportamento di UIWebView che consentiva ad Adobe di acquisire i cookie di autenticazione e di riprodurli durante il flusso &quot;passivo&quot;. WKWebView introduce una sicurezza più forte che impedisce ad Adobe di acquisire i cookie impostati al momento dell&#39;accesso e di riprodurli utilizzando un&#39;istanza nascosta di WKWebView. A causa di questo miglioramento della sicurezza e considerando che il flusso &quot;passivo&quot; ha beneficiato solo di un set molto limitato di MVPD in uno scenario di implementazione molto specifico (più applicazioni che utilizzano lo stesso ID del team), l&#39;Adobe ha rimosso la funzione di &quot;autenticazione passiva&quot; per gli MVPD che utilizzano webview per l&#39;autenticazione.

La funzione è ancora presente per gli MVPD configurati per utilizzare SFSafariViewController, ma si noti che in questo caso l&#39;autenticazione &quot;passiva&quot; sarà visibile all&#39;utente in quanto SFSafariViewController non può essere utilizzato in modo &quot;nascosto&quot;.
