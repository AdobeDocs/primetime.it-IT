---
description: Per utilizzare TVSDK nel modo più efficace, è necessario considerare alcuni dettagli del suo funzionamento e seguire alcune best practice.
title: Considerazioni e best practice
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# Considerazioni e best practice{#considerations-and-best-practices}

Per utilizzare TVSDK nel modo più efficace, è necessario considerare alcuni dettagli del suo funzionamento e seguire alcune best practice.

## Considerazioni {#section_tvsdk_considerations}

Quando si utilizza TVSDK, tenere presenti le seguenti informazioni:

* Adobe Primetime non funziona sui simulatori iOS.

  Per il test è necessario utilizzare dispositivi reali.
* La riproduzione è supportata solo per contenuti HTTP Live Streaming (HLS).
* Il contenuto video principale può essere multiplexato, dove i flussi video e audio si trovano nella stessa rappresentazione, o non multiplexato, dove i flussi video e audio si trovano in rappresentazioni separate.
* L’API TVSDK è implementata in Objective-C.
* La riproduzione video richiede il framework Apple AV Foundation nativo. Questo influisce su come e quando è possibile accedere alle risorse multimediali, inclusi i sottotitoli codificati e le timeline:

   * Le regolazioni della sequenza temporale non possono essere riviste dopo la configurazione iniziale.

     Ad esempio, un annuncio pubblicitario non può essere rimosso dalla timeline dopo che è stato riprodotto. Se l’utente cerca nuovamente nella presentazione, lo stesso annuncio viene riprodotto anche se la policy prevede la rimozione dell’annuncio.
   * A seconda della precisione del codificatore, la durata effettiva dei file multimediali codificati potrebbe essere diversa dalle durate registrate nel manifesto della risorsa del flusso.

     Non esiste un modo affidabile per risincronizzare tra la timeline virtuale ideale e la timeline effettiva del playout. Il tracciamento dell’avanzamento della riproduzione del flusso per la gestione degli annunci e Video Analytics deve utilizzare il tempo di riproduzione effettivo, pertanto la generazione di rapporti e il comportamento dell’interfaccia utente potrebbero non tenere traccia con precisione del contenuto multimediale e pubblicitario.
   * L’agente utente in ingresso per tutte le richieste HTTP da TVSDK su questa piattaforma è determinato dal dispositivo e dalla versione di iOS in esecuzione sul dispositivo.

     Il valore della stringa dell’agente utente viene impostato automaticamente su ciò che il sistema operativo assegna.

## Best practice {#section_tvsdk_best_practices}

Di seguito sono riportate le procedure consigliate per TVSDK:

* Utilizza la versione 3.0 o successiva di HLS per i contenuti del programma.
* Utilizza lo strumento mediastreamvalidator di Apple per convalidare i flussi VOD.
* Il `PTSDKConfig` La classe fornisce metodi per applicare SSL alle richieste effettuate ai server Primetime Ad Decisioning, DRM e Video Analytics.

  Per ulteriori informazioni, vedere `forceHTTPS` e `isForcingHTTPS` metodi in questa classe.

  >[!IMPORTANT]
  >
  >Le richieste a domini di terze parti come pixel di tracciamento degli annunci, URL di contenuti e annunci e richieste simili non vengono modificate. È responsabilità dei provider di contenuti e dei server di annunci fornire URL supportati tramite HTTPS.
