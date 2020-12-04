---
description: Potete attivare e creare controlli per il binding dell'audio in ritardo.
seo-description: Potete attivare e creare controlli per il binding dell'audio in ritardo.
seo-title: Panoramica
title: Panoramica
uuid: 7656f930-f426-426e-bcd4-dfa9d39e7ae4
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---


# Panoramica {#overview}

Potete attivare e creare controlli per il binding dell&#39;audio in ritardo.

Lo standard HLS consente flussi multi-formato, il che significa che possiamo tenere le tracce audio e video di un flusso separate l&#39;una dall&#39;altra. La traccia video, con più rappresentazioni (ad esempio, 240p, 480p, 720p e 1080p) e le tracce audio (ad esempio, inglese, spagnolo, francese, tedesco) possono essere codificate separatamente. Il lettore multimediale sceglie quindi i brani video e audio desiderati e li lega al volo, sul lato client.

È possibile implementare vari flussi di lavoro, a seconda dell&#39;interfaccia utente del lettore. Il flusso di lavoro generale per il lettore Primetime è il seguente:

1. Quando l&#39;utente finale seleziona un video, viene compilato un elenco delle tracce audio disponibili per tale elemento multimediale.
1. Quando l&#39;utente tocca il pulsante Impostazioni nell&#39;interfaccia utente, vengono visualizzate le opzioni della traccia audio.
1. Quando una traccia audio è selezionata, la traccia diventa la traccia audio attiva.
1. L&#39;utente finale può toccare il pulsante Impostazioni per tornare alla traccia audio originale.

