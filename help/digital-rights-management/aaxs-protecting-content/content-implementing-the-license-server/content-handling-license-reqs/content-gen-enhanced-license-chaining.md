---
seo-title: Concatenamento Delle Licenze Migliorato
title: Concatenamento Delle Licenze Migliorato
uuid: dc0e0a46-d3cd-44e8-a45d-3e22787be44e
translation-type: tm+mt
source-git-commit: da8736769f7b47318dbd955aa854f83ae64d6d7b

---


# Concatenamento Delle Licenze Migliorato {#enhanced-license-chaining}

Con la concatenazione delle licenze avanzata in Adobe Access 3.0, si consiglia di rilasciare sia una foglia che una radice la prima volta che l&#39;utente richiede una licenza per un particolare computer. Se l&#39;utente dispone già della licenza Root, il server può emettere solo una chiamata Leaf (per determinare se il client dispone già di una radice Enhanced 3.0). `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` Per le richieste di licenza successive, il client indicherà che dispone già di una foglia e di una radice, pertanto il server dovrebbe emettere una nuova licenza Root. Quando si utilizza il concatenamento di licenze avanzato, `setRootKeyRetrievalInfo()` deve essere chiamato per fornire le credenziali necessarie per decifrare la chiave di crittografia principale nel criterio.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Se il criterio supporta il concatenamento delle licenze avanzato 3.0, ma il client è Adobe Access 2.0, il server rilascerà una licenza concatenata originale 2.0. Per determinare la versione client, utilizzate LicenseRequestMessage.getClientVersion().

