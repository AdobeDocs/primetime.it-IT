---
description: È possibile impostare il formato, ad esempio font, dimensioni, colore, bordo e opacità per il testo a didascalia chiusa.
title: Impostare gli stili per sottotitoli
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---


# Imposta stili di sottotitoli{#set-closed-caption-styles}

È possibile impostare il formato, ad esempio font, dimensioni, colore, bordo e opacità per il testo a didascalia chiusa.

1. Attendi che lo stato `MediaPlayer` sia almeno PREPARATO.

   Per ulteriori informazioni sugli stati, vedere [Attendi uno stato valido](../../../content-playback-options-browser-tvsdk/ui-configure/t-psdk-browser-tvsdk-2.4-ui-state-prepared-wait-for.md).
1. Crea un&#39;istanza `TextFormat`.

   Ora puoi fornire tutti i parametri di stile dei sottotitoli o impostarli in un secondo momento.

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

1. (Facoltativo) Ottenere le impostazioni correnti dello stile dei sottotitoli con `MediaPlayer.ccStyle`.

   Il valore restituito è un&#39;istanza dell&#39;interfaccia `TextFormat`.

   Se non è stato precedentemente impostato alcuno stile, restituisce un oggetto TextFormat con valori predefiniti per ogni attributo:

   ```js
   ccStyle :AdobePSDK.TextFormat
   ```

1. Per modificare le impostazioni dello stile, utilizzare `MediaPlayer.ccStyle`, passando un&#39;istanza dell&#39;interfaccia `TextFormat`.

   È possibile utilizzare questo metodo anche se il flusso multimediale corrente non dispone di sottotitoli codificati.

   ```js
   ccStyle :AdobePSDK.TextFormat 
   ```

   >[!TIP]
   >
   >L’impostazione dello stile dei sottotitoli non codificati è asincrona, pertanto potrebbero essere necessari alcuni secondi affinché le modifiche vengano visualizzate sullo schermo.

