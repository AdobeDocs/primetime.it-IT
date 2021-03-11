---
description: L'audio alternativo o in ritardo consente di passare da una traccia audio all'altra per una traccia video. In questo modo, gli utenti possono selezionare una traccia della lingua durante la riproduzione del video.
title: Audio alternativo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---


# Audio alternativo{#alternate-audio}

L&#39;audio alternativo o in ritardo consente di passare da una traccia audio all&#39;altra per una traccia video. In questo modo, gli utenti possono selezionare una traccia della lingua durante la riproduzione del video.

<!--<a id="section_E4F9DC28A2944BD08B4190A7F98A8365"></a>-->

Quando TVSDK crea l’istanza `MediaPlayerItem` per il video corrente, crea un elemento `AudioTrack` per ogni traccia audio disponibile. L&#39;elemento contiene una proprietà `name` , una stringa che in genere contiene una descrizione riconoscibile dall&#39;utente della lingua del brano. L&#39;elemento contiene inoltre informazioni sull&#39;utilizzo predefinito del brano.

Quando è il momento di riprodurre il video, è possibile chiedere un elenco di tracce audio disponibili, facoltativamente lasciare che l&#39;utente ne scelga una e impostare il video da riprodurre con la traccia selezionata.

Anche se raramente, se una traccia audio aggiuntiva diventa disponibile dopo la creazione di `MediaPlayerItem`, TVSDK genera un evento `MediaPlayerItem.AUDIO_UPDATED` .

## API aggiunte {#section_87C42C30BA8C4F58A2DAB7CE07FCD3DE}

Per supportare l’audio alternativo sono state aggiunte le seguenti API:

`hasAlternateAudio`

Se il supporto specificato dispone di una traccia audio alternativa, diversa dalla traccia predefinita, questa funzione booleana restituisce `true`. Se non è presente alcuna traccia audio alternativa, la funzione restituisce `false`.

```
bool MediaPlayerItemImpl::hasAlternateAudio() const { 
    return _hasAlternateAudio; 
}
```

** `getAudioTracks`*

Questa funzione restituisce l&#39;elenco di tutte le tracce audio attualmente disponibili in un supporto specificato.

```
virtual PSDKErrorCode getAudioTracks(PSDKImmutableArray<AudioTrack>*& out) const { 
    if (_audioTracks) { 
        out = _audioTracks; 
        out->addRef(); 
        return kECSuccess; 
    } 
    return kECDataNotAvailable; 
} 
```

`getSelectedAudioTrack`

Questa funzione restituisce la traccia audio alternativa attualmente selezionata e proprietà quali la lingua. È inoltre possibile estrarre la selezione automatica del brano.

```
PSDKErrorCode MediaPlayerItemImpl::getSelectedAudioTrack(AudioTrack &out) const { 
    out = _currentAudioTrack; 
    return kECSuccess; 
}
```

`selectAudioTrack`

Questa funzione seleziona una traccia audio alternativa da riprodurre.

```
PSDKErrorCode MediaPlayerItemImpl::selectAudioTrack(const AudioTrack &audioTrack) { 
    _lastPlayedAudioTrack = _currentAudioTrack; 
    if(_mediaPlayer && _mediaPlayer->_trickPlay) 
        return kECUnsupportedOperation; 
    _currentAudioTrack = audioTrack; 
    PSDKErrorCode result = kECSuccess; 
    if (_currentAudioTrack) { 
        media::TimeLine* timeline = NULL; 
        if (_mediaPlayer->_fragHttpStreamer) 
            _mediaPlayer->_fragHttpStreamer->GetTimeLine(&timeline); 
        if (timeline) { 
            for (int32_t i = timeline->GetFirstPeriodIndex(); i <= timeline->GetLastPeriodIndex(); i++){ 
                media::ErrorCode error = selectTrack(timeline,_mediaPlayer->_fragHttpStreamer, i, audioTrack.getName(), media::kSTTAudioIndex); 
                return _mediaPlayer->convertToPSDKError(error); 
            } 
        } 
    }   
    return result; 
}
```

