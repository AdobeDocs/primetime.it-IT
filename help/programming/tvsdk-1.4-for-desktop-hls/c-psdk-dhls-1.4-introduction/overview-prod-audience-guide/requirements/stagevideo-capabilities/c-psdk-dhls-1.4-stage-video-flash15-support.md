---
description: Dal Flash 15 e versioni successive, quando il rendering hardware con StageVideo non è disponibile, StageVideo torna direttamente a un oggetto software StageVideo.
title: Supporto di Flash 15 per StageVideo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---


# Supporto di Flash 15 per StageVideo{#flash-support-for-stagevideo}

Dal Flash 15 e versioni successive, quando il rendering hardware con StageVideo non è disponibile, StageVideo torna direttamente a un oggetto software StageVideo.

Considera le seguenti informazioni sul fallback Flash 15 StageVideo al software:

* Nell&#39;applicazione non sono necessarie modifiche al codice.
* Non è richiesta alcuna modifica a TVSDK.

   Non è necessario un aggiornamento TVSDK per utilizzare il fallback StageVideo al software.
* Le tue applicazioni devono essere ricompilate per il Flash 15.
* Le applicazioni ricompilate per il Flash 15 continueranno a funzionare con i Flash 14 e precedenti, purché non utilizzino nuove API introdotte nel Flash Player 15.

   Se l’applicazione Flash 14 deve utilizzare una nuova API Flash 15, è necessario chiamare dinamicamente l’API con un cast al tipo di oggetto, in modo che l’applicazione non abbia esito negativo nel Flash Player 14 in fase di esecuzione.

## Sovrapposizioni HTML {#html-overlays}

Nel Flash 15 e versioni successive, è possibile mantenere una visualizzazione perfetta delle sovrapposizioni HTML quando l&#39;hardware StageVideo diventa non disponibile e torna al software StageVideo. Per abilitare questa funzione, imposta `wmode=opaque`.

Alcuni browser meno recenti non supportano l&#39;accelerazione hardware. Per ulteriori informazioni su questi requisiti, consulta [Requisiti minimi di StageVideo](../../../../../tvsdk-1.4-for-desktop-hls/c-psdk-dhls-1.4-introduction/overview-prod-audience-guide/requirements/stagevideo-capabilities/r-psdk-dhls-1.4-requirements-stage-video.md). Quando si imposta `wmode=opaque`, il video viene riprodotto con il software StageVideo, che può influire sulle prestazioni. In genere, l’impostazione `wmode=direct` esegue il rendering diretto del video su GPU, ottenendo prestazioni molto migliori. Tuttavia, questa opzione sostituisce anche le sovrapposizioni HTML.
