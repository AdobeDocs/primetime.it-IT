---
title: Metadati personalizzati
description: Metadati personalizzati
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---

# Metadati personalizzati {#custom-metadata}

Utilizza questa opzione per aggiungere coppie chiave/valore personalizzate ai metadati di contenuto che possono essere interpretati dall’applicazione server.

Il formato dei metadati per il contenuto DRM di Primetime consente di includere coppie chiave/valore personalizzate al momento della creazione del pacchetto. Questi metadati personalizzati possono quindi essere elaborati dal server licenze durante il rilascio della licenza. I metadati sono distinti da una regola DRM di Primetime e possono essere univoci per ogni sezione di contenuto.

Caso d’uso di esempio: durante una fase Beta, puoi includere la proprietà personalizzata `Release:BETA` al momento del confezionamento. I server di licenze possono distribuire licenze a questo contenuto durante il periodo Beta. Tuttavia, dopo la scadenza del periodo Beta, i server di licenze non consentono l’accesso al contenuto.
