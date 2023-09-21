---
title: Note sulla versione di Adobe Primetime authentication 2.64
description: Note sulla versione di Adobe Primetime authentication 2.64
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---

# Note sulla versione di Adobe Primetime authentication 2.64 {#authn-264-rn}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente di Adobe. Non è consentito alcun uso non autorizzato.

Questa pagina descrive nuove funzioni, modifiche e problemi noti relativi a questa versione:

## Client Web e lato server {#ss-web-clients}

* [Numero build](#build-no-264)
* [Nuove funzioni](#new-featres-264)
* [Correzioni di bug](#bug-fixes-264)


### Numero build {#build-no-264}

Autenticazione Adobe Primetime: adobe-pass-**2,64**

Data di rilascio: **11/08/2022 - 11/10/2022**

### Nuove funzioni {#new-featres-264}

* Aggiornamenti dell&#39;infrastruttura, con l&#39;obiettivo di ridurre i tempi di risposta dei server e migliorare le prestazioni complessive del sistema.
* Miglioramenti al nuovo meccanismo di identificazione delle piattaforme.
* Possibilità di bloccare le risposte di autenticazione non richieste provenienti da MVPD in cui il parametro &quot;in_response_to&quot; non è presente nell’asserzione SAML.

### Correzioni di bug {#bug-fixes-264}

* È stata corretta la formattazione errata di alcuni token TempPass legacy.
* Sono stati risolti alcuni problemi minori relativi al flusso di autenticazione nella seconda schermata.
