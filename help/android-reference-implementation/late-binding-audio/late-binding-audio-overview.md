---
description: È possibile abilitare e creare controlli per l'audio di associazione tardiva.
title: Panoramica
exl-id: be3b41c5-1c30-430c-9baa-06b6496aceb4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---

# Panoramica {#overview}

È possibile abilitare e creare controlli per l&#39;audio di associazione tardiva.

Lo standard HLS consente flussi multi-formato, il che significa che possiamo mantenere le tracce audio e video di un flusso separate l&#39;una dall&#39;altra. La traccia video, con rappresentazioni multiple (ad esempio, 240p, 480p, 720p e 1080p) e le tracce audio (ad esempio, inglese, spagnolo, francese, tedesco) possono essere codificate separatamente. Il lettore multimediale sceglie quindi le tracce audio e video desiderate e le associa al volo, sul lato client.

Puoi implementare vari flussi di lavoro, a seconda dell’interfaccia utente del lettore. Il flusso di lavoro generale per il lettore Primetime è il seguente:

1. Quando l’utente finale seleziona un video, viene compilato un elenco delle tracce audio disponibili per tale elemento multimediale.
1. Quando l’utente tocca il pulsante Settings (Impostazioni) nell’interfaccia utente, vengono visualizzate le opzioni per la traccia audio.
1. Quando è selezionata una traccia audio, la traccia diventa la traccia audio attiva.
1. L’utente finale può toccare il pulsante Settings (Impostazioni) per tornare alla traccia audio originale.
