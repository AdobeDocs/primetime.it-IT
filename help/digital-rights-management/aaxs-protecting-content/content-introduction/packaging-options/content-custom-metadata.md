---
title: Metadati personalizzati
description: Metadati personalizzati
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---

# Metadati personalizzati {#custom-metadata}

**Specificare chiave/valore personalizzato da aggiungere ai metadati di contenuto che possono essere interpretati dall&#39;applicazione server.**

Il formato dei metadati del contenuto di Access di Adobe consente di includere coppie chiave/valore personalizzate in fase di creazione del pacchetto che devono essere elaborate dal server licenze durante il rilascio della licenza. Questi metadati sono separati dalla policy e possono essere univoci per ogni contenuto.

Caso d’uso di esempio: durante una fase Beta, includi la proprietà personalizzata &quot;Release:BETA&quot; al momento del packaging. I server di licenze possono distribuire licenze a questo contenuto durante il periodo Beta, ma dopo la scadenza del periodo Beta, i server di licenze non consentono l’accesso al contenuto.
