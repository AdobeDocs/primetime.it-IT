---
description: TVSDK fornisce strumenti per la creazione di un’applicazione per lettori video avanzata (il lettore Primetime), che potete integrare con altri componenti Primetime. Offre inoltre una serie di funzioni progettate per massimizzare la qualità della riproduzione video.
seo-description: TVSDK fornisce strumenti per la creazione di un’applicazione per lettori video avanzata (il lettore Primetime), che potete integrare con altri componenti Primetime. Offre inoltre una serie di funzioni progettate per massimizzare la qualità della riproduzione video.
seo-title: Configurare il lettore multimediale
title: Configurare il lettore multimediale
uuid: 1f672484-b340-4f92-8a47-dad4c9f3b3fc
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---


# Impostare il lettore multimediale {#set-up-the-media-player}

TVSDK fornisce strumenti per la creazione di un’applicazione per lettori video avanzata (il lettore Primetime), che potete integrare con altri componenti Primetime. Offre inoltre una serie di funzioni progettate per massimizzare la qualità della riproduzione video.

<!--<a id="section_1FE83A68DE624F20B52C0959851F5699"></a>-->

Create un&#39;istanza di `MediaPlayer` e inserite una visualizzazione in un layout di frame.

1. Creare un&#39;istanza `MediaPlayer`, passando un oggetto `android.content.Context` al costruttore:

   ```java
   MediaPlayer mediaPlayer = new MediaPlayer(context);
   ```

1. Fornire un layout di fotogramma ( `android.widget.FrameLayout`) per contenere una `ViewGroup` di `mediaPlayer`:

   ```java
   FrameLayout playerFrame = (FrameLayout) _viewGroup.findViewById(R.id.playerFrame);
   ```

   >[!NOTE]
   >
   >Di seguito è riportato lo snippet di codice da creare `_viewGroup`.

   ```
   @Override 
    public ViewGroup onCreateView(LayoutInflater inflater, ViewGroup container, 
      Bundle savedInstanceState) { 
     _viewGroup = (ViewGroup) inflater.inflate( 
       R.layout.fragment_player, container, false); 
     return _viewGroup; 
    }
   ```

1. Inserite una vista di `mediaPlayer` all&#39;interno del layout del frame:

   ```java
   playerFrame.addView(mediaPlayer.getView());
   ```

   >[!NOTE]
   >
   >L&#39;istanza `MediaPlayer` ( `mediaPlayer`) è ora disponibile e configurata correttamente per visualizzare il contenuto video sullo schermo del dispositivo.