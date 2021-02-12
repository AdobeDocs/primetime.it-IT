---
description: La maggior parte degli inserzionisti richiede alcune informazioni dettagliate su quando, per quanto tempo e con quale successo sono stati visualizzati i loro annunci. L'approccio più efficace consiste nell'inviare i report al lettore client durante la riproduzione degli annunci, ma il server manifesto supporta anche il monitoraggio degli annunci ibridi e lato server.
seo-description: La maggior parte degli inserzionisti richiede alcune informazioni dettagliate su quando, per quanto tempo e con quale successo sono stati visualizzati i loro annunci. L'approccio più efficace consiste nell'inviare i report al lettore client durante la riproduzione degli annunci, ma il server manifesto supporta anche il monitoraggio degli annunci ibridi e lato server.
seo-title: Tracciamento annunci
title: Tracciamento annunci
uuid: 184b8c36-5e51-42a7-b905-53f2b7b15e49
translation-type: tm+mt
source-git-commit: e437f4143fb939f46d106c64efc391137c33fe17
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---


# Tracciamento annunci {#ad-tracking}

La maggior parte degli inserzionisti richiede alcune informazioni dettagliate su quando, per quanto tempo e con quale successo sono stati visualizzati i loro annunci. L&#39;approccio più efficace consiste nell&#39;inviare i report al lettore client durante la riproduzione degli annunci, ma il server manifesto supporta anche il monitoraggio degli annunci ibridi e lato server.

Quando si abilita il tracciamento annunci, il client specifica uno dei seguenti approcci:

* **Lato client** Insieme alla playlist con punti annuncio, il server invia al client una struttura JSON, VMAP o in-manifest che specifica eventi di tracciamento e URL. Questo metodo è compatibile con IAB (Interactive Advertising Bureau)

* **Lato serverIl client non partecipa al tracciamento degli annunci.** Il server invia qualsiasi informazione di tracciamento annunci sia possibile. I dati di tracciamento sono calcolati solo sul lato server e potrebbero non corrispondere all&#39;attività di riproduzione sul lato client. Ad esempio, se un utente finale non visualizza l’intero annuncio, dopo la distribuzione dei segmenti, il server considera comunque l’annuncio da riprodurre.

* **** Ibrido: è simile al tracciamento lato client, ma il client invia i propri rapporti al server manifesto, che li invia agli URL appropriati. Gli inserzionisti ricevono le stesse informazioni del tracciamento lato client. Questa modalità consente ai client in esecuzione con accesso Internet limitato.