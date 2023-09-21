---
description: La playlist di un video può specificare un numero illimitato di tracce audio alternative per il contenuto video principale. Ad esempio, potrebbe essere utile aggiungere lingue diverse al contenuto video o consentire all'utente di passare da un brano all'altro del dispositivo durante la riproduzione del contenuto.
title: Brani audio alternativi nella playlist
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# Brani audio alternativi nella playlist{#alternate-audio-tracks-in-the-playlist}

La playlist di un video può specificare un numero illimitato di tracce audio alternative per il contenuto video principale. Ad esempio, potrebbe essere utile aggiungere lingue diverse al contenuto video o consentire all&#39;utente di passare da un brano all&#39;altro del dispositivo durante la riproduzione del contenuto.

Le tracce audio alternative, o l&#39;audio di associazione tardiva, consentono agli utenti di passare da una traccia in più lingue per i flussi video HTTP (live/linear e VOD) e non è necessario modificare, duplicare o ricompilare il video per ogni traccia audio. Puoi fornire tracce in più lingue per una risorsa video prima o dopo la sua creazione iniziale.

>[!TIP]
>
>Affinché l&#39;audio alternativo possa essere mixato con la traccia video del supporto principale, le marche temporali della traccia alternativa devono corrispondere a quelle dell&#39;audio nella traccia principale.

La traccia audio principale è inclusa nella raccolta di tracce audio con `default` etichetta. I metadati per i flussi audio alternativi sono inclusi nella playlist nel `#EXT-X-MEDIA` tag con `TYPE=AUDIO`.

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
