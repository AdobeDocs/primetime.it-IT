---
description: Da Flash 15 e versioni successive, quando il rendering hardware con StageVideo non è disponibile, StageVideo torna direttamente a un oggetto software StageVideo.
seo-description: Da Flash 15 e versioni successive, quando il rendering hardware con StageVideo non è disponibile, StageVideo torna direttamente a un oggetto software StageVideo.
seo-title: Supporto di Flash 15 per StageVideo
title: Supporto di Flash 15 per StageVideo
uuid: 49bd8703-016e-4fda-8773-5254d4774ec6
translation-type: tm+mt
source-git-commit: fd686391df0fa711bba99bc1bc312c9ef619f184

---


# Supporto di Flash 15 per StageVideo{#flash-support-for-stagevideo}

Da Flash 15 e versioni successive, quando il rendering hardware con StageVideo non è disponibile, StageVideo torna direttamente a un oggetto software StageVideo.

Tenete in considerazione le seguenti informazioni sul fallback video di Flash 15 StageVideo al software:

* Nell’applicazione non sono necessarie modifiche al codice.
* Non è richiesta alcuna modifica a TVSDK.

   Non è necessario un aggiornamento TVSDK per utilizzare il fallback StageVideo per il software.
* Le applicazioni devono essere ricompilate per Flash 15.
* Le applicazioni ricompilate per Flash 15 continueranno a funzionare con Flash 14 e versioni precedenti, purché non utilizzino nuove API introdotte in Flash Player 15.

   Se l&#39;applicazione Flash 14 deve utilizzare una nuova API Flash 15, è necessario chiamare in modo dinamico l&#39;API con un cast al tipo Object, in modo che l&#39;applicazione non si attivi in Flash Player 14 in fase di esecuzione.

## Sovrapposizioni HTML {#html-overlays}

In Flash 15 e versioni successive, potete mantenere una visualizzazione uniforme delle sovrapposizioni HTML quando l’hardware StageVideo diventa non disponibile e torna al software StageVideo. Per abilitare questa funzione, impostate `wmode=opaque`.

Alcuni browser meno recenti non supportano l&#39;accelerazione hardware. Per ulteriori informazioni su questi requisiti, consultate Requisiti [minimi di](../../../../../tvsdk-1.4-for-desktop-hls/c-psdk-dhls-1.4-introduction/overview-prod-audience-guide/requirements/stagevideo-capabilities/r-psdk-dhls-1.4-requirements-stage-video.md)StageVideo. Quando si imposta `wmode=opaque`, il video viene riprodotto con il software StageVideo, che può avere un impatto sulle prestazioni. In genere, l&#39;impostazione `wmode=direct` diretta esegue il rendering del video su GPU, ottenendo prestazioni migliori. Tuttavia, questa opzione sostituisce anche le sovrapposizioni HTML.
