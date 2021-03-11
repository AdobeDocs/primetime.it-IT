---
title: Aggiornamento dei criteri DRM
description: Aggiornamento dei criteri DRM
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---


# Aggiornamento dei criteri DRM {#updating-drm-policies}

Se i criteri DRM vengono aggiornati dopo il pacchetto del contenuto, fornisci i criteri DRM aggiornati al server licenze in modo che la versione aggiornata possa essere utilizzata quando si rilascia una licenza. Se un server licenze ha accesso a un database per la memorizzazione dei criteri DRM, è possibile recuperare il criterio DRM aggiornato dal database e chiamare `LicenseRequestMessage.setSelectedPolicy()` per fornire la nuova versione del criterio DRM.

Per i server di licenza che non si basano su un database centrale, l&#39;SDK fornisce il supporto per gli elenchi di aggiornamento dei criteri DRM. Un elenco di aggiornamento dei criteri DRM è un file che include un elenco di criteri DRM aggiornati o revocati. Quando un criterio DRM viene aggiornato, genera un nuovo elenco di aggiornamento dei criteri DRM e invia periodicamente l’elenco a tutti i server di licenza. Passa l&#39;elenco all&#39;SDK impostando `HandlerConfiguration.setPolicyUpdateList()`. Se viene fornito un elenco di aggiornamenti, l’SDK lo consulta quando analizza i metadati del contenuto. `ContentInfo.getUpdatedPolicies()` include le versioni aggiornate dei criteri DRM specificati nei metadati.

Consulta [Utilizzo dei criteri DRM](../../../protecting-content/working-policies-overview/working-with-policies.md) e [Elenchi di aggiornamento dei criteri DRM](../../../protecting-content/working-policies-overview/policy-update-lists/working-with-policy-update-lists.md)