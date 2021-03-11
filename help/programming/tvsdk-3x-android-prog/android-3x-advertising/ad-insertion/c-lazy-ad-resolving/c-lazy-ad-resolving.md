---
description: La risoluzione degli annunci e il caricamento degli annunci possono causare un ritardo inaccettabile per un utente in attesa dell'avvio della riproduzione. Le funzioni Lazy Ad Loading e Lazy Ad Resolving possono ridurre questo ritardo di avvio. Lazy Ad Resolving è cambiato significativamente nella versione 3.0. Nel caricamento di annunci Lazy prima della versione 3.0, la risoluzione degli annunci è stata suddivisa in due passaggi, risolvendo solo gli annunci pre-roll prima dello stato PREPARED, e i giri medi e i post-roll dopo lo stato PREPARED. Questo è cambiato e le interruzioni pubblicitarie vengono ora risolte a un intervallo specificato prima della posizione dell’interruzione pubblicitaria.
keywords: Pigro;risoluzione annunci;Caricamento annunci
title: Risoluzione tempestiva degli annunci
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 0%

---


# Panoramica {#just-in-time-ad-resolving-overview}

La risoluzione degli annunci e il caricamento degli annunci possono causare un ritardo inaccettabile per un utente in attesa dell&#39;avvio della riproduzione. Le funzioni Lazy Ad Loading e Lazy Ad Resolving possono ridurre questo ritardo di avvio. Lazy Ad Resolving è cambiato significativamente nella versione 3.0. Nel caricamento di annunci Lazy prima della versione 3.0, la risoluzione degli annunci è stata suddivisa in due passaggi, risolvendo solo gli annunci pre-roll prima dello stato PREPARED, e i giri medi e i post-roll dopo lo stato PREPARED. Questo è cambiato e le interruzioni pubblicitarie vengono ora risolte a un intervallo specificato prima della posizione dell’interruzione pubblicitaria.

* Processo di risoluzione e caricamento degli annunci di base:

   1. TVSDK scarica un manifesto (playlist) e *risolve* tutti gli annunci.
   1. TVSDK *carica* tutti gli annunci e li inserisce nella timeline.
   1. TVSDK sposta il lettore nello stato PREPARATO e inizia la riproduzione del contenuto.

   Il lettore utilizza gli URL nel manifesto per ottenere il contenuto dell’annuncio (creativi), assicura che il contenuto dell’annuncio sia in un formato che TVSDK può riprodurre e TVSDK inserisce gli annunci nella timeline. Questo processo di base di risoluzione e caricamento degli annunci può causare un ritardo inaccettabilmente lungo per un utente che aspetta di riprodurre il proprio contenuto, soprattutto se il manifesto contiene diversi URL di annunci.

* *Caricamento* annuncio pigro:

   1. TVSDK scarica una playlist e *risolve* tutti gli annunci.
   1. TVSDK *carica* annunci pre-scorrimento, sposta il lettore nello stato PREPARATO e inizia la riproduzione del contenuto.
   1. TVSDK *carica* gli annunci rimanenti e li inserisce sulla timeline mentre si verifica la riproduzione.

   Questa funzione migliora il processo di base inserendo il lettore nello stato PREPARATO prima che tutti gli annunci vengano caricati.

* *Risoluzione* annunci pigri:

   1. TVSDK scarica la playlist.
   1. TVSDK risolve e carica tutti gli annunci pre-roll, sposta il lettore nello stato PREPARATO e inizia la riproduzione del contenuto.
   1. TVSDK risolve e ogni annuncio rimanente si interrompe singolarmente in base al seguente calcolo:

      `AdvertisingMetadata::getDelayAdLoadingTolerance() + PlayBufferTime::playBufferTime + the value defined in EXT-X-TARGETDURATION`

      Per impostazione predefinita, per contenuti con una durata di Target di 6 secondi, saranno 5,0 + 30,0 + 6,0 secondi (41 secondi)

   1. Se un’interruzione pubblicitaria si verifica entro 10 secondi dalla posizione iniziale, verrà risolta insieme agli annunci pre-scorrimento prima dello stato PREPARATO.

>[!IMPORTANT]
>
>**Fattori da considerare con Lazy Ad Resolving:**
>
>* Lazy Ad Resolving è supportato solo per i flussi VOD solo con le modalità SERVER_MAP e MANIFEST_CUES.
>* La risoluzione degli annunci pigri non è abilitata per impostazione predefinita. Se disabilitata, tutti gli annunci vengono risolti sui flussi VOD prima dell&#39;avvio della riproduzione.
>* La risoluzione degli annunci pigri non è compatibile con la funzione Instant On. Per ulteriori informazioni su Instant On, consulta Instant On.
>* Con Lazy Ad Resolving, mentre cerca di andare avanti durante una pausa pubblicitaria, la pausa pubblicitaria più vicina alla posizione di ricerca sarà risolta durante la ricerca.
>* Con Lazy Ad Resolving, se più interruzioni pubblicitarie esistono contemporaneamente (VMAP), saranno risolte allo stesso tempo.
>* Si sconsiglia di ridurre il valore di *setDelayAdLoadingTolerance() *al di sotto del valore predefinito (5 secondi). In questo modo il lettore potrebbe creare un &quot;buffer&quot; inutilmente.
>* Lazy Ad Resolving non influenza gli annunci pre-roll.
>* La risoluzione degli annunci pigri è attualmente supportata con il plugin Auditude-Plugin. Si consiglia di non impostare *setDelayAdLoading* su true se si utilizza un resolver personalizzato.

>


