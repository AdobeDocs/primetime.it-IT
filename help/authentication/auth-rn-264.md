---
title: Note sulla versione di Adobe Primetime Authentication 2.64
description: Note sulla versione di Adobe Primetime Authentication 2.64
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---


# Note sulla versione di Adobe Primetime Authentication 2.64 {#authn-264-rn}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

Questa pagina descrive nuove funzioni, modifiche e problemi noti relativi a questa versione:

## Client lato server e Web {#ss-web-clients}

* [Numero build](#build-no-264)
* [Nuove funzioni](#new-featres-264)
* [Correzioni di bug](#bug-fixes-264)


### Numero build {#build-no-264}

Autenticazione Adobe Primetime: adobe-pass-**2,64**

Data di rilascio: **08/11/2022 - 10/11/2022**

### Nuove funzioni {#new-featres-264}

* Aggiornamenti dell&#39;infrastruttura mirati a ridurre i tempi di risposta dei server, a migliorare le prestazioni complessive del sistema.
* Miglioramenti al nuovo meccanismo di identificazione della piattaforma.
* Possibilità di bloccare le risposte di autenticazione non richieste dagli MVPD in cui manca il parametro &quot;in_response_to&quot; dall&#39;asserzione SAML.

### Correzioni di bug {#bug-fixes-264}

* È stata corretta la formattazione errata di alcuni token TempPass legacy.
* Sono stati risolti problemi minori nel flusso di autenticazione secondo schermo.
