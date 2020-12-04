---
description: 'null'
seo-description: 'null'
seo-title: File delle proprietà del server licenze
title: File delle proprietà del server licenze
uuid: 5e94ed1f-1dbf-4506-a097-183fcd5d25ef
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# File delle proprietà del server licenze{#license-server-properties-file}

Il server licenze fa riferimento alle proprietà impostate nel file [!DNL flashaccess-refimpl.properties]. È possibile fare riferimento direttamente a tale file per informazioni dettagliate su valori specifici e per informazioni sull&#39;utilizzo di ciascuna proprietà. Un esempio completamente funzionale è fornito nella directory [!DNL resources] dell&#39;implementazione di riferimento ( `([DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources/).`).

**Credenziali**  - Il file delle proprietà include impostazioni per la posizione delle credenziali che  Adobe ti rilascia. È possibile specificare queste credenziali in un file [!DNL .pfx] con una password, oppure fornire un alias e una password per una credenziale memorizzata in un HSM. È necessario almeno configurare le proprietà correlate alle credenziali di trasporto e alle credenziali del server licenze. Specificare le posizioni dei file delle credenziali relative alla directory specificata nella proprietà `config.resourcesDirectory`.

**Flash Media Rights Management Server**  - Il  `flashaccess-refimpl.properties` file include anche diverse proprietà correlate alla creazione di pacchetti di contenuto. Queste proprietà vengono utilizzate solo per la conversione dei metadati di Flash Media Rights Management Server 1.x. Dopo aver modificato i valori in questo file di proprietà, affinché le modifiche abbiano effetto, riavviare il server licenze.
