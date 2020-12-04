---
description: La riproduzione a tutti gli eventi (FER) è una risorsa VOD che funge da risorsa live/DVR, pertanto l’applicazione deve adottare misure per garantire che gli annunci vengano inseriti correttamente.
seo-description: La riproduzione a tutti gli eventi (FER) è una risorsa VOD che funge da risorsa live/DVR, pertanto l’applicazione deve adottare misure per garantire che gli annunci vengano inseriti correttamente.
seo-title: Abilitare gli annunci nella riproduzione a tutti gli eventi
title: Abilitare gli annunci nella riproduzione a tutti gli eventi
uuid: 70e463bd-332c-4f91-ac05-03e79c0939a4
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---


# Abilitare gli annunci nella riproduzione a tutti gli eventi{#enable-ads-in-full-event-replay}

La riproduzione a tutti gli eventi (FER) è una risorsa VOD che funge da risorsa live/DVR, pertanto l’applicazione deve adottare misure per garantire che gli annunci vengano inseriti correttamente.

Per i contenuti live, TVSDK utilizza i metadati/suggerimenti presenti nel manifesto per determinare dove inserire gli annunci. Tuttavia, a volte i contenuti live/lineari possono assomigliare ai contenuti VOD. Ad esempio, al termine del contenuto live, al manifesto live viene aggiunto un tag `EXT-X-ENDLIST`. Per HLS, il tag `EXT-X-ENDLIST` indica che il flusso è un flusso VOD. TVSDK non è in grado di distinguere automaticamente questo flusso da un normale flusso VOD per inserire correttamente gli annunci.

L&#39;applicazione deve indicare a TVSDK se il contenuto è live o VOD specificando il `AdSignalingMode`.

Per un flusso FER, il server di gestione annunci  Adobe Primetime non deve fornire l&#39;elenco delle interruzioni pubblicitarie che devono essere inserite nella timeline prima di avviare la riproduzione. Questo è il processo tipico per il contenuto VOD. Al contrario, specificando una diversa modalità di segnalazione, TVSDK legge tutti i cue point dal manifesto FER e va al server di annunci per ogni cue point per richiedere un&#39;interruzione annuncio. Questo processo è simile al contenuto live/DVR.

Oltre a ogni richiesta associata a un cue point, TVSDK invia una richiesta aggiuntiva per annunci pre-roll.

1. Da un&#39;origine esterna, come vCMS, ottenete la modalità di segnalazione da utilizzare.
1. Create i metadati relativi alla pubblicità.
1. Se il comportamento predefinito deve essere sovrascritto, specificare il `AdSignalingMode` utilizzando `AdvertisingMetadata.setSignalingMode`.

   I valori validi sono `DEFAULT, SERVER_MAP` e `MANIFEST_CUES`.

   È necessario impostare la modalità di segnalazione degli annunci prima di chiamare `prepareToPlay`. Dopo che TVSDK ha iniziato a risolvere e inserire gli annunci sulla timeline, le modifiche alla modalità di segnalazione degli annunci vengono ignorate. Impostare la modalità quando si crea l&#39;oggetto `AuditudeSettings`.

1. Continua a riprodurre.

<!--<a id="example_3567B4A0D53E4DA99C10C13244454026"></a>-->

