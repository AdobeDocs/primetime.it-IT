---
title: Consumo di CRL generati localmente
description: Consumo di CRL generati localmente
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# Consumo di CRL generati localmente{#consume-locally-generated-crls}

Per utilizzare gli elenchi di revoche di certificati (CRL) generati localmente e gli elenchi di aggiornamento dei criteri, utilizza le API di accesso Adobe per verificare la firma. Le API verificano che gli elenchi non siano stati manomessi e che siano stati firmati dal server licenze corretto.

* Chiamata `RevocationList.verifySignature` per controllare la firma prima di fornire RevocationList a qualsiasi API.

  Per ulteriori informazioni, consulta `RevocationListFactory` nel *Riferimento API per l’accesso agli Adobi*.

* Chiamata `PolicyUpdateList.verifySignature`per verificare la firma prima di fornire `PolicyUpdateList` a qualsiasi API.

  Per ulteriori informazioni, consulta `PolicyUpdateList` nel *Riferimento API per l’accesso agli Adobi*.
