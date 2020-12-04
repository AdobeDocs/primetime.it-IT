---
description: L’audio alternativo o in fase di rilegatura successiva consente di passare dalle tracce audio disponibili per una traccia video. In questo modo, gli utenti possono selezionare una traccia della lingua durante la riproduzione del video.
seo-description: L’audio alternativo o in fase di rilegatura successiva consente di passare dalle tracce audio disponibili per una traccia video. In questo modo, gli utenti possono selezionare una traccia della lingua durante la riproduzione del video.
seo-title: Audio alternativo
title: Audio alternativo
uuid: 9dc3bec6-2135-4083-8db2-50a492e6bd67
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---


# Panoramica {#alternate-audio-overview}

L’audio alternativo o in fase di rilegatura successiva consente di passare dalle tracce audio disponibili per una traccia video. In questo modo, gli utenti possono selezionare una traccia della lingua durante la riproduzione del video.

<!--<a id="section_E4F9DC28A2944BD08B4190A7F98A8365"></a>-->

Quando TVSDK crea l&#39;istanza `MediaPlayerItem` per il video corrente, crea un elemento `AudioTrack` per ogni traccia audio disponibile. L&#39;elemento contiene una proprietà `name`, una stringa che in genere contiene una descrizione riconoscibile dall&#39;utente della lingua del brano. L&#39;elemento contiene anche informazioni sull&#39;utilizzo di tale traccia per impostazione predefinita.

Quando è il momento di riprodurre il video, potete richiedere un elenco delle tracce audio disponibili, lasciare che l&#39;utente ne scelga una e impostare il video in modo che venga riprodotto con la traccia selezionata.

Anche se raramente, se dopo la creazione della `MediaPlayerItem` diventa disponibile una traccia audio aggiuntiva, TVSDK attiva un evento `MediaPlayerItem.AUDIO_UPDATED`.

## API aggiunte {#section_87C42C30BA8C4F58A2DAB7CE07FCD3DE}

Sono state aggiunte le seguenti API per supportare l&#39;audio alternativo:

`hasAlternateAudio`

Se il supporto specificato dispone di una traccia audio alternativa, diversa dalla traccia predefinita, questa funzione booleana restituisce `true`. In assenza di tracce audio alternative, la funzione restituisce `false`.

```
bool MediaPlayerItemImpl::hasAlternateAudio() const 
{ 
    return _hasAlternateAudio; 
}
```

** `getAudioTracks`*

Questa funzione restituisce l&#39;elenco di tutte le tracce audio disponibili correnti in un supporto specificato.

```
virtual PSDKErrorCode getAudioTracks(PSDKImmutableArray<AudioTrack>*& out) const 
    { 
        if (_audioTracks) 
        { 
            out = _audioTracks; 
            out->addRef(); 
            return kECSuccess; 
        } 
        return kECDataNotAvailable; 
    }
```

`getSelectedAudioTrack`

Questa funzione restituisce la traccia audio alternativa correntemente selezionata e proprietà quali la lingua. È inoltre possibile estrarre la selezione automatica del brano.

```
PSDKErrorCode MediaPlayerItemImpl::getSelectedAudioTrack(AudioTrack &out) const 
{ 
    out = _currentAudioTrack; 
    return kECSuccess; 
}
```

`selectAudioTrack`

Questa funzione seleziona una traccia audio alternativa da riprodurre.

```
PSDKErrorCode MediaPlayerItemImpl::selectAudioTrack(const AudioTrack &audioTrack) 
{ 
    _lastPlayedAudioTrack = _currentAudioTrack; 
    if(_mediaPlayer && _mediaPlayer->_trickPlay) 
        return kECUnsupportedOperation; 
    _currentAudioTrack = audioTrack; 
    PSDKErrorCode result = kECSuccess; 
    if (_currentAudioTrack) 
    { 
        media::TimeLine* timeline = NULL; 
        if (_mediaPlayer->_fragHttpStreamer) 
            _mediaPlayer->_fragHttpStreamer->GetTimeLine(&timeline); 
        if (timeline) 
        { 
            for (int32_t i = timeline->GetFirstPeriodIndex(); i <= timeline->GetLastPeriodIndex(); i++){ 
                media::ErrorCode error = selectTrack(timeline,_mediaPlayer->_fragHttpStreamer, i, audioTrack.getName(), media::kSTTAudioIndex); 
                return _mediaPlayer->convertToPSDKError(error); 
            } 
        } 
    }   
    return result; 
}
```

