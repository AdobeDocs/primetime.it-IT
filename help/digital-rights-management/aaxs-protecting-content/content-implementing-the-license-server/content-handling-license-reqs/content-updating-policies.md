---
title: Aggiornamento dei criteri
description: Aggiornamento dei criteri
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# Aggiornamento dei criteri {#updating-policies}

Se i criteri vengono aggiornati dopo il pacchetto del contenuto, fornisci i criteri aggiornati al server licenze in modo che la versione aggiornata possa essere utilizzata al momento del rilascio di una licenza. Se il server licenze dispone dell&#39;accesso a un database per la memorizzazione dei criteri, è possibile recuperare il criterio aggiornato dal database e chiamare `LicenseRequestMessage.setSelectedPolicy()` per fornire la nuova versione del criterio.

Per i server di licenza che non si basano su un database centrale, l&#39;SDK fornisce il supporto per gli elenchi di aggiornamento dei criteri. Un elenco di aggiornamento dei criteri è un file contenente un elenco di criteri aggiornati o revocati. Quando un criterio viene aggiornato, genera un nuovo elenco di aggiornamento dei criteri e invia periodicamente l’elenco a tutti i server di licenza. Passa l&#39;elenco all&#39;SDK impostando `HandlerConfiguration.setPolicyUpdateList()`. Se viene fornito un elenco di aggiornamenti, l’SDK lo consulta quando analizza i metadati del contenuto. `ContentInfo.getUpdatedPolicies()` contiene le versioni aggiornate dei criteri specificati nei metadati.

Vedere [Uso dei criteri](../../../aaxs-protecting-content/content-working-with-policies/content-working-with-policies-overview.md) e [Elenchi di aggiornamento dei criteri.](/help/digital-rights-management/protecting-content/working-policies-overview/policy-update-lists/working-with-policy-update-lists.md)
