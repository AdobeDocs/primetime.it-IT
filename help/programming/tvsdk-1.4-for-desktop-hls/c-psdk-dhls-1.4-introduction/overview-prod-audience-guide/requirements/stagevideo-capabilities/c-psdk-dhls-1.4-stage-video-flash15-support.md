---
description: Dal Flash 15 in poi, quando non è disponibile il rendering hardware con StageVideo, StageVideo torna direttamente a un oggetto StageVideo software.
title: Supporto Flash 15 per StageVideo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---

# Supporto Flash 15 per StageVideo{#flash-support-for-stagevideo}

Dal Flash 15 in poi, quando non è disponibile il rendering hardware con StageVideo, StageVideo torna direttamente a un oggetto StageVideo software.

Considera le seguenti informazioni sul fallback Flash 15 StageVideo al software:

* Non sono richieste modifiche al codice nell&#39;applicazione.
* Non è richiesta alcuna modifica a TVSDK.

  Non è necessario un aggiornamento TVSDK per utilizzare StageVideo di fallback al software.
* Le applicazioni devono essere ricompilate per il Flash 15.
* Le applicazioni ricompilate per il Flash 15 continueranno a funzionare con il Flash 14 e versioni precedenti, purché non utilizzino nuove API introdotte nel Flash Player 15.

  Se l’applicazione Flash 14 deve utilizzare una nuova API Flash 15, è necessario chiamare dinamicamente l’API con un cast al tipo Oggetto, in modo che l’applicazione non abbia esito negativo nel Flash Player 14 in fase di esecuzione.

## Sovrapposizioni HTML {#html-overlays}

Nel Flash 15 e versioni successive, è possibile mantenere una visualizzazione perfetta delle sovrapposizioni HTML quando l&#39;hardware StageVideo non è più disponibile e torna al software StageVideo. Per abilitare questa funzione, impostare `wmode=opaque`.

Alcuni browser meno recenti non supportano l&#39;accelerazione hardware. Per ulteriori informazioni su questi requisiti, consulta [Requisiti minimi di StageVideo](../../../../../tvsdk-1.4-for-desktop-hls/c-psdk-dhls-1.4-introduction/overview-prod-audience-guide/requirements/stagevideo-capabilities/r-psdk-dhls-1.4-requirements-stage-video.md). Quando si imposta `wmode=opaque`, il video viene renderizzato con il software StageVideo, che può influire sulle prestazioni. In genere, l&#39;impostazione `wmode=direct` esegue direttamente il rendering del video nella GPU, ottenendo prestazioni molto migliori. Tuttavia, questa opzione sostituisce anche le sovrapposizioni HTML.
