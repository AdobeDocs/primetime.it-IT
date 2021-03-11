---
title: File delle proprietà del server licenze
description: File delle proprietà del server licenze
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---


# File delle proprietà del server licenze{#license-server-properties-file}

Il server licenze fa riferimento alle proprietà impostate nel file [!DNL flashaccess-refimpl.properties]. È possibile fare riferimento a tale file direttamente per informazioni dettagliate su valori specifici e per informazioni sull&#39;utilizzo di ciascuna proprietà. Un esempio completamente funzionale viene fornito nella directory [!DNL resources] dell’implementazione di riferimento ( `([DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources/).`).

**Credenziali**  - Il file delle proprietà include le impostazioni per la posizione delle credenziali che Adobe ti invia. È possibile specificare queste credenziali in un file [!DNL .pfx] con una password oppure fornire un alias e una password per una credenziale memorizzata in un HSM. È necessario almeno configurare le proprietà relative alle credenziali di trasporto e alle credenziali del server licenze. Specifica le posizioni dei file delle credenziali relative alla directory specificata nella proprietà `config.resourcesDirectory` .

**Flash Media Rights Management Server**  - Il  `flashaccess-refimpl.properties` file include anche diverse proprietà relative al contenuto del pacchetto. Queste proprietà vengono utilizzate solo per la conversione dei metadati Flash Media Rights Management Server 1.x. Dopo aver modificato i valori in questo file di proprietà, poiché le modifiche hanno effetto, riavvia il server licenze.
