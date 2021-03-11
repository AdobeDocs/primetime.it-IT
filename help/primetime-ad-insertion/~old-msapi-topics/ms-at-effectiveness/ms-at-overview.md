---
description: La maggior parte degli inserzionisti richiede alcune informazioni dettagliate su quando, per quanto tempo e con quale successo sono stati visualizzati i loro annunci. L'approccio più efficiente è quello di far sì che il lettore client invii i report mentre riproduce gli annunci, ma il server manifest supporta anche il server-side e il tracciamento degli annunci ibridi.
title: Tracciamento degli annunci
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# Tracciamento annunci {#ad-tracking}

La maggior parte degli inserzionisti richiede alcune informazioni dettagliate su quando, per quanto tempo e con quale successo sono stati visualizzati i loro annunci. L&#39;approccio più efficiente è quello di far sì che il lettore client invii i report mentre riproduce gli annunci, ma il server manifest supporta anche il server-side e il tracciamento degli annunci ibridi.

Quando si abilita il tracciamento degli annunci, il client specifica uno dei seguenti approcci:

* **Lato clientInsieme** alla playlist con punti ad, il server invia al client una struttura JSON, VMAP o in-manifest specificando eventi di tracciamento e URL. Questo metodo è conforme a IAB (Interactive Advertising Bureau)

* **Server** sideIl client non partecipa al tracciamento degli annunci. Il server invia tutte le informazioni di tracciamento degli annunci che può. I dati di tracciamento vengono calcolati solo sul lato server e potrebbero non corrispondere all’attività di riproduzione sul lato client. Ad esempio, se un utente finale non visualizza l’intero annuncio, dopo la distribuzione dei segmenti, il server considera comunque l’annuncio da riprodurre.

* **** HybridSimile al tracciamento lato client, ma il client invia i propri report al server manifest, che li inoltra agli URL appropriati. Gli inserzionisti ricevono le stesse informazioni del tracciamento lato client. Questa modalità gestisce i client in esecuzione con accesso Internet limitato.