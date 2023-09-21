---
description: La risoluzione e il caricamento degli annunci possono causare un ritardo inaccettabile per l’utente in attesa dell’avvio della riproduzione. Le funzioni Lazy Ad Loading e Lazy Ad Resolving possono ridurre questo ritardo di avvio. Lazy Ad Resolving è cambiato in modo significativo nella versione 3.0. Nel caricamento di Lazy Ad prima della versione 3.0, la risoluzione dell’annuncio è stata suddivisa in due passaggi, risolvendo solo gli annunci pre-roll prima dello stato READY e mid-roll e post-roll dopo lo stato READY. Questa situazione è cambiata e le interruzioni pubblicitarie vengono ora risolte a un intervallo specificato prima della posizione dell’interruzione pubblicitaria.
keywords: Lazy;Risoluzione annuncio;Caricamento annuncio
title: Risoluzione degli annunci just-in-time
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 0%

---

# Panoramica {#just-in-time-ad-resolving-overview}

La risoluzione e il caricamento degli annunci possono causare un ritardo inaccettabile per l’utente in attesa dell’avvio della riproduzione. Le funzioni Lazy Ad Loading e Lazy Ad Resolving possono ridurre questo ritardo di avvio. Lazy Ad Resolving è cambiato in modo significativo nella versione 3.0. Nel caricamento di Lazy Ad prima della versione 3.0, la risoluzione dell’annuncio è stata suddivisa in due passaggi, risolvendo solo gli annunci pre-roll prima dello stato READY e mid-roll e post-roll dopo lo stato READY. Questa situazione è cambiata e le interruzioni pubblicitarie vengono ora risolte a un intervallo specificato prima della posizione dell’interruzione pubblicitaria.

* Processo di base di risoluzione e caricamento degli annunci:

   1. TVSDK scarica un manifesto (playlist) e *risolve* tutti gli annunci.
   1. TVSDK *Carichi* tutti gli annunci e li inserisce nella timeline.
   1. TVSDK sposta il lettore nello stato READY e inizia la riproduzione del contenuto.

  Il lettore utilizza gli URL nel manifesto per ottenere il contenuto dell’annuncio (creativi), si assicura che il contenuto dell’annuncio sia in un formato riproducibile da TVSDK e che TVSDK inserisca gli annunci nella timeline. Questo processo di base di risoluzione e caricamento degli annunci può causare un ritardo inaccettabilmente lungo per un utente in attesa di riprodurre il proprio contenuto, soprattutto se il manifesto contiene diversi URL di annunci.

* *Caricamento annuncio lazy*:

   1. TVSDK scarica una playlist e *risolve* tutti gli annunci.
   1. TVSDK *Carichi* pre-roll di annunci, sposta il lettore nello stato READY e inizia la riproduzione del contenuto.
   1. TVSDK *Carichi* gli annunci rimanenti e li inserisce nella timeline durante la riproduzione.

  Questa funzione migliora il processo di base portando il lettore nello stato READY prima che tutti gli annunci vengano caricati.

* *Lazy Ad Resolving*:

   1. TVSDK scarica la playlist.
   1. TVSDK risolve e carica tutti gli annunci pre-roll, sposta il lettore nello stato READY e inizia la riproduzione del contenuto.
   1. TVSDK risolve e ciascuno degli annunci rimanenti si interrompe singolarmente in base al seguente calcolo:

      `AdvertisingMetadata::getDelayAdLoadingTolerance() + PlayBufferTime::playBufferTime + the value defined in EXT-X-TARGETDURATION`

      Per impostazione predefinita, per i contenuti con una durata di Target di 6 secondi, sarà 5,0 + 30,0 + 6,0 secondi (41 secondi)

   1. Se un’interruzione pubblicitaria si verifica entro 10 secondi dalla posizione di avvio, verrà risolta insieme agli annunci pre-roll prima dello stato PREPARATO.

>[!IMPORTANT]
>
>**Fattori da considerare con Lazy Ad Resolving:**
>
>* La risoluzione degli annunci lazy è supportata solo per i flussi VOD solo con le modalità SERVER_MAP e MANIFEST_CUES.
>* La funzione Lazy Ad Resolving non è attivata per impostazione predefinita. Se è disattivato, tutti gli annunci vengono risolti sui flussi VOD prima dell’avvio della riproduzione.
>* Lazy Ad Resolving non è compatibile con la funzione Instant On. Per ulteriori informazioni su Instant On, vedere Instant On.
>* Con Lazy Ad Resolving, durante la ricerca in avanti su un’interruzione pubblicitaria, l’interruzione pubblicitaria più vicina alla posizione di ricerca verrà risolta durante la ricerca.
>* Con Lazy Ad Resolving, se esistono più interruzioni pubblicitarie contemporaneamente (VMAP), queste verranno risolte contemporaneamente.
>* Si sconsiglia di ridurre il valore di *setDelayAdLoadingTolerance() *al di sotto del valore predefinito (5 secondi). Così facendo, il lettore potrebbe effettuare un &quot;buffer&quot; non necessario.
>* Lazy Ad Resolving non influisce sugli annunci pre-roll.
>* Il Lazy Ad Resolving è attualmente supportato con il plug-in di Auditude. Si consiglia di non impostare *setDelayAdLoading* to true se si utilizza un resolver personalizzato.
>
