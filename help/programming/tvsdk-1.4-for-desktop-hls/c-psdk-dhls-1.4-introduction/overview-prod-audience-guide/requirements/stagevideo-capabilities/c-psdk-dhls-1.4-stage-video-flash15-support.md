---
description: A partire dall'Flash 15 e versioni successive, quando il rendering hardware con StageVideo non è disponibile, StageVideo torna direttamente a un oggetto software StageVideo.
seo-description: A partire dall'Flash 15 e versioni successive, quando il rendering hardware con StageVideo non è disponibile, StageVideo torna direttamente a un oggetto software StageVideo.
seo-title: Supporto Flash 15 per StageVideo
title: Supporto Flash 15 per StageVideo
uuid: 49bd8703-016e-4fda-8773-5254d4774ec6
translation-type: tm+mt
source-git-commit: fd686391df0fa711bba99bc1bc312c9ef619f184
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---


# Flash 15: supporto per StageVideo{#flash-support-for-stagevideo}

A partire dall&#39;Flash 15 e versioni successive, quando il rendering hardware con StageVideo non è disponibile, StageVideo torna direttamente a un oggetto software StageVideo.

Considerate le seguenti informazioni sul fallback Flash 15 StageVideo al software:

* Nell’applicazione non sono necessarie modifiche al codice.
* Non è richiesta alcuna modifica a TVSDK.

   Non è necessario un aggiornamento TVSDK per utilizzare il fallback StageVideo per il software.
* Le applicazioni devono essere ricompilate per l&#39;Flash 15.
* Le applicazioni ricompilate per l&#39;Flash 15 continueranno a funzionare con l&#39;Flash 14 e versioni precedenti, purché non utilizzino nuove API introdotte nell&#39;Flash Player 15.

   Se l&#39;applicazione di Flash 14 deve utilizzare una nuova API Flash 15, è necessario chiamare dinamicamente l&#39;API con un cast al tipo Object, in modo che l&#39;applicazione non si verifichi un errore Flash Player 14 in fase di esecuzione.

## Sovrapposizioni HTML {#html-overlays}

Negli Flash 15 e versioni successive, potete mantenere una visualizzazione uniforme delle sovrapposizioni HTML quando l’hardware StageVideo diventa non disponibile e torna al software StageVideo. Per abilitare questa funzione, impostare `wmode=opaque`.

Alcuni browser meno recenti non supportano l&#39;accelerazione hardware. Per ulteriori informazioni su questi requisiti, vedere [Requisiti minimi di StageVideo](../../../../../tvsdk-1.4-for-desktop-hls/c-psdk-dhls-1.4-introduction/overview-prod-audience-guide/requirements/stagevideo-capabilities/r-psdk-dhls-1.4-requirements-stage-video.md). Quando si imposta `wmode=opaque`, il video viene riprodotto con il software StageVideo, che può avere un impatto sulle prestazioni. In genere, l&#39;impostazione di `wmode=direct` esegue il rendering diretto del video su GPU, ottenendo prestazioni migliori. Tuttavia, questa opzione sostituisce anche le sovrapposizioni HTML.
