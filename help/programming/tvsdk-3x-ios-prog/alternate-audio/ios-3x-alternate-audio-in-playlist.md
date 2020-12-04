---
description: L’audio alternativo o in fase di rilegatura successiva consente di passare dalle tracce audio disponibili per una traccia video. In questo modo, gli utenti possono selezionare una traccia della lingua durante la riproduzione del video.
seo-description: L’audio alternativo o in fase di rilegatura successiva consente di passare dalle tracce audio disponibili per una traccia video. In questo modo, gli utenti possono selezionare una traccia della lingua durante la riproduzione del video.
seo-title: Tracce audio alternative nella playlist
title: Tracce audio alternative nella playlist
uuid: 6241d3e4-6e07-44fb-bc0e-5d49d1a76824
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---


# Tracce audio alternative nella playlist {#section_BC8C1C74A5A24A8CA68C1E7E721EE742}

La playlist di un video può specificare un numero illimitato di tracce audio alternative per il contenuto video principale. Ad esempio, potrebbe essere utile aggiungere lingue diverse al contenuto video o consentire all&#39;utente di passare da un&#39;altra traccia del dispositivo all&#39;altra durante la riproduzione del contenuto.

Le tracce audio alternative, o l&#39;audio con rilegatura successiva, consentono agli utenti di passare da una traccia video HTTP all&#39;altra in più lingue (dal vivo/lineare e dal VOD) e non è necessario modificare, duplicare o riassemblare il video per ciascuna traccia audio. Potete fornire tracce in più lingue per una risorsa video prima o dopo la creazione del pacchetto iniziale della risorsa.

>[!TIP]
>
>Affinché l’audio alternativo sia associato alla traccia video del supporto principale, le marche temporali della traccia alternativa devono corrispondere alle marche temporali dell’audio nella traccia principale.

I seguenti requisiti si applicano se utilizzate tracce audio alternative e incorporate pubblicità:

* Se il contenuto principale contiene tracce audio alternative, gli annunci devono avere almeno un flusso solo audio.
* Ogni durata del segmento del flusso solo audio di un annuncio deve essere uguale alla durata del segmento del flusso video di un annuncio.

La traccia audio principale è inclusa nella raccolta di tracce audio con l&#39;etichetta `default`. I metadati per i flussi audio alternativi sono inclusi nella playlist nei tag `#EXT-X-MEDIA` con `TYPE=AUDIO`.

Ad esempio, un manifesto M3U8 che specifica più flussi audio alternativi potrebbe essere simile al seguente:

```
#EXTM3U 
#EXT-X-MEDIA:TYPE=AUDIO,GROUP-ID="bipbop_audio",LANGUAGE="eng",NAME="BipBop Audio 1", 
 AUTOSELECT=YES,DEFAULT=YES 
#EXT-X-MEDIA:TYPE=AUDIO,GROUP-ID="bipbop_audio",LANGUAGE="eng",NAME="BipBop Audio 2", 
 AUTOSELECT=NO,DEFAULT=NO,URI="alternate_audio_aac/prog_index.m3u8" 
#EXT-X-MEDIA:TYPE=SUBTITLES,GROUP-ID="subs",NAME="English",AUTOSELECT=YES,FORCED=NO, 
 LANGUAGE="eng",URI="subtitles/eng/prog_index.m3u8" 
#EXT-X-MEDIA:TYPE=SUBTITLES,GROUP-ID="subs",NAME="English (Forced)",DEFAULT=YES, 
 AUTOSELECT=YES,FORCED=YES,LANGUAGE="eng",URI="subtitles/eng_forced/prog_index.m3u8" 
#EXT-X-MEDIA:TYPE=SUBTITLES,GROUP-ID="subs",NAME="Français",AUTOSELECT=YES,FORCED=NO, 
 LANGUAGE="fra",URI="subtitles/fra/prog_index.m3u8" 
#EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=263851,CODECS="mp4a.40.2, avc1.4d400d", 
 RESOLUTION=416x234,AUDIO="bipbop_audio",SUBTITLES="subs"  
gear1/prog_index.m3u8 
#EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=577610,CODECS="mp4a.40.2, avc1.4d401e", 
 RESOLUTION=640x360,AUDIO="bipbop_audio",SUBTITLES="subs" 
gear2/prog_index.m3u8 
... 
```
