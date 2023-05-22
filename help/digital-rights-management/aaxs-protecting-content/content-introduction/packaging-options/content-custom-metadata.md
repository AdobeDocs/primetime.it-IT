---
title: Metadati personalizzati
description: Metadati personalizzati
copied-description: true
exl-id: d7783420-b345-44de-8f22-a16dda5d7554
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---

# Metadati personalizzati {#custom-metadata}

**Specificare chiave/valore personalizzato da aggiungere ai metadati di contenuto che possono essere interpretati dall&#39;applicazione server.**

Il formato dei metadati del contenuto di Access di Adobe consente di includere coppie chiave/valore personalizzate in fase di creazione del pacchetto che devono essere elaborate dal server licenze durante il rilascio della licenza. Questi metadati sono separati dalla policy e possono essere univoci per ogni contenuto.

Caso d’uso di esempio: durante una fase Beta, includi la proprietà personalizzata &quot;Release:BETA&quot; al momento del packaging. I server di licenze possono distribuire licenze a questo contenuto durante il periodo Beta, ma dopo la scadenza del periodo Beta, i server di licenze non consentono l’accesso al contenuto.
