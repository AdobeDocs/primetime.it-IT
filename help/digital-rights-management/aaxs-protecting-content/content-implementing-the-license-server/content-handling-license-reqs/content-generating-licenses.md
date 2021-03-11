---
title: Generazione di licenze
description: Generazione di licenze
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---


# Generazione di licenze {#generating-licenses}

Per rilasciare una licenza foglia all&#39;utente, l&#39;SDK deve decrittografare il CEK contenuto nei metadati del contenuto e ricrittografarlo per il computer che richiede una licenza. Per decrittografare la CEK, il server deve fornire le informazioni necessarie per decrittografare la chiave. Chiama `ContentInfo.setKeyRetrievalInfo()` e fornisci un oggetto `AsymmetricKeyRetrieval`. Se i metadati contengono più criteri, il server deve determinare quali criteri utilizzare e chiamare `LicenseRequestMessage.setSelectedPolicy()`. Quindi chiama `LicenseRequestMessage.generateLicense()` per generare la licenza. Utilizzando l&#39;oggetto `License` restituito, puoi modificare la scadenza o i diritti nella licenza.

Se nell&#39;oggetto `ContentInfo` è specificato un oggetto ExternalKeyRetrieval, il server di licenze deve utilizzare l&#39;ID CEK associato per recuperare il CEK appropriato che verrà inserito nella licenza. Per ulteriori dettagli su come utilizzare il flusso di lavoro CEK esterno, consulta [Panoramica di accesso Adobe DRM CEK esterno](../../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md)
