---
title: Gestisci un elenco consentiti di pacchetti di contenuti attendibili
description: Gestisci un elenco consentiti di pacchetti di contenuti attendibili
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---

# Gestisci un elenco consentiti di pacchetti di contenuti attendibili {#maintain-a-allowlist-of-trusted-content-packagers}

Un **elenco consentiti** è un elenco di entità attendibili. Nel caso dei pacchetti di contenuti, si tratta di organizzazioni considerate attendibili dal proprietario del contenuto per creare pacchetti (o crittografare) di file video FLV/F4V, creando contenuti protetti da DRM. Durante la distribuzione di Adobe Access, si consiglia di mantenere un elenco consentiti di pacchetti di contenuti attendibili e di verificare l&#39;identità del pacchetto di contenuti contenuto contenuto nei metadati DRM (intestazione DRM) di un file protetto DRM prima di rilasciare una licenza.

Per ulteriori informazioni su come ottenere informazioni sull’entità che ha creato il pacchetto del contenuto, consulta `V2ContentMetaData.getPackagerInfo()` nel *Riferimento API per l’accesso agli Adobi*.
