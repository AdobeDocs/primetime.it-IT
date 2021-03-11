---
description: Creare un'istanza di MediaPlayer e inserirne una visualizzazione in un layout di frame.
title: Configurare MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---


# Configurare MediaPlayer {#set-up-the-mediaplayer}

TVSDK fornisce gli strumenti per creare un’applicazione di lettore video avanzata (il lettore Primetime) che è possibile integrare con altri componenti Primetime. Offre inoltre una serie di funzioni progettate per massimizzare la qualità di riproduzione video.

Creare un&#39;istanza di MediaPlayer e inserirne una visualizzazione in un layout di frame.

1. Creare un&#39;istanza `MediaPlayer` passando un oggetto `android.content.Context` al costruttore:

   ```java
   MediaPlayer mediaPlayer = new MediaPlayer(context);
   ```

1. Fornire un layout di fotogramma ( `android.widget.FrameLayout`) per contenere un `ViewGroup` di `mediaPlayer`:

   ```java
   FrameLayout playerFrame = (FrameLayout) _viewGroup.findViewById(R.id.playerFrame);
   ```

   Di seguito è riportato il frammento di codice da creare `_viewGroup`.

   ```
   @Override 
    public ViewGroup onCreateView(LayoutInflater inflater, ViewGroup container, 
      Bundle savedInstanceState) { 
     _viewGroup = (ViewGroup) inflater.inflate( 
       R.layout.fragment_player, container, false); 
     return _viewGroup; 
    }
   ```

1. Posizionate una vista di `mediaPlayer` all&#39;interno del layout del fotogramma:

   ```java
   playerFrame.addView(mediaPlayer.getView());
   ```

>L’istanza `MediaPlayer` ( `mediaPlayer`) è ora disponibile e configurata correttamente per visualizzare il contenuto video sullo schermo del dispositivo.