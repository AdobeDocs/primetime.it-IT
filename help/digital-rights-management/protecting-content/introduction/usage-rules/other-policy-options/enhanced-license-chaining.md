---
title: Concatena di licenze migliorata
description: Concatena di licenze migliorata
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---


# Caching avanzato delle licenze {#enhanced-license-chaining}

È possibile utilizzare una catena di licenze avanzata per aggiornare una licenza utilizzando una licenza principale per l&#39;aggiornamento batch delle licenze.

Primetime DRM 2.0 supporta la concatenazione delle licenze in cui sia le licenze foglia che root sono legate a una macchina specifica. Primetime DRM 3.0 e versioni successive supporta il miglioramento della concatenazione delle licenze, in cui una foglia è associata a una licenza root e solo la licenza root è associata a una macchina o a un dominio specifico. La catena di licenze avanzata supporta l’incorporazione di una licenza foglia con il contenuto e il client deve solo acquisire la licenza radice dal server licenze per utilizzare il contenuto protetto.

Se desideri abilitare il concatenamento di licenze avanzato, devi assegnare una chiave di crittografia principale a un criterio DRM di Primetime. La chiave di crittografia radice viene utilizzata per eseguire un binding crittografato della licenza foglia alla licenza radice.

>[!NOTE]
>
>La catena di licenze migliorata è supportata dai client DRM di Primetime versione 3.0 o successiva. Se un client precedente richiede una licenza per contenuti che supportano la catena di licenze avanzata, il server licenze può comunque rilasciare una licenza a questo client utilizzando la catena di licenze supportata da Primetime DRM 2.0.

Esempio di utilizzo: Utilizza questa opzione per aggiornare tutte le licenze collegate scaricando una singola licenza root. Ad esempio, implementa modelli di abbonamento in cui è possibile riprodurre il contenuto finché l’utente rinnova l’abbonamento su base mensile. Il vantaggio di questo approccio è che gli utenti devono solo acquisire una singola licenza per aggiornare tutte le loro licenze di abbonamento.
