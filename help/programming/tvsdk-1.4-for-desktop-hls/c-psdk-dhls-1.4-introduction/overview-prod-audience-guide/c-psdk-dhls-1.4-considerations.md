---
description: Per utilizzare TVSDK nel modo più efficace, è necessario considerare alcuni dettagli del suo funzionamento e seguire alcune best practice.
title: Considerazioni e best practice
exl-id: 5e1e09e1-f22e-4797-807a-14dbf50bb835
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# Considerazioni e best practice{#considerations-and-best-practices}

Per utilizzare TVSDK nel modo più efficace, è necessario considerare alcuni dettagli del suo funzionamento e seguire alcune best practice.

## Considerazioni {#section_tvsdk_considerations}

Quando si utilizza TVSDK, tenere presenti le seguenti informazioni:

* Adobe Primetime non funziona su emulatori o simulatori.

   Per il test è necessario utilizzare dispositivi reali.
* La riproduzione è supportata solo per contenuti HTTP Live Streaming (HLS).
* Il contenuto video principale può essere multiplexato, dove i flussi video e audio si trovano nella stessa rappresentazione, o non multiplexato, dove i flussi video e audio si trovano in rappresentazioni separate.
* L’API TVSDK è implementata in ActionScript.
* La riproduzione video richiede l&#39;Adobe del motore video (AVE). Questo influisce su come e quando è possibile accedere alle risorse multimediali:

   * I sottotitoli codificati sono supportati nella misura fornita da AVE.
   * A seconda della precisione del codificatore, la durata effettiva dei file multimediali codificati potrebbe essere diversa dalle durate registrate nel manifesto della risorsa del flusso.

      Non esiste un modo affidabile per risincronizzare tra la timeline virtuale ideale e la timeline effettiva del playout. Il tracciamento dell’avanzamento della riproduzione del flusso per la gestione degli annunci e Video Analytics deve utilizzare il tempo di riproduzione effettivo, pertanto la generazione di rapporti e il comportamento dell’interfaccia utente potrebbero non tenere traccia con precisione del contenuto multimediale e pubblicitario.
   * Al nome dell’agente utente in ingresso per tutte le richieste HTTP da TVSDK su questa piattaforma viene assegnato il seguente pattern di stringa:

      ```
      "Adobe Flash Player"
      ```

## Best practice {#section_tvsdk_best_practices}

Di seguito sono riportate le procedure consigliate per TVSDK:

* Utilizza la versione 3.0 o successiva di HLS per i contenuti del programma.
* Per TVSDK 1.4 per DHLS, il caricamento lazy degli annunci è abilitato per impostazione predefinita.

   Per i contenuti senza pre-roll o mid-roll, puoi utilizzare `AdvertisingMetadata.delayAdLoading` per accelerare ulteriormente il caricamento dei contenuti.
