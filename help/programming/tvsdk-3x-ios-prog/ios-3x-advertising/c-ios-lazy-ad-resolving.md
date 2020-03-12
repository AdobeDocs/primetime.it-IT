---
description: La risoluzione degli annunci e il caricamento degli annunci potrebbero causare un ritardo inaccettabile per l'utente in attesa dell'avvio della riproduzione. La funzione Lazy Ad Loading Resolving può ridurre questo ritardo di avvio. Gli annunci ora possono essere risolti a un intervallo specificato prima della posizione dell'interruzione di annuncio. Ciò si ottiene utilizzando un approccio a doppio giocatore.
seo-description: La risoluzione degli annunci e il caricamento degli annunci potrebbero causare un ritardo inaccettabile per l'utente in attesa dell'avvio della riproduzione. La funzione Lazy Ad Loading Resolving può ridurre questo ritardo di avvio. Gli annunci ora possono essere risolti a un intervallo specificato prima della posizione dell'interruzione di annuncio. Ciò si ottiene utilizzando un approccio a doppio giocatore.
seo-title: Soluzione di annunci Just-in-Time
title: Soluzione di annunci Just-in-Time
uuid: f7b20439-3604-4d69-bdfe-2e0ad26f495b
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Soluzione di annunci Just-in-Time {#just-in-time-ad-resolving}

La risoluzione degli annunci e il caricamento degli annunci potrebbero causare un ritardo inaccettabile per l&#39;utente in attesa dell&#39;avvio della riproduzione. La funzione Lazy Ad Loading Resolving può ridurre questo ritardo di avvio. Gli annunci ora possono essere risolti a un intervallo specificato prima della posizione dell&#39;interruzione di annuncio. Ciò si ottiene utilizzando un approccio a doppio giocatore.

**Processo di base per la risoluzione e il caricamento degli annunci:**

1. TVSDK scarica un manifesto (playlist) e *risolve* tutti gli annunci.
1. TVSDK *carica* tutti gli annunci e blocca i segmenti degli annunci nei manifesti.
1. TVSDK sposta il lettore nello stato PREPARATO e inizia la riproduzione del contenuto.

Il lettore utilizza gli URL nel manifesto per ottenere il contenuto dell’annuncio (creativi), assicura che il contenuto dell’annuncio sia in un formato che possa essere riprodotto da TVSDK e che TVSDK inserisca gli annunci nella timeline. Questo processo di base per la risoluzione e il caricamento degli annunci può causare un ritardo inaccettabilmente lungo per un utente che attende di riprodurre il proprio contenuto, soprattutto se il manifesto contiene diversi URL di annunci.

**Lazy Ad Resolving:**

1. TVSDK scarica la playlist.
1. TVSDK *risolve e carica* eventuali annunci pre-roll, sposta il lettore nello stato PREPARATO e inizia la riproduzione del contenuto.
1. TVSDK *risolve* ogni interruzione di annuncio prima della sua posizione in base al valore definito in `PTAdMetadata::delayAdLoadingTolerance`.

Ad esempio, per impostazione predefinita `delayAdLoadingTolerance` è impostato su 5 secondi. Se un AdBreak è impostato per essere riprodotto alle 3:00, verrà risolto alle 2:55:00. Potete aumentare questo valore se ritenete che la risoluzione dell&#39;annuncio richieda più di 5 secondi.

>[!IMPORTANT]
>
>**Fattori da considerare con Lazy Ad Resolving:**
>* Lazy Ad Resolving è supportato solo per i flussi VOD solo con modalità SERVER_MAP e modalità di segnalazione annunci.
>* La risoluzione annuncio non è abilitata per impostazione predefinita. È necessario impostare `PTAdMetadata::delayAdLoading` = SÌ per attivarlo.
>* Lazy Ad Resolving è incompatibile con la funzione Instant On. Per ulteriori informazioni su Attivato istantaneo, consultate [Attivato](../../tvsdk-3x-ios-prog/ios-3x-instant-on-ios.md)istantaneo.
>* La modalità Picture-in-Picture non è supportata con Lazy Ad Resolving. Disattivate le modalità Picture-in-picture se attivate Lazy Ad Resolving.
>* La risoluzione degli annunci pigri non influisce sugli annunci pre-roll.
>


**Abilita risoluzione annunci pigri**

Potete attivare o disattivare la funzione Lazy Ad Resolving utilizzando il meccanismo di caricamento Lazy Ad esistente (Lazy Ad Resolving è disabilitato per impostazione predefinita).

Potete attivare la risoluzione degli annunci pigri impostando `PTAdMetadata::delayAdLoading`= SÌ quando configurate i metadati degli annunci.

**API rilevanti per la risoluzione degli annunci pigri:**

```
Class:    PTAdMetadata 
Properties: 
  
/** 
 * Property to define whether ad break resolution must be delayed until after stream start or not. 
 * When this value is NO, ads are resolved before stream start and spliced into the content when possible allowing  
   for a seamless playback experience. 
 * When this value is YES, ads are displayed in a secondary video player instance and resolved lazily only when  
   needed. 
 * Default value is NO 
 */ 
@property (nonatomic, assign) BOOL delayAdLoading; 
  
/** 
 * Property to define the lookahead for ad break resolution.  Ad breaks will be resolved when they occur between  
   the playhead time and the specified tolerance. 
 * If set to zero, the ad will be resolved immediately before playing the ad.  This may cause a slight delay in the  
   playback of the ads. 
 * Default value is 5.0 or 5 seconds. 
 */ 
  
@property (nonatomic, assign) NSTimeInterval delayAdLoadingTolerance;
```
