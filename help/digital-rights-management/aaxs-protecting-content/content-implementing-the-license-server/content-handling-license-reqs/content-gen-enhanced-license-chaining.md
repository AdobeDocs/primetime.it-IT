---
title: Concatena delle licenze migliorata
description: Concatena delle licenze migliorata
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# Concatena delle licenze migliorata {#enhanced-license-chaining}

Con una catena di licenze migliorata in Adobe Access 3.0, si consiglia di rilasciare sia una foglia che una radice la prima volta che l&#39;utente richiede una licenza per un particolare computer. Se l&#39;utente dispone già della licenza Root, il server può emettere solo una chiamata Leaf (chiamare `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` per determinare se il client dispone già di una radice Enhanced 3.0). Per le richieste di licenza successive, il client indicherà che dispone già di una foglia e di una radice, pertanto il server dovrebbe rilasciare una nuova licenza Root. Quando si utilizza il concatenamento di licenze avanzato, `setRootKeyRetrievalInfo()` deve essere chiamato per fornire le credenziali necessarie per decrittografare la chiave di crittografia radice nel criterio.

>[!NOTE]
>
>Se il criterio supporta il concatenamento licenze avanzato 3.0, ma il client è Adobe Access 2.0, il server rilascerà una licenza concatenata originale 2.0. Per determinare la versione client, utilizzare LicenseRequestMessage.getClientVersion().

