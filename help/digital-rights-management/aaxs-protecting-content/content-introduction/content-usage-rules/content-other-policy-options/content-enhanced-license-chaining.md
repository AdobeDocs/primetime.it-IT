---
title: Concatena di licenze migliorata
description: Concatena di licenze migliorata
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---


# Caching avanzato delle licenze {#enhanced-license-chaining}

Consente di aggiornare una licenza utilizzando una licenza principale per l&#39;aggiornamento batch delle licenze.

Adobe Access 2.0 supporta la catena di licenze in cui le licenze foglia e radice sono legate a una macchina specifica. Adobe Access 3.0 supporta la catena di licenze avanzata, in cui una foglia è associata a una licenza radice e solo la licenza radice è associata a una macchina o a un dominio specifico. La catena di licenze avanzata supporta l’incorporazione di una licenza foglia con il contenuto e il client deve solo acquisire la licenza radice dal server licenze per utilizzare il contenuto protetto.

Per abilitare il concatenamento di licenze avanzato, al criterio viene assegnata una chiave di crittografia radice. La chiave di crittografia radice viene utilizzata per eseguire un binding crittografato della licenza foglia alla licenza radice.

>[!NOTE]
>
>La catena di licenze avanzata è supportata dai client Adobe Access versione 3.0 e successive. Se un client precedente richiede una licenza per contenuti che supportano il concatenamento di licenze avanzato, il server licenze può comunque rilasciare una licenza a questo client utilizzando il concatenamento di licenze supportato da Adobe Access 2.0.

Esempio di utilizzo: Utilizza questa opzione per aggiornare tutte le licenze collegate scaricando una singola licenza root. Ad esempio, implementa modelli di abbonamento in cui è possibile riprodurre il contenuto finché l’utente rinnova l’abbonamento su base mensile. Il vantaggio di questo approccio è che gli utenti devono effettuare una sola acquisizione di licenza per aggiornare tutte le licenze di abbonamento.
