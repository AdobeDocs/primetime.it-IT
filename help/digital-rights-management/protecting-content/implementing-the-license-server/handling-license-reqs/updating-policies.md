---
title: Aggiornamento dei criteri DRM
description: Aggiornamento dei criteri DRM
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# Aggiornamento dei criteri DRM {#updating-drm-policies}

Se i criteri DRM vengono aggiornati dopo il pacchetto del contenuto, fornire i criteri DRM aggiornati al server licenze in modo che la versione aggiornata possa essere utilizzata durante il rilascio di una licenza. Se un server licenze ha accesso a un database per l&#39;archiviazione dei criteri DRM, è possibile recuperare i criteri DRM aggiornati dal database e chiamare `LicenseRequestMessage.setSelectedPolicy()` per fornire la nuova versione del criterio DRM.

Per i server licenze che non si basano su un database centrale, l&#39;SDK fornisce il supporto per gli elenchi di aggiornamento dei criteri DRM. Un elenco di aggiornamenti dei criteri DRM è un file che include un elenco di criteri DRM aggiornati o revocati. Quando si aggiorna un criterio DRM, generare un nuovo elenco di aggiornamento dei criteri DRM e inviare periodicamente l&#39;elenco a tutti i server licenze. Passa l’elenco all’SDK impostando `HandlerConfiguration.setPolicyUpdateList()`. Se viene fornito un elenco di aggiornamento, l’SDK lo consulta quando analizza i metadati del contenuto. `ContentInfo.getUpdatedPolicies()` include le versioni aggiornate dei criteri DRM specificati nei metadati.

Consulta [Utilizzo dei criteri DRM](../../../protecting-content/working-policies-overview/working-with-policies.md) e [Elenchi di aggiornamento criteri DRM](../../../protecting-content/working-policies-overview/policy-update-lists/working-with-policy-update-lists.md)
