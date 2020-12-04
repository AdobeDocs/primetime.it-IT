---
seo-title: Aggiornamento dei criteri
title: Aggiornamento dei criteri
uuid: f6686c8b-bedf-4ec5-a14e-f03326519f89
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# Aggiornamento dei criteri {#updating-policies}

Se i criteri vengono aggiornati dopo che il contenuto è stato creato, fornite i criteri aggiornati al server licenze in modo che la versione aggiornata possa essere utilizzata al momento del rilascio della licenza. Se il server licenze dispone dell&#39;accesso a un database per la memorizzazione dei criteri, è possibile recuperare il criterio aggiornato dal database e chiamare `LicenseRequestMessage.setSelectedPolicy()` per fornire la nuova versione del criterio.

Per i server di licenze che non si basano su un database centrale, l&#39;SDK fornisce il supporto per gli elenchi degli aggiornamenti dei criteri. Un elenco di aggiornamento dei criteri è un file contenente un elenco di criteri aggiornati o revocati. Quando un criterio viene aggiornato, generate un nuovo elenco di aggiornamento criteri e inviate periodicamente l&#39;elenco a tutti i server licenze. Passa l&#39;elenco all&#39;SDK impostando `HandlerConfiguration.setPolicyUpdateList()`. Se viene fornito un elenco di aggiornamenti, l’SDK lo consulta quando analizza i metadati del contenuto. `ContentInfo.getUpdatedPolicies()` contiene le versioni aggiornate dei criteri specificati nei metadati.

Vedere [Utilizzo degli elenchi di criteri](../../../aaxs-protecting-content/content-working-with-policies/content-working-with-policies-overview.md) e [aggiornamento dei criteri.](/help/digital-rights-management/protecting-content/working-policies-overview/policy-update-lists/working-with-policy-update-lists.md)
