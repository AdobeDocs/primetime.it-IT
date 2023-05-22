---
title: Aggiornamento dei criteri
description: Aggiornamento dei criteri
copied-description: true
exl-id: 0ea8d03b-68dd-415e-a75b-fd439bf858b6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# Aggiornamento dei criteri {#updating-policies}

Se i criteri vengono aggiornati dopo il pacchetto del contenuto, fornisci i criteri aggiornati al server licenze in modo che la versione aggiornata possa essere utilizzata durante il rilascio di una licenza. Se il server licenze ha accesso a un database per l&#39;archiviazione dei criteri, è possibile recuperare i criteri aggiornati dal database e chiamare `LicenseRequestMessage.setSelectedPolicy()` per fornire la nuova versione del criterio.

Per i server licenze che non si basano su un database centrale, l’SDK fornisce il supporto per gli elenchi di aggiornamento dei criteri. Un elenco di aggiornamento dei criteri è un file contenente un elenco di criteri aggiornati o revocati. Quando un criterio viene aggiornato, generare un nuovo elenco di aggiornamento dei criteri e inviarlo periodicamente a tutti i server licenze. Passa l’elenco all’SDK impostando `HandlerConfiguration.setPolicyUpdateList()`. Se viene fornito un elenco di aggiornamento, l’SDK lo consulta durante l’analisi dei metadati del contenuto. `ContentInfo.getUpdatedPolicies()` contiene le versioni aggiornate dei criteri specificati nei metadati.

Consulta [Utilizzo dei criteri](../../../aaxs-protecting-content/content-working-with-policies/content-working-with-policies-overview.md) e [Elenchi di aggiornamento dei criteri.](/help/digital-rights-management/protecting-content/working-policies-overview/policy-update-lists/working-with-policy-update-lists.md)
