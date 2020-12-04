---
description: Potete impostare il formato, ad esempio font, dimensioni, colore, bordo e opacità per il testo delle didascalie.
seo-description: Potete impostare il formato, ad esempio font, dimensioni, colore, bordo e opacità per il testo delle didascalie.
seo-title: Impostare gli stili di didascalia
title: Impostare gli stili di didascalia
uuid: 906ed22c-e673-4211-a14b-d95d176aad21
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---


# Imposta stili di sottotitoli codificati{#set-closed-caption-styles}

Potete impostare il formato, ad esempio font, dimensioni, colore, bordo e opacità per il testo delle didascalie.

1. Attendere che `MediaPlayer` sia almeno nello stato PREPARATO.

   Per ulteriori informazioni sugli stati, vedere [Attendere uno stato valido](../../../content-playback-options-browser-tvsdk/ui-configure/t-psdk-browser-tvsdk-2.4-ui-state-prepared-wait-for.md).
1. Create un&#39;istanza `TextFormat`.

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

   Il valore restituito è un&#39;istanza dell&#39;interfaccia `TextFormat`.

   Se non è stato precedentemente impostato alcuno stile, restituisce un oggetto TextFormat con valori predefiniti per ciascun attributo:

   ```js
   ccStyle :AdobePSDK.TextFormat
   ```

1. Per modificare le impostazioni di stile, utilizzare `MediaPlayer.ccStyle`, passando un&#39;istanza dell&#39;interfaccia `TextFormat`.

   È possibile utilizzare questo metodo anche se il flusso multimediale corrente non contiene didascalie.

   ```js
   ccStyle :AdobePSDK.TextFormat 
   ```

   >[!TIP]
   >
   >L&#39;impostazione dello stile dei sottotitoli codificati è asincrona, pertanto la visualizzazione delle modifiche potrebbe richiedere alcuni secondi.

