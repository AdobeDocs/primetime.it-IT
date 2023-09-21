---
description: È possibile impostare il formato, ad esempio il tipo di carattere, la dimensione, il colore, il bordo e l'opacità del testo con sottotitoli.
title: Imposta stili sottotitoli codificati
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# Imposta stili sottotitoli codificati{#set-closed-caption-styles}

È possibile impostare il formato, ad esempio il tipo di carattere, la dimensione, il colore, il bordo e l&#39;opacità del testo con sottotitoli.

1. Attendi `MediaPlayer` essere almeno nello stato PREPARATO.

   Per ulteriori informazioni sugli stati, consulta [Attesa di uno stato valido](../../../content-playback-options-browser-tvsdk/ui-configure/t-psdk-browser-tvsdk-2.4-ui-state-prepared-wait-for.md).
1. Creare un `TextFormat` dell&#39;istanza.

   Potete specificare tutti i parametri di stile dei sottotitoli o impostarli in un secondo momento.

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

1. (Facoltativo) Ottieni le impostazioni correnti dello stile sottotitoli con `MediaPlayer.ccStyle`.

   Il valore restituito è un&#39;istanza del `TextFormat` di rete.

   Se in precedenza non è stato impostato alcuno stile, viene restituito un oggetto TextFormat con valori predefiniti per ogni attributo:

   ```js
   ccStyle :AdobePSDK.TextFormat
   ```

1. Per modificare le impostazioni di stile, utilizzare `MediaPlayer.ccStyle`, passaggio di un&#39;istanza di `TextFormat` di rete.

   Puoi utilizzare questo metodo anche se il flusso multimediale corrente non contiene sottotitoli.

   ```js
   ccStyle :AdobePSDK.TextFormat 
   ```

   >[!TIP]
   >
   >L&#39;impostazione dello stile dei sottotitoli è asincrona e la visualizzazione delle modifiche sullo schermo potrebbe richiedere alcuni secondi.
