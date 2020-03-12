---
seo-title: Consumo di CRL generati localmente
title: Consumo di CRL generati localmente
uuid: 5a4519b8-6dbd-4921-9048-6c9f67aae18d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Consumo di CRL generati localmente{#consume-locally-generated-crls}

Per utilizzare elenchi di revoche di certificati (CRL, Certificate Revocation List) generati localmente ed elenchi di aggiornamenti di criteri, utilizzare le API di Adobe Access per verificare la firma. Le API verificano che gli elenchi non siano stati alterati e che siano stati firmati dal server licenze corretto.

* Chiamare `RevocationList.verifySignature` per controllare la firma prima di fornire RevocationList a qualsiasi API.

   Per ulteriori informazioni, consulta `RevocationListFactory` la Guida di riferimento *alle API di* Adobe Access.

* Chiamata `PolicyUpdateList.verifySignature`per controllare la firma prima di fornire l&#39; `PolicyUpdateList` ID a qualsiasi API.

   Per ulteriori informazioni, consulta `PolicyUpdateList` la Guida di riferimento *alle API di* Adobe Access.

