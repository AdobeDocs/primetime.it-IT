---
title: File delle proprietà del server licenze
description: File delle proprietà del server licenze
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---

# File delle proprietà del server licenze{#license-server-properties-file}

Il server licenze fa riferimento alle proprietà impostate in [!DNL flashaccess-refimpl.properties] file. Puoi fare riferimento direttamente a tale file per informazioni dettagliate su valori specifici e per informazioni sull’utilizzo di ciascuna proprietà. Un campione pienamente funzionale è fornito nel [!DNL resources] directory dell&#39;implementazione di riferimento ( `([DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources/).`).

**Credenziali** : il file delle proprietà include le impostazioni relative alla posizione delle credenziali che Adobe ti invia. È possibile specificare queste credenziali in un [!DNL .pfx] o fornire un alias e una password per una credenziale memorizzata in un HSM. È necessario configurare almeno le proprietà correlate alle credenziali di trasporto e alle credenziali del server licenze. Specificare i percorsi dei file delle credenziali relativi alla directory specificata in `config.resourcesDirectory` proprietà.

**Server di Rights Management multimediale di Flash** - Il `flashaccess-refimpl.properties` Il file include anche diverse proprietà correlate alla creazione di pacchetti di contenuto. Queste proprietà vengono utilizzate solo per la conversione dei metadati 1.x di Flash Media Rights Management Server. Dopo aver modificato i valori in questo file di proprietà, per rendere effettive le modifiche, riavviare il server licenze.
