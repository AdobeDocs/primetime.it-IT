---
description: L'audio alternativo consente di alternare le tracce audio disponibili per una traccia video. Gli utenti possono selezionare la traccia nella lingua preferita durante la riproduzione del video.
title: Audio alternativo
exl-id: c2eb10dc-3fe0-472b-8450-2fbfc6b09487
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---

# Panoramica {#alternate-audio-overview}

L&#39;audio alternativo consente di alternare le tracce audio disponibili per una traccia video. Gli utenti possono selezionare la traccia nella lingua preferita durante la riproduzione del video.

<!--<a id="section_E4F9DC28A2944BD08B4190A7F98A8365"></a>-->

Quando TVSDK crea `MediaPlayerItem` per il video corrente, crea un `AudioTrack` per ogni traccia audio disponibile. L&#39;elemento contiene un `name` proprietà, una stringa che in genere contiene una descrizione riconoscibile dall&#39;utente della lingua di tale brano. L&#39;elemento contiene inoltre informazioni sull&#39;utilizzo predefinito del brano. Quando è il momento di riprodurre il video, è possibile richiedere un elenco delle tracce audio disponibili, consentire facoltativamente all&#39;utente di selezionare una traccia e impostare il video per la riproduzione con la traccia selezionata.

>[!TIP]
>
>Sebbene raro, se dopo la creazione di TVSDK diventa disponibile una traccia audio aggiuntiva, `MediaPlayerItem`, TVSDK genera un `MediaPlayerItem.AUDIO_TRACK_UPDATED` evento.

## API aggiunte {#section_87C42C30BA8C4F58A2DAB7CE07FCD3DE}

Per supportare l’audio alternativo sono state aggiunte le seguenti API:

`hasAlternateAudio`

Se il supporto specificato dispone di una traccia audio alternativa, diversa da quella predefinita, questa funzione booleana restituisce `true`. Se non è presente alcuna traccia audio alternativa, la funzione restituisce `false`.

```java
boolean hasAlternateAudio();
```

** `getAudioTracks`**

Questa funzione restituisce l’elenco di tutte le tracce audio attualmente disponibili in un supporto specificato.

```java
List<AudioTrack> getAudioTracks();
```

`getSelectedAudioTrack`

Questa funzione restituisce la traccia audio alternativa attualmente selezionata e proprietà come lingua. È inoltre possibile estrarre la selezione automatica del brano.

```java
AudioTrack getSelectedAudioTrack();
```

`selectAudioTrack`

Questa funzione seleziona una traccia audio alternativa da riprodurre.

```java
void selectAudioTrack(AudioTrack audioTrack);
```

Ad esempio:

```java
private void onPrepared() { 
    // Select the AA track in PREPARED State 
    boolean hasAlternateAudio = _mediaPlayer.getCurrentItem().hasAlternateAudio(); 
    if(hasAlternateAudio) { 
        AudioTrack selectedAudioTrack =  
          _mediaPlayer.getCurrentItem().getSelectedAudioTrack(); 
 
        if (selectedAudioTrack == null) {  
            // Selecting default audio track  
            // If index is 1 it will select alternate audio track  
            selectedAudioTrack = _mediaPlayer.getCurrentItem().getAudioTracks().get(0);  
        } 
    } 
    _mediaPlayer.getCurrentItem().selectAudioTrack(selectedAudioTrack); 
} 
```
