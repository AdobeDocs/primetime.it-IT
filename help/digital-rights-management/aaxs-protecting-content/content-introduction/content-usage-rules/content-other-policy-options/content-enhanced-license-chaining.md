---
title: Migliore concatenamento delle licenze
description: Migliore concatenamento delle licenze
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---

# Migliore concatenamento delle licenze {#enhanced-license-chaining}

Consente di aggiornare una licenza utilizzando una licenza radice padre per l&#39;aggiornamento in batch delle licenze.

Adobe Access 2.0 supporta il concatenamento delle licenze in cui le licenze foglia e radice sono associate a un computer specifico. Adobe Access 3.0 supporta il concatenamento avanzato delle licenze, in cui una foglia è associata a una licenza radice e solo la licenza radice è associata a un computer o dominio specifico. Il concatenamento avanzato delle licenze supporta l’incorporamento della licenza foglia con il contenuto e il client deve acquisire solo la licenza root dal server licenze per utilizzare il contenuto protetto.

Per abilitare il concatenamento avanzato delle licenze, al criterio viene assegnata una chiave di crittografia radice. La chiave di crittografia radice viene utilizzata per associare in modo crittografico la licenza foglia alla licenza radice.

>[!NOTE]
>
>Il concatenamento avanzato delle licenze è supportato dai client Adobe Access versione 3.0 e successive. Se un client meno recente richiede una licenza per il contenuto che supporta il concatenamento delle licenze avanzato, il server licenze può comunque rilasciare una licenza a questo client utilizzando il concatenamento delle licenze supportato dall&#39;Adobe Access 2.0.

Caso d’uso di esempio: utilizza questa opzione per aggiornare tutte le licenze collegate scaricando una singola licenza root. Ad esempio, implementa modelli di abbonamento in cui il contenuto può essere riprodotto, purché l’utente rinnovi l’abbonamento su base mensile. Il vantaggio di questo approccio è che gli utenti devono effettuare un&#39;unica acquisizione della licenza per aggiornare tutte le loro licenze di abbonamento.
