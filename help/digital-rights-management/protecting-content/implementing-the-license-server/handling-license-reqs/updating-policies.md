---
seo-title: Aggiornamento dei criteri DRM
title: Aggiornamento dei criteri DRM
uuid: 6f7a1432-88e4-499b-a008-6c8cf0e9c09b
translation-type: tm+mt
source-git-commit: d5986e9bc8689bf37abdf242a41aea5e768df754
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---


# Aggiornamento dei criteri DRM {#updating-drm-policies}

Se i criteri DRM vengono aggiornati dopo il pacchetto del contenuto, fornite i criteri DRM aggiornati al server licenze in modo che la versione aggiornata possa essere utilizzata al momento del rilascio di una licenza. Se un server licenze dispone dell&#39;accesso a un database per la memorizzazione dei criteri DRM, è possibile recuperare il criterio DRM aggiornato dal database e chiamare `LicenseRequestMessage.setSelectedPolicy()` per fornire la nuova versione del criterio DRM.

Per i server di licenze che non si basano su un database centrale, l&#39;SDK fornisce il supporto per gli elenchi degli aggiornamenti dei criteri DRM. Un elenco di aggiornamento dei criteri DRM è un file che include un elenco di criteri DRM aggiornati o revocati. Quando un criterio DRM viene aggiornato, genera un nuovo elenco di aggiornamento criteri DRM e invia periodicamente l&#39;elenco a tutti i server licenze. Passa l&#39;elenco all&#39;SDK impostando `HandlerConfiguration.setPolicyUpdateList()`. Se viene fornito un elenco di aggiornamenti, l’SDK lo consulta quando analizza i metadati del contenuto. `ContentInfo.getUpdatedPolicies()` include le versioni aggiornate dei criteri DRM specificati nei metadati.

Vedere [Utilizzo di criteri DRM](../../../protecting-content/working-policies-overview/working-with-policies.md) e [elenchi di aggiornamenti dei criteri DRM](../../../protecting-content/working-policies-overview/policy-update-lists/working-with-policy-update-lists.md)