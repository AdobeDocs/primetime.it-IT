---
description: L'audio alternativo o di associazione tardiva consente di passare tra le tracce audio disponibili per una traccia video. In questo modo, gli utenti possono selezionare una traccia della lingua durante la riproduzione del video.
title: Audio alternativo
exl-id: c8158888-2e2a-42a6-a948-dc6ba4ce7a9c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# Panoramica {#alternate-audio-overview}

L&#39;audio alternativo o di associazione tardiva consente di passare tra le tracce audio disponibili per una traccia video. In questo modo, gli utenti possono selezionare una traccia della lingua durante la riproduzione del video.

<!--<a id="section_E4F9DC28A2944BD08B4190A7F98A8365"></a>-->

Quando TVSDK crea `MediaPlayerItem` per il video corrente, crea un `AudioTrack` per ogni traccia audio disponibile. L&#39;elemento contiene un `name` proprietà, una stringa che in genere contiene una descrizione riconoscibile dall&#39;utente della lingua del brano. L&#39;elemento contiene inoltre informazioni sull&#39;utilizzo predefinito del brano.

Quando è il momento di riprodurre il video, è possibile richiedere un elenco delle tracce audio disponibili, consentire all&#39;utente di sceglierne una e impostare il video per la riproduzione con la traccia selezionata.

Anche se raro, se una traccia audio aggiuntiva diventa disponibile dopo la creazione del `MediaPlayerItem`, TVSDK genera un `MediaPlayerItem.AUDIO_UPDATED` evento.

## API aggiunte {#section_87C42C30BA8C4F58A2DAB7CE07FCD3DE}

Per supportare l’audio alternativo sono state aggiunte le seguenti API:

`hasAlternateAudio`

Se il supporto specificato dispone di una traccia audio alternativa, diversa da quella predefinita, questa funzione booleana restituisce `true`. Se non è presente alcuna traccia audio alternativa, la funzione restituisce `false`.

```
bool MediaPlayerItemImpl::hasAlternateAudio() const 
{ 
    return _hasAlternateAudio; 
}
```

** `getAudioTracks`**

Questa funzione restituisce l’elenco di tutte le tracce audio attualmente disponibili in un supporto specificato.

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

Questa funzione restituisce la traccia audio alternativa attualmente selezionata e proprietà come lingua. È inoltre possibile estrarre la selezione automatica del brano.

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
