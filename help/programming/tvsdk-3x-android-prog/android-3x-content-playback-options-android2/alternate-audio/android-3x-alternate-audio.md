---
description: L'audio alternativo consente di passare da una traccia audio all'altra tra le tracce audio disponibili per una traccia video. Gli utenti possono selezionare la traccia della lingua preferita durante la riproduzione del video.
title: Audio alternativo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---


# Panoramica {#alternate-audio-overview}

L&#39;audio alternativo consente di passare da una traccia audio all&#39;altra tra le tracce audio disponibili per una traccia video. Gli utenti possono selezionare la traccia della lingua preferita durante la riproduzione del video.

<!--<a id="section_E4F9DC28A2944BD08B4190A7F98A8365"></a>-->

Quando TVSDK crea l’istanza `MediaPlayerItem` per il video corrente, crea un elemento `AudioTrack` per ogni traccia audio disponibile. L&#39;elemento contiene una proprietà `name` , che è una stringa che in genere contiene una descrizione riconoscibile dall&#39;utente della lingua del brano. L&#39;elemento contiene inoltre informazioni sull&#39;utilizzo predefinito del brano. Quando è il momento di riprodurre il video, è possibile chiedere un elenco di tracce audio disponibili, facoltativamente consentire all&#39;utente di selezionare una traccia e impostare il video da riprodurre con la traccia selezionata.

>[!TIP]
>
>Anche se raramente, se dopo la creazione della `MediaPlayerItem` da parte di TVSDK è disponibile una traccia audio aggiuntiva, TVSDK genera un evento `MediaPlayerItem.AUDIO_TRACK_UPDATED` .

## API aggiunte {#section_87C42C30BA8C4F58A2DAB7CE07FCD3DE}

Per supportare l’audio alternativo sono state aggiunte le seguenti API:

**`hasAlternateAudio`**

Se il supporto specificato dispone di una traccia audio alternativa, diversa dalla traccia predefinita, questa funzione booleana restituisce `true`. Se non è presente alcuna traccia audio alternativa, la funzione restituisce `false`.

```java
boolean hasAlternateAudio();
```

**`getAudioTracks`**

Questa funzione restituisce l&#39;elenco di tutte le tracce audio attualmente disponibili in un supporto specificato.

```java
List<AudioTrack> getAudioTracks();
```

**`getSelectedAudioTrack`**

Questa funzione restituisce la traccia audio alternativa attualmente selezionata e proprietà quali la lingua. È inoltre possibile estrarre la selezione automatica del brano.

```java
AudioTrack getSelectedAudioTrack();
```

**`selectAudioTrack`**

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
