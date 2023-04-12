---
title: Note sulla versione di Adobe Primetime authentication 2.64.1
description: Note sulla versione di Adobe Primetime authentication 2.64.1
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---


# Note sulla versione di Adobe Primetime authentication 2.64.1 {#authn-264-rn}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

Questa pagina descrive nuove funzioni, modifiche e problemi noti relativi a questa versione:

## Client lato server e Web {#server-side-web-clients-2641}

* [Numero build](#build-number-2641)
* [Panoramica sulla versione](#release-overview-2641)

### Numero build {#build-number-2641}

Autenticazione Adobe Primetime: adobe-pass-**2.64.1**
Data di rilascio: **31/01/2023 - 02/02/2023**

### Panoramica sulla versione {#release-overview-2641}

Questa versione aggiunge quanto segue:

* La capacità di bloccare le risposte di autenticazione non richieste dagli MVPD in cui il parametro &quot;in_response_to&quot; è mancante dall&#39;asserzione SAML.
* È stata migliorata la convalida rispetto al parametro redirect_url al fine di soddisfare i requisiti di sicurezza.
* Registrazione migliorata delle informazioni sul dispositivo per le richieste di autenticazione a seconda schermata, utilizzando le informazioni fornite dal dispositivo iniziale.
