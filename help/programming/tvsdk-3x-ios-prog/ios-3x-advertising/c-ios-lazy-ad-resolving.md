---
description: La risoluzione degli annunci e il caricamento degli annunci possono causare un ritardo inaccettabile per un utente in attesa dell'avvio della riproduzione. La funzione Lazy Ad Loading Resolving può ridurre questo ritardo di avvio. Gli annunci possono ora essere risolti a un intervallo specificato prima della posizione dell’interruzione pubblicitaria. Ciò si ottiene utilizzando un approccio a doppio player.
title: Soluzione per annunci just-in-time
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---


# Risoluzione degli annunci just-in-time {#just-in-time-ad-resolving}

La risoluzione degli annunci e il caricamento degli annunci possono causare un ritardo inaccettabile per un utente in attesa dell&#39;avvio della riproduzione. La funzione Lazy Ad Loading Resolving può ridurre questo ritardo di avvio. Gli annunci possono ora essere risolti a un intervallo specificato prima della posizione dell’interruzione pubblicitaria. Ciò si ottiene utilizzando un approccio a doppio player.

**Processo di risoluzione e caricamento degli annunci di base:**

1. TVSDK scarica un manifesto (playlist) e *risolve* tutti gli annunci.
1. TVSDK *carica* tutti gli annunci e unisce i segmenti di annunci nei manifesti.
1. TVSDK sposta il lettore nello stato PREPARATO e inizia la riproduzione del contenuto.

Il lettore utilizza gli URL nel manifesto per ottenere il contenuto dell’annuncio (creativi), assicura che il contenuto dell’annuncio sia in un formato che TVSDK può riprodurre e TVSDK inserisce gli annunci nella timeline. Questo processo di base di risoluzione e caricamento degli annunci può causare un ritardo inaccettabilmente lungo per un utente che aspetta di riprodurre il proprio contenuto, soprattutto se il manifesto contiene diversi URL di annunci.

**Lazy Ad Resolving:**

1. TVSDK scarica la playlist.
1. TVSDK *risolve e carica* qualsiasi annuncio pre-roll, sposta il lettore nello stato PREPARATO e inizia la riproduzione del contenuto.
1. TVSDK *risolve* ogni annuncio prima della sua posizione in base al valore definito in `PTAdMetadata::delayAdLoadingTolerance`.

Ad esempio, per impostazione predefinita `delayAdLoadingTolerance` è impostato su 5 secondi. Se un AdBreak è impostato per essere riprodotto alle 3:00, verrà risolto alle 2:55:00. Puoi aumentare questo valore se ritieni che la risoluzione dell’annuncio richieda più di 5 secondi.

>[!IMPORTANT]
>
>**Fattori da considerare con Lazy Ad Resolving:**
>* Lazy Ad Resolving è supportato solo per i flussi VOD solo con le modalità SERVER_MAP e di segnalazione.
>* La risoluzione degli annunci pigri non è abilitata per impostazione predefinita. È necessario impostare `PTAdMetadata::delayAdLoading` = YES per attivarlo.
>* La risoluzione degli annunci pigri non è compatibile con la funzione Instant On. Per ulteriori informazioni su Attivato istantaneo, vedere [Attivato istantaneo](../../tvsdk-3x-ios-prog/ios-3x-instant-on-ios.md).
>* La modalità Picture-in-Picture non è supportata con Lazy Ad Resolving. Disattivare le modalità Picture-in-Picture se si abilita Lazy Ad Resolving.
>* La risoluzione degli annunci pigri non influisce sugli annunci pre-roll.

>


**Abilita risoluzione annunci pigri**

Puoi abilitare o disabilitare la funzione Lazy Ad Resolving utilizzando il meccanismo esistente Lazy Ad Loading (Lazy Ad Resolving è disabilitato per impostazione predefinita).

Puoi abilitare Lazy Ad Resolving impostando `PTAdMetadata::delayAdLoading`= YES durante la configurazione dei metadati dell&#39;annuncio.

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
