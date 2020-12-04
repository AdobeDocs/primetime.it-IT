---
description: La playlist di un video può specificare un numero illimitato di tracce audio alternative per il contenuto video principale. Ad esempio, potrebbe essere utile aggiungere lingue diverse al contenuto video o consentire all'utente di passare da un'altra traccia del dispositivo all'altra durante la riproduzione del contenuto.
seo-description: La playlist di un video può specificare un numero illimitato di tracce audio alternative per il contenuto video principale. Ad esempio, potrebbe essere utile aggiungere lingue diverse al contenuto video o consentire all'utente di passare da un'altra traccia del dispositivo all'altra durante la riproduzione del contenuto.
seo-title: Tracce audio alternative nella playlist
title: Tracce audio alternative nella playlist
uuid: e134cc46-5cd3-4c3c-a6ef-5ae54a2108ce
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---


# Tracce audio alternative nella playlist {#alternate-audio-tracks-in-the-playlist}

La playlist di un video può specificare un numero illimitato di tracce audio alternative per il contenuto video principale. Ad esempio, potrebbe essere utile aggiungere lingue diverse al contenuto video o consentire all&#39;utente di passare da un&#39;altra traccia del dispositivo all&#39;altra durante la riproduzione del contenuto.

Le tracce audio alternative consentono agli utenti di passare da una traccia in più lingue a quella in streaming video HTTP (dal vivo/lineare e dal VOD) e non è necessario modificare, duplicare o ricompilare il video per ciascuna traccia audio. Potete fornire tracce in più lingue per una risorsa video prima o dopo la creazione del pacchetto iniziale della risorsa.

>[!IMPORTANT]
>
>Affinché l’audio alternativo sia associato alla traccia video del supporto principale, le marche temporali della traccia alternativa devono corrispondere alle marche temporali dell’audio nella traccia principale.

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
