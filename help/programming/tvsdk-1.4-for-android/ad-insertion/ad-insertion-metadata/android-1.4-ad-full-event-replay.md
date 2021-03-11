---
description: La riproduzione a eventi completi (FER) è una risorsa VOD che agisce come risorsa live/DVR, pertanto l’applicazione deve adottare misure per garantire che gli annunci siano posizionati correttamente.
title: Abilitare gli annunci nella riproduzione completa degli eventi
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---


# Abilita gli annunci nella riproduzione a eventi completi{#enable-ads-in-full-event-replay}

La riproduzione a eventi completi (FER) è una risorsa VOD che agisce come risorsa live/DVR, pertanto l’applicazione deve adottare misure per garantire che gli annunci siano posizionati correttamente.

Per i contenuti live, TVSDK utilizza i metadati/suggerimenti nel manifesto per determinare dove collocare gli annunci. Tuttavia, a volte i contenuti live/lineari potrebbero assomigliare al contenuto VOD. Ad esempio, al completamento del contenuto live, al manifesto live viene aggiunto un tag `EXT-X-ENDLIST` . Per HLS, il tag `EXT-X-ENDLIST` indica che il flusso è un flusso VOD. TVSDK non è in grado di distinguere automaticamente questo flusso da un normale flusso VOD per inserire correttamente gli annunci.

L’applicazione deve indicare a TVSDK se il contenuto è live o VOD specificando il `AdSignalingMode`.

Per un flusso FER, il server Adobe Primetime ad decisioning non deve fornire l&#39;elenco delle interruzioni pubblicitarie che devono essere inserite nella timeline prima di avviare la riproduzione. Questo è il processo tipico per il contenuto VOD. Invece, specificando una modalità di segnalazione diversa, TVSDK legge tutti i punti di cue dal manifesto FER e va al server di annunci per ogni punto di cue per richiedere un&#39;interruzione pubblicitaria. Questo processo è simile al contenuto live/DVR.

Oltre a ogni richiesta associata a un punto di cue, TVSDK invia una richiesta aggiuntiva di annunci per annunci pre-roll.

1. Da un&#39;origine esterna, ad esempio vCMS, ottenere la modalità di segnalazione da utilizzare.
1. Crea i metadati relativi alla pubblicità.
1. Se il comportamento predefinito deve essere sovrascritto, specifica `AdSignalingMode` utilizzando `AdvertisingMetadata.setSignalingMode`.

   I valori validi sono `DEFAULT, SERVER_MAP` e `MANIFEST_CUES`.

   È necessario impostare la modalità di segnalazione degli annunci prima di chiamare `prepareToPlay`. Dopo che TVSDK inizia a risolvere e posizionare gli annunci sulla timeline, le modifiche alla modalità di segnalazione degli annunci vengono ignorate. Impostare la modalità quando si crea l&#39;oggetto `AuditudeSettings` .

1. Continua a riprodurre.

<!--<a id="example_3567B4A0D53E4DA99C10C13244454026"></a>-->

