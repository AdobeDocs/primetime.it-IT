---
description: Creare un'istanza di MediaPlayer e visualizzarne una visualizzazione in un layout di frame.
seo-description: Creare un'istanza di MediaPlayer e visualizzarne una visualizzazione in un layout di frame.
seo-title: Configurare MediaPlayer
title: Configurare MediaPlayer
uuid: 49c3edb9-b6e2-49f8-b4aa-f230af7de6b0
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Configurare MediaPlayer {#set-up-the-mediaplayer}

TVSDK fornisce strumenti per la creazione di un’applicazione per lettori video avanzata (il lettore Primetime), che potete integrare con altri componenti Primetime. Offre inoltre una serie di funzioni progettate per massimizzare la qualità della riproduzione video.

Creare un&#39;istanza di MediaPlayer e visualizzarne una visualizzazione in un layout di frame.

1. Creare un&#39;istanza `MediaPlayer`, passare un `android.content.Context` oggetto al costruttore:

   ```java
   MediaPlayer mediaPlayer = new MediaPlayer(context);
   ```

1. Fornite un layout di fotogramma ( `android.widget.FrameLayout`) per contenere un `ViewGroup` di `mediaPlayer`:

   ```java
   FrameLayout playerFrame = (FrameLayout) _viewGroup.findViewById(R.id.playerFrame);
   ```

   Di seguito è riportato lo snippet di codice da creare `_viewGroup`.

   ```
   @Override 
    public ViewGroup onCreateView(LayoutInflater inflater, ViewGroup container, 
      Bundle savedInstanceState) { 
     _viewGroup = (ViewGroup) inflater.inflate( 
       R.layout.fragment_player, container, false); 
     return _viewGroup; 
    }
   ```

1. Inserite una vista all’ `mediaPlayer` interno del layout della cornice:

   ```java
   playerFrame.addView(mediaPlayer.getView());
   ```

>L&#39; `MediaPlayer` istanza ( `mediaPlayer`) è ora disponibile e configurata correttamente per visualizzare il contenuto video sullo schermo del dispositivo.