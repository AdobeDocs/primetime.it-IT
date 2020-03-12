---
seo-title: Gestione di una whitelist di pacchetti di contenuti affidabili
title: Gestione di una whitelist di pacchetti di contenuti affidabili
uuid: ad40993c-15c3-43b2-9593-7b75802cfe69
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Gestione di una whitelist di pacchetti di contenuti affidabili{#maintain-a-whitelist-of-trusted-content-packagers}

Una *whitelist* è un elenco di entità affidabili. Nel caso dei pacchetti di contenuti, si tratta di organizzazioni fidate dal proprietario del contenuto per creare pacchetti (o cifrare) di file video FLV/F4V, creando contenuto protetto con DRM. Durante l&#39;implementazione di Adobe Access, si consiglia di mantenere una whitelist di content packager affidabili e di verificare l&#39;identità del packager di contenuti contenuto nei metadati DRM (l&#39;intestazione DRM) di un file protetto DRM prima di rilasciare una licenza.

Per ulteriori informazioni su come ottenere informazioni sull&#39;entità che crea il pacchetto di contenuto, vedere `V2ContentMetaData.getPackagerInfo()` nella Guida di riferimento *alle API di* Adobe Access.
