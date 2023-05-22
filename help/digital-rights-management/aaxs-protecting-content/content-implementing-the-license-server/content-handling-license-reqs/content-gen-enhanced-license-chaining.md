---
title: Concatenamento licenze migliorato
description: Concatenamento licenze migliorato
copied-description: true
exl-id: 4548cdc4-4a55-411b-ad22-8c77927f4564
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# Concatenamento licenze migliorato {#enhanced-license-chaining}

Con il concatenamento migliorato delle licenze in Adobe Access 3.0, si consiglia di emettere sia un Leaf che un Root la prima volta che l’utente richiede una licenza per una particolare macchina. Se l’utente dispone già della licenza Root, il server può emettere solo un Leaf (chiamata `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` per determinare se il client dispone già di una radice avanzata 3.0). Per le richieste di licenza successive, il client indicherà che dispone già di una licenza Leaf e di una licenza Root, pertanto il server deve rilasciare una nuova licenza Root. Quando si utilizza il concatenamento avanzato delle licenze, `setRootKeyRetrievalInfo()` è necessario chiamare per fornire le credenziali necessarie per decrittografare la chiave di crittografia radice nel criterio.

>[!NOTE]
>
>Se la policy supporta il concatenamento licenze avanzato 3.0, ma il client è Adobe Access 2.0, il server rilascerà una licenza concatenata originale 2.0. Per determinare la versione del client, utilizzare LicenseRequestMessage.getClientVersion().
