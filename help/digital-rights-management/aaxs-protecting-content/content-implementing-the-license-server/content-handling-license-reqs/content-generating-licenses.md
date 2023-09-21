---
title: Generazione delle licenze
description: Generazione delle licenze
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# Generazione delle licenze {#generating-licenses}

Per rilasciare una licenza foglia all’utente, l’SDK deve decrittografare il CEK contenuto nei metadati del contenuto e crittografarlo nuovamente per il computer che richiede una licenza. Per decrittografare la chiave, il server deve fornire le informazioni necessarie per decrittografarla. Chiamata `ContentInfo.setKeyRetrievalInfo()` e forniscono un `AsymmetricKeyRetrieval` oggetto. Se i metadati contengono più criteri, il server deve determinare quale criterio utilizzare e chiamare `LicenseRequestMessage.setSelectedPolicy()`. Quindi chiama `LicenseRequestMessage.generateLicense()` per generare la licenza. Utilizzo di `License` oggetto restituito, è possibile modificare la scadenza o i diritti nella licenza.

Se in è specificato un oggetto ExternalKeyRetrieval `ContentInfo` , il server licenze deve utilizzare l&#39;ID CEK associato per recuperare il CEK appropriato che verrà inserito nella licenza. Per ulteriori dettagli su come utilizzare il flusso di lavoro External CEK, consulta [Panoramica sul controllo esterno DRM di accesso Adobe](../../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md)
