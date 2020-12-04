---
description: L'audio alternativo consente di passare tra le tracce audio disponibili per una traccia video. Gli utenti possono selezionare la traccia della lingua preferita al momento della riproduzione del video.
seo-description: L'audio alternativo consente di passare tra le tracce audio disponibili per una traccia video. Gli utenti possono selezionare la traccia della lingua preferita al momento della riproduzione del video.
seo-title: Audio alternativo
title: Audio alternativo
uuid: d1af1ea9-2516-4835-baff-3577ad5b705e
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---


# Panoramica {#alternate-audio-overview}

L&#39;audio alternativo consente di passare tra le tracce audio disponibili per una traccia video. Gli utenti possono selezionare la traccia della lingua preferita al momento della riproduzione del video.

<!--<a id="section_E4F9DC28A2944BD08B4190A7F98A8365"></a>-->

Quando TVSDK crea l&#39;istanza `MediaPlayerItem` per il video corrente, crea un elemento `AudioTrack` per ogni traccia audio disponibile. L&#39;elemento contiene una proprietà `name`, ovvero una stringa che in genere contiene una descrizione riconoscibile dall&#39;utente della lingua della traccia. L&#39;elemento contiene anche informazioni sull&#39;utilizzo di tale traccia per impostazione predefinita. Quando è il momento di riprodurre il video, potete richiedere un elenco delle tracce audio disponibili, eventualmente consentire all’utente di selezionare una traccia e impostare il video in modo che venga riprodotto con la traccia selezionata.

>[!TIP]
>
>Anche se raramente, se dopo la creazione di `MediaPlayerItem` da parte di TVSDK diventa disponibile una traccia audio aggiuntiva, TVSDK attiva un evento `MediaPlayerItem.AUDIO_TRACK_UPDATED`.

## API aggiunte {#section_87C42C30BA8C4F58A2DAB7CE07FCD3DE}

Sono state aggiunte le seguenti API per supportare l&#39;audio alternativo:

**`hasAlternateAudio`**

Se il supporto specificato dispone di una traccia audio alternativa, diversa dalla traccia predefinita, questa funzione booleana restituisce `true`. In assenza di tracce audio alternative, la funzione restituisce `false`.

```java
boolean hasAlternateAudio();
```

**`getAudioTracks`**

Questa funzione restituisce l&#39;elenco di tutte le tracce audio disponibili correnti in un supporto specificato.

```java
List<AudioTrack> getAudioTracks();
```

**`getSelectedAudioTrack`**

Questa funzione restituisce la traccia audio alternativa correntemente selezionata e proprietà quali la lingua. È inoltre possibile estrarre la selezione automatica del brano.

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
