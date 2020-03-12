---
description: Questa procedura è un esempio di come creare un pulsante che consente all'utente di selezionare una traccia di sottotitoli codificati.
seo-description: Questa procedura è un esempio di come creare un pulsante che consente all'utente di selezionare una traccia di sottotitoli codificati.
seo-title: Consenti agli utenti di modificare la traccia della didascalia
title: Consenti agli utenti di modificare la traccia della didascalia
uuid: 043dc492-1dd4-4b7f-8541-d60a1d3d7c4a
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Consenti agli utenti di modificare la traccia della didascalia {#allow-users-to-change-the-caption-track}

Questa procedura è un esempio di come creare un pulsante che consente all&#39;utente di selezionare una traccia di sottotitoli codificati.

1. Creare un pulsante per modificare la traccia dei sottotitoli codificati.

   ```xml
   <Button 
     android:id="@+id/selectCC" 
     android:layout_width="wrap_content" 
     android:layout_height="wrap_content" 
     android:layout_alignParentBottom="true" 
     android:layout_alignParentRight="true" 
     android:layout_marginRight="10dp" 
     android:onClick="selectClosedCaptioningClick" 
     android:text="CC" /> 
   ```

1. Convertire l&#39;elenco delle tracce di didascalie chiuse disponibili in un array di stringhe.

   I brani dei sottotitoli codificati con attività, ovvero canali per i quali TVSDK ha rilevato dati, vengono contrassegnati di conseguenza.

   ```java
   /** 
   * Converts the closed captions tracks to a string array. 
   * 
   * @return array of CC tracks 
   */ 
   private String[] getCCsAsArray() { 
       List<String> closedCaptionsTracksAsStrings = new ArrayList<String>(); 
       MediaPlayerItem currentItem = mediaPlayer.getCurrentItem(); 
       if (currentItem != null) { 
           List<ClosedCaptionsTrack> closedCaptionsTracks = 
           currentItem.getClosedCaptionsTracks(); 
           Iterator<ClosedCaptionsTrack> iterator = closedCaptionsTracks.iterator(); 
           while (iterator.hasNext()) { 
               ClosedCaptionsTrack closedCaptionsTrack = iterator.next(); 
               String isActive = closedCaptionsTrack.isActive() ? " (" +  
                 getString(R.string.active)+ ")" : ""; 
               closedCaptionsTracksAsStrings.add(closedCaptionsTrack.getName() +  
                 isActive); 
           } 
       } 
       return closedCaptionsTracksAsStrings. 
         toArray(new String[closedCaptionsTracksAsStrings.size()]); 
   } 
   ```

1. Quando l&#39;utente fa clic sul pulsante, viene visualizzata una finestra di dialogo in cui sono elencate tutte le tracce predefinite delle didascalie.

   ```java
   public void selectClosedCaptioningClick(View view) { 
       Log.i(LOG_TAG + "#selectClosedCaptions", "Displaying closed captions chooser dialog."); 
       final String items[] = getCCsAsArray(); 
       final AlertDialog.Builder ab = new AlertDialog.Builder(this); 
       ab.setTitle(R.string.PlayerControlCCDialogTitle); 
       ab.setSingleChoiceItems(items, selectedClosedCaptionsIndex, new DialogInterface.OnClickListener() { 
           public void onClick(DialogInterface dialog, int whichButton) { 
               // Select the new closed captioning track. 
               MediaPlayerItem currentItem = mediaPlayer.getCurrentItem(); 
               ClosedCaptionsTrack desiredClosedCaptionsTrack =  
                 currentItem.getClosedCaptionsTracks().get(whichButton); 
               boolean result = currentItem.selectClosedCaptionsTrack(desiredClosedCaptionsTrack); 
               if (result) { 
                   selectedClosedCaptionsIndex = whichButton; 
               } 
               // Dismiss dialog. 
               dialog.cancel(); 
        } 
       }).setNegativeButton(R.string.PlayerControlCCDialogCancel, new DialogInterface.OnClickListener() { 
           public void onClick(DialogInterface dialog, int whichButton) { 
               // Just cancel the dialog. 
           } 
       }); 
       ab.show(); 
   } 
   ```

