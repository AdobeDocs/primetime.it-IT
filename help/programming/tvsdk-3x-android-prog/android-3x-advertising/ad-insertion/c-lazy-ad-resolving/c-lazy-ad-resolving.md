---
description: La risoluzione degli annunci e il caricamento degli annunci potrebbero causare un ritardo inaccettabile per l'utente in attesa dell'avvio della riproduzione. Le funzioni Lazy Ad Loading e Lazy Ad Resolving possono ridurre questo ritardo di avvio. Lazy Ad Resolving è cambiato notevolmente nella versione 3.0. Nel caricamento di Lazy Ad prima della versione 3.0, la risoluzione degli annunci è stata suddivisa in due passaggi, risolvendo solo gli annunci pre-roll prima dello stato PREPARATO, e i mid-roll e post-roll dopo lo stato PREPARATO. Questo è cambiato e le interruzioni di annuncio ora vengono risolte a un intervallo specificato prima della posizione dell'interruzione di annuncio.
keywords: Lazy;Ad resolving;Ad loading
seo-description: La risoluzione degli annunci e il caricamento degli annunci potrebbero causare un ritardo inaccettabile per l'utente in attesa dell'avvio della riproduzione. Le funzioni Lazy Ad Loading e Lazy Ad Resolving possono ridurre questo ritardo di avvio. Lazy Ad Resolving è cambiato notevolmente nella versione 3.0. Nel caricamento di Lazy Ad prima della versione 3.0, la risoluzione degli annunci è stata suddivisa in due passaggi, risolvendo solo gli annunci pre-roll prima dello stato PREPARATO, e i mid-roll e post-roll dopo lo stato PREPARATO. Questo è cambiato e le interruzioni di annuncio ora vengono risolte a un intervallo specificato prima della posizione dell'interruzione di annuncio.
seo-title: Risoluzione degli annunci nel tempo
title: Risoluzione degli annunci nel tempo
uuid: 77028f6e-7e53-45d1-bcc0-54f8224d6d18
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Panoramica {#just-in-time-ad-resolving-overview}

La risoluzione degli annunci e il caricamento degli annunci potrebbero causare un ritardo inaccettabile per l&#39;utente in attesa dell&#39;avvio della riproduzione. Le funzioni Lazy Ad Loading e Lazy Ad Resolving possono ridurre questo ritardo di avvio. Lazy Ad Resolving è cambiato notevolmente nella versione 3.0. Nel caricamento di Lazy Ad prima della versione 3.0, la risoluzione degli annunci è stata suddivisa in due passaggi, risolvendo solo gli annunci pre-roll prima dello stato PREPARATO, e i mid-roll e post-roll dopo lo stato PREPARATO. Questo è cambiato e le interruzioni di annuncio ora vengono risolte a un intervallo specificato prima della posizione dell&#39;interruzione di annuncio.

* Processo di base per la risoluzione e il caricamento degli annunci:

   1. TVSDK scarica un manifesto (playlist) e *risolve* tutti gli annunci.
   1. TVSDK *carica* tutti gli annunci e li inserisce nella timeline.
   1. TVSDK sposta il lettore nello stato PREPARATO e inizia la riproduzione del contenuto.
   Il lettore utilizza gli URL nel manifesto per ottenere il contenuto dell’annuncio (creativi), assicura che il contenuto dell’annuncio sia in un formato che possa essere riprodotto da TVSDK e che TVSDK inserisca gli annunci nella timeline. Questo processo di base per la risoluzione e il caricamento degli annunci può causare un ritardo inaccettabilmente lungo per un utente che attende di riprodurre il proprio contenuto, soprattutto se il manifesto contiene diversi URL di annunci.

* *Caricamento* annuncio non aggiornato:

   1. TVSDK scarica una playlist e *risolve* tutti gli annunci.
   1. TVSDK *carica* annunci pre-roll, sposta il lettore nello stato PREPARATO e inizia la riproduzione del contenuto.
   1. TVSDK *carica* gli annunci rimanenti e li inserisce nella timeline durante la riproduzione.
   Questa funzione migliora il processo di base mettendo il lettore nello stato PREPARATO prima che tutti gli annunci vengano caricati.

* *Lazy Ad Resolving*:

   1. TVSDK scarica la playlist.
   1. TVSDK risolve e carica eventuali annunci pre-roll, sposta il lettore nello stato PREPARATO e inizia la riproduzione del contenuto.
   1. Le risoluzioni TVSDK e ciascuna delle interruzioni pubblicitarie rimanenti singolarmente si basano sul seguente calcolo:

      `AdvertisingMetadata::getDelayAdLoadingTolerance() + PlayBufferTime::playBufferTime + the value defined in EXT-X-TARGETDURATION`

      Per impostazione predefinita, per il contenuto con una durata Target di 6 secondi, questo sarà di 5,0 + 30,0 + 6,0 secondi (41 secondi)

   1. Se un&#39;interruzione annuncio si verifica entro 10 secondi dalla posizione iniziale, verrà risolta insieme agli annunci pre-roll prima dello stato PREPARATO.

>[!IMPORTANT]
>
>**Fattori da considerare con Lazy Ad Resolving:** >
>* Lazy Ad Resolving è supportato solo per i flussi VOD solo con le modalità SERVER_MAP e MANIFEST_CUES.
>* La risoluzione annuncio non è abilitata per impostazione predefinita. Se disabilitato, tutti gli annunci vengono risolti sui flussi VOD prima dell&#39;avvio della riproduzione.
>* Lazy Ad Resolving è incompatibile con la funzione Instant On. Per ulteriori informazioni su Attivato istantaneo, consultate Attivato istantaneo.
>* Con Lazy Ad Resolving, mentre si cerca avanti per un&#39;interruzione annuncio, l&#39;interruzione annuncio più vicina alla posizione di ricerca verrà risolta durante la ricerca.
>* Con Lazy Ad Resolving, se più interruzioni pubblicitarie esistono contemporaneamente (VMAP), verranno risolte allo stesso tempo.
>* Non è consigliabile ridurre il valore di *setDelayAdLoadingTolerance() *al di sotto del valore predefinito (5 secondi). In questo modo il lettore potrebbe creare un &quot;buffer&quot; inutilmente.
>* Lazy Ad Resolving non influisce sugli annunci pre-roll.
>* Lazy Ad Resolving è attualmente supportato con Auditude-Plugin. È consigliabile non impostare ** setDelayAdLoadingsu true se si utilizza un risolutore personalizzato.
>


