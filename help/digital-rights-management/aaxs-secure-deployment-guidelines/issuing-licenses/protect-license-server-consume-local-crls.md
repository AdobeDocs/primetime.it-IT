---
title: Consuma CRL generati localmente
description: Consuma CRL generati localmente
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---


# Consuma CRL generati localmente{#consume-locally-generated-crls}

Per utilizzare elenchi di revoche di certificati (CRL) generati localmente e elenchi di aggiornamenti dei criteri, utilizzare le API di accesso di Adobe per verificare la firma. Le API verificano che gli elenchi non siano stati manomessi e che siano stati firmati dal server licenze corretto.

* Chiama `RevocationList.verifySignature` per controllare la firma prima di fornire RevocationList a qualsiasi API.

   Per ulteriori informazioni, consulta `RevocationListFactory` in *Riferimento API di accesso agli Adobi*.

* Chiama `PolicyUpdateList.verifySignature`per controllare la firma prima di fornire `PolicyUpdateList` a qualsiasi API.

   Per ulteriori informazioni, consulta `PolicyUpdateList` in *Riferimento API di accesso agli Adobi*.

