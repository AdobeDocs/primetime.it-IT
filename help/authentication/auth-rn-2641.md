---
title: Note sulla versione di Adobe Primetime authentication 2.64.1
description: Note sulla versione di Adobe Primetime authentication 2.64.1
exl-id: b0edbd90-ebb5-40a7-9034-1699dccfadb5
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---

# Note sulla versione di Adobe Primetime authentication 2.64.1 {#authn-264-rn}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente di Adobe. Non è consentito alcun uso non autorizzato.

Questa pagina descrive nuove funzioni, modifiche e problemi noti relativi a questa versione:

## Client Web e lato server {#server-side-web-clients-2641}

* [Numero build](#build-number-2641)
* [Panoramica sulla versione](#release-overview-2641)

### Numero build {#build-number-2641}

Autenticazione Adobe Primetime: adobe-pass-**2.64.1**
Data di rilascio: **01/31/2023 - 02/02/2023**

### Panoramica sulla versione {#release-overview-2641}

Questa versione aggiunge quanto segue:

* Possibilità di bloccare le risposte di autenticazione non richieste provenienti da MVPD in cui il parametro &quot;in_response_to&quot; non è presente nell’asserzione SAML.
* È stata migliorata la convalida sul parametro redirect_url per garantire la conformità ai requisiti di sicurezza.
* È stata migliorata la registrazione delle informazioni sul dispositivo per le richieste di autenticazione della seconda schermata, utilizzando le informazioni fornite dal dispositivo iniziale.
