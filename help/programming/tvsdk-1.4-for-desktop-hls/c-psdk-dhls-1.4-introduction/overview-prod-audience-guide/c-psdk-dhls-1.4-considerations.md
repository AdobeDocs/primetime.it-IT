---
description: Per utilizzare TVSDK nel modo più efficace, è necessario prendere in considerazione alcuni dettagli del suo funzionamento e seguire alcune best practice.
seo-description: Per utilizzare TVSDK nel modo più efficace, è necessario prendere in considerazione alcuni dettagli del suo funzionamento e seguire alcune best practice.
seo-title: Considerazioni e procedure ottimali
title: Considerazioni e procedure ottimali
uuid: 62a5d641-6f37-4e4d-bbc2-414bf3681d9c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 0%

---


# Considerazioni e best practice{#considerations-and-best-practices}

Per utilizzare TVSDK nel modo più efficace, è necessario prendere in considerazione alcuni dettagli del suo funzionamento e seguire alcune best practice.

## Considerazioni {#section_tvsdk_considerations}

Ricorda le seguenti informazioni quando utilizzi TVSDK:

*  Adobe Primetime non funziona su emulatori o simulatori.

   Per eseguire il test dovete utilizzare dei dispositivi reali.
* La riproduzione è supportata solo per il contenuto HTTP Live Streaming (HLS).
* Il contenuto video principale può essere multiplexato, dove i flussi video e audio si trovano nella stessa rappresentazione, o non multiplexato, dove i flussi video e audio si trovano in rappresentazioni separate.
* L&#39;API TVSDK è implementata in  ActionScript.
* La riproduzione video richiede il motore video  Adobe (AVE). Questo incide su come e quando è possibile accedere alle risorse multimediali:

   * I sottotitoli codificati sono supportati nella misura fornita dall’AVE.
   * A seconda della precisione del codificatore, la durata effettiva del supporto codificato potrebbe essere diversa dalle durate registrate nel manifesto della risorsa di flusso.

      Non esiste un modo affidabile per risincronizzare tra la timeline virtuale ideale e la timeline di riproduzione effettiva. Il tracciamento dell’avanzamento della riproduzione del flusso per la gestione degli annunci e per l’analisi video deve utilizzare il tempo di riproduzione effettivo, pertanto il comportamento dei rapporti e dell’interfaccia utente potrebbe non tenere traccia con precisione dei contenuti multimediali e pubblicitari.
   * Al nome agente utente in arrivo per tutte le richieste HTTP da TVSDK su questa piattaforma viene assegnato il seguente pattern di stringa:

      ```
      "Adobe Flash Player"
      ```

## Best practice {#section_tvsdk_best_practices}

Seguono le procedure consigliate per TVSDK:

* Utilizzate HLS versione 3.0 o successiva per il contenuto del programma.
* Per TVSDK 1.4 per DHLS, il caricamento degli annunci pigri è abilitato per impostazione predefinita.

   Per i contenuti senza pre-roll o mid-roll, potete utilizzare `AdvertisingMetadata.delayAdLoading` per accelerare ulteriormente il caricamento dei contenuti.

