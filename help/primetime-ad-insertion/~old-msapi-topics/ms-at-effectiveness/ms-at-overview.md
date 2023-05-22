---
description: La maggior parte degli inserzionisti richiede informazioni dettagliate su quando, per quanto tempo e con quale successo sono stati visualizzati i loro annunci. L’approccio più efficiente consiste nell’richiedere al lettore client di inviare rapporti durante la riproduzione degli annunci, ma il server manifesto supporta anche il tracciamento degli annunci lato server e ibridi.
title: Tracciamento degli annunci
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# Tracciamento degli annunci {#ad-tracking}

La maggior parte degli inserzionisti richiede informazioni dettagliate su quando, per quanto tempo e con quale successo sono stati visualizzati i loro annunci. L’approccio più efficiente consiste nell’richiedere al lettore client di inviare rapporti durante la riproduzione degli annunci, ma il server manifesto supporta anche il tracciamento degli annunci lato server e ibridi.

Quando si abilita il tracciamento degli annunci, il client specifica uno dei seguenti approcci:

* **Lato client** Insieme alla playlist con unione di annunci, il server invia al client una struttura JSON, VMAP o in-manifest che specifica gli eventi di tracciamento e gli URL. Questo metodo è compatibile con Interactive Advertising Bureau (IAB)

* **Lato server** Il client non partecipa al tracciamento degli annunci. Il server invia tutte le informazioni di tracciamento degli annunci possibili. I dati di tracciamento vengono calcolati solo sul lato server e potrebbero non corrispondere con l’attività di riproduzione sul lato client. Ad esempio, se un utente finale non visualizza l’intero annuncio, dopo la distribuzione dei segmenti il server considera comunque l’annuncio da riprodurre.

* **Ibrido** È simile al tracciamento lato client, ma il client invia i propri rapporti al server manifesto, che li inoltra agli URL appropriati. Gli inserzionisti ricevono le stesse informazioni del tracciamento lato client. Questa modalità consente ai client in esecuzione con accesso a Internet limitato.