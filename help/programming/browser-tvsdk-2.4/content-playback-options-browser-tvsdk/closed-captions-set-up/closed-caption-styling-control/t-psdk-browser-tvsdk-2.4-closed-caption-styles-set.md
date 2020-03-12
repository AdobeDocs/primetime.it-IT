---
description: Potete impostare il formato, ad esempio font, dimensioni, colore, bordo e opacità per il testo delle didascalie.
seo-description: Potete impostare il formato, ad esempio font, dimensioni, colore, bordo e opacità per il testo delle didascalie.
seo-title: Impostare gli stili di didascalia
title: Impostare gli stili di didascalia
uuid: 906ed22c-e673-4211-a14b-d95d176aad21
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Impostare gli stili di didascalia{#set-closed-caption-styles}

Potete impostare il formato, ad esempio font, dimensioni, colore, bordo e opacità per il testo delle didascalie.

1. Attendete che lo stato `MediaPlayer` sia almeno PREPARATO.

   Per ulteriori informazioni sugli stati, vedere [Attendere uno stato](../../../content-playback-options-browser-tvsdk/ui-configure/t-psdk-browser-tvsdk-2.4-ui-state-prepared-wait-for.md)valido.
1. Create un&#39; `TextFormat` istanza.

   Potete fornire ora tutti i parametri di stile per i sottotitoli codificati o impostarli successivamente.

   ```js
   new TextFormat( 
       font,   
       fontColor,  
       edgeColor,   
       fontEdge,  
       backgroundColor,   
       fillColor,  
       size,   
       fontOpacity,   
       backgroundOpacity,  
       fillOpacity, 
       bottomInset 
       safeArea) → {AdobePSDK.TextFormat}
   ```

1. (Facoltativo) Ottenete le impostazioni di stile correnti per i sottotitoli codificati con `MediaPlayer.ccStyle`.

   Il valore restituito è un&#39;istanza dell&#39; `TextFormat` interfaccia.

   Se non è stato precedentemente impostato alcuno stile, restituisce un oggetto TextFormat con valori predefiniti per ciascun attributo:

   ```js
   ccStyle :AdobePSDK.TextFormat
   ```

1. Per modificare le impostazioni di stile, utilizzare `MediaPlayer.ccStyle`, passando un&#39;istanza dell&#39; `TextFormat` interfaccia.

   È possibile utilizzare questo metodo anche se il flusso multimediale corrente non contiene didascalie.

   ```js
   ccStyle :AdobePSDK.TextFormat 
   ```

   >[!TIP]
   >
   >L&#39;impostazione dello stile dei sottotitoli codificati è asincrona, pertanto la visualizzazione delle modifiche potrebbe richiedere alcuni secondi.

