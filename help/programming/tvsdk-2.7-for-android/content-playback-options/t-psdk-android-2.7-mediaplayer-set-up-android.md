---
description: Creare un'istanza di MediaPlayer e inserire una visualizzazione in un layout di frame.
title: Configurare MediaPlayer
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# Configurare MediaPlayer {#set-up-the-mediaplayer}

TVSDK fornisce gli strumenti per creare un’applicazione video player avanzata (il lettore Primetime) che puoi integrare con altri componenti di Primetime. Offre inoltre una serie di funzioni progettate per ottimizzare la qualità della riproduzione video.

Creare un&#39;istanza di MediaPlayer e inserire una visualizzazione in un layout di frame.

1. Crea istanza `MediaPlayer`, passaggio di un `android.content.Context` oggetto al costruttore:

   ```java
   MediaPlayer mediaPlayer = new MediaPlayer(context);
   ```

1. Fornire un layout di frame ( `android.widget.FrameLayout`) per contenere una `ViewGroup` di `mediaPlayer`:

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

1. Posiziona una visualizzazione di `mediaPlayer` all&#39;interno del layout del frame:

   ```java
   playerFrame.addView(mediaPlayer.getView());
   ```

>Il `MediaPlayer` istanza ( `mediaPlayer`) è ora disponibile e configurato correttamente per visualizzare il contenuto video sullo schermo del dispositivo.
