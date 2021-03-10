---
title: Generazione di licenze
description: Generazione di licenze
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---


# Generazione di licenze{#generating-licenses}

Se desideri rilasciare una licenza foglia a un utente, l’SDK deve decrittografare la CEK contenuta nei metadati del contenuto e ricrittografarla per il computer che richiede una licenza. Per decrittografare la CEK, il server deve fornire le informazioni necessarie per decrittografare la chiave. Chiama `ContentInfo.setKeyRetrievalInfo()` e fornisci un oggetto `AsymmetricKeyRetrieval`. Se i metadati includono più criteri, il server deve determinare quali criteri utilizzare e chiamare `LicenseRequestMessage.setSelectedPolicy()`. Quindi chiama `LicenseRequestMessage.generateLicense()` per generare la licenza. Utilizzando l&#39;oggetto `License` restituito, puoi modificare la scadenza o i diritti nella licenza.

Se nell&#39;oggetto `ContentInfo` è specificato un oggetto `ExternalKeyRetrieval`, il server licenze deve utilizzare l&#39;ID CEK associato per recuperare il CEK appropriato inserito nella licenza.

Per ulteriori informazioni su come utilizzare il flusso di lavoro CEK esterno, consulta la [Panoramica CEK esterna Adobe Primetime DRM](../../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md) .
