---
title: Migliore concatenamento delle licenze
description: Migliore concatenamento delle licenze
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# Migliore concatenamento delle licenze {#enhanced-license-chaining}

È possibile utilizzare il concatenamento avanzato delle licenze per aggiornare una licenza utilizzando una licenza radice padre per l&#39;aggiornamento batch delle licenze.

Primetime DRM 2.0 supporta il concatenamento delle licenze in cui le licenze foglia e radice sono associate a un computer specifico. Primetime DRM 3.0 e versioni successive supportano il concatenamento avanzato delle licenze, in cui una foglia è associata a una licenza radice e solo la licenza radice è associata a un computer o dominio specifico. Il concatenamento avanzato delle licenze supporta l’incorporazione di una licenza foglia con il contenuto e il client deve acquisire solo la licenza root dal server di licenze per utilizzare il contenuto protetto.

Se si desidera abilitare il concatenamento delle licenze avanzato, è necessario assegnare una chiave di crittografia radice a un criterio DRM di Primetime. La chiave di crittografia radice viene utilizzata per associare in modo crittografico la licenza foglia alla licenza radice.

>[!NOTE]
>
>Il concatenamento delle licenze avanzato è supportato dai client DRM Primetime versione 3.0 o successiva. Se un client precedente richiede una licenza per il contenuto che supporta il concatenamento delle licenze avanzato, il server licenze può comunque rilasciare una licenza a questo client utilizzando il concatenamento delle licenze supportato da Primetime DRM 2.0.

Caso d’uso di esempio: utilizza questa opzione per aggiornare tutte le licenze collegate scaricando una singola licenza root. Ad esempio, implementa modelli di abbonamento in cui il contenuto può essere riprodotto, purché l’utente rinnovi l’abbonamento su base mensile. Il vantaggio di questo approccio è che gli utenti devono acquisire un&#39;unica licenza per aggiornare tutte le loro licenze di abbonamento.
