---
title: Generazione delle licenze
description: Generazione delle licenze
copied-description: true
exl-id: c47627b5-19de-41e5-8cb6-4084af714e09
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---

# Generazione delle licenze{#generating-licenses}

Se desideri rilasciare una licenza foglia a un utente, l’SDK deve decrittografare il CEK contenuto nei metadati del contenuto e crittografarlo nuovamente per il computer che richiede una licenza. Per decrittografare la chiave, il server deve fornire le informazioni necessarie per decrittografarla. Chiamata `ContentInfo.setKeyRetrievalInfo()` e forniscono un `AsymmetricKeyRetrieval` oggetto. Se i metadati includono più criteri, il server deve determinare quale criterio utilizzare e chiamare `LicenseRequestMessage.setSelectedPolicy()`. Quindi chiama `LicenseRequestMessage.generateLicense()` per generare la licenza. Utilizzo di `License` oggetto restituito, è possibile modificare la scadenza o i diritti nella licenza.

Se un `ExternalKeyRetrieval` l&#39;oggetto è specificato in `ContentInfo` , il server licenze deve utilizzare il CEK ID associato per recuperare il CEK appropriato inserito nella licenza.

Consulta la [Panoramica di Adobe Primetime DRM External CEK](../../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md) per ulteriori dettagli su come utilizzare il flusso di lavoro External CEK.
