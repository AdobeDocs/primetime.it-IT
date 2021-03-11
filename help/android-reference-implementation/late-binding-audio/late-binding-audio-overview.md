---
description: È possibile abilitare e creare controlli per il binding dell’audio in ritardo.
title: Panoramica
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---


# Panoramica {#overview}

È possibile abilitare e creare controlli per il binding dell’audio in ritardo.

Lo standard HLS consente flussi multiformato, il che significa che possiamo mantenere le tracce audio e video di un flusso separate l&#39;una dall&#39;altra. La traccia video, con più rappresentazioni (ad esempio 240p, 480p, 720p e 1080p) e le tracce audio (ad esempio, inglese, spagnolo, francese, tedesco) possono essere codificate separatamente. Il lettore multimediale sceglie quindi le tracce video e audio desiderate e le lega al volo, sul lato client.

Puoi implementare vari flussi di lavoro, a seconda dell’interfaccia utente del lettore. Il flusso di lavoro generale per il lettore Primetime è il seguente:

1. Quando l&#39;utente finale seleziona un video, viene compilato un elenco delle tracce audio disponibili per tale elemento multimediale.
1. Quando l’utente tocca il pulsante Impostazioni nell’interfaccia utente, vengono visualizzate le opzioni di traccia audio.
1. Quando viene selezionata una traccia audio, questa diventa la traccia audio attiva.
1. L&#39;utente finale può toccare il pulsante Impostazioni per tornare alla traccia audio originale.

