---
seo-title: Concatenamento Delle Licenze Migliorato
title: Concatenamento Delle Licenze Migliorato
uuid: dc0e0a46-d3cd-44e8-a45d-3e22787be44e
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# Concatenamento delle licenze migliorato {#enhanced-license-chaining}

Con la catena delle licenze migliorata in  Adobe Access 3.0, si consiglia di rilasciare sia una foglia che una radice la prima volta che l&#39;utente richiede una licenza per un particolare computer. Se l&#39;utente dispone già della licenza Root, il server può emettere solo un comando Leaf (chiamare `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` per determinare se il client ha già una directory principale Enhanced 3.0). Per le richieste di licenza successive, il client indicherà che dispone già di una foglia e di una radice, pertanto il server dovrebbe emettere una nuova licenza Root. Quando si utilizza il concatenamento delle licenze avanzato, è necessario chiamare `setRootKeyRetrievalInfo()` per fornire le credenziali necessarie per decrittografare la chiave di crittografia principale nel criterio.

>[!NOTE]
>
>Se il criterio supporta il concatenamento delle licenze avanzato 3.0, ma il client è  Access 2.0 Adobe, il server rilascerà una licenza concatenata originale 2.0. Per determinare la versione client, utilizzate LicenseRequestMessage.getClientVersion().

