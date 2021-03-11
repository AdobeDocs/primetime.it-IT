---
title: Gestisci un elenco consentiti di pacchetti di contenuti affidabili
description: Gestisci un elenco consentiti di pacchetti di contenuti affidabili
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---


# Gestisci un elenco consentiti di pacchetti di contenuti affidabili {#maintain-a-allowlist-of-trusted-content-packagers}

Un **elenco consentiti** è un elenco di entità affidabili. Nel caso dei pacchetti di contenuti, si tratta di organizzazioni fidate dal proprietario del contenuto per creare pacchetti (o cifrare) di file video FLV/F4V, creando contenuti protetti da DRM. Durante la distribuzione di Adobe Access, si consiglia di mantenere un elenco consentiti di pacchetti di contenuti affidabili e di verificare l&#39;identità del content packager contenuto nei metadati DRM (l&#39;intestazione DRM) di un file protetto DRM prima di rilasciare una licenza.

Per ulteriori informazioni su come ottenere informazioni sull&#39;entità che ha creato il pacchetto di contenuti, consulta `V2ContentMetaData.getPackagerInfo()` in *Riferimento API di accesso agli Adobi*.
