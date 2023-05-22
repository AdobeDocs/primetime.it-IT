---
description: La risoluzione e il caricamento degli annunci possono causare un ritardo inaccettabile per l’utente in attesa dell’avvio della riproduzione. La funzione di risoluzione Lazy Ad Loading può ridurre questo ritardo di avvio. Gli annunci possono ora essere risolti a un intervallo specificato prima della posizione dell’interruzione pubblicitaria. Ciò si ottiene utilizzando un approccio basato sul doppio lettore.
title: Risoluzione degli annunci just-in-time
exl-id: dd5342c5-9f34-4778-a47a-91ff2eb03155
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# Risoluzione degli annunci just-in-time {#just-in-time-ad-resolving}

La risoluzione e il caricamento degli annunci possono causare un ritardo inaccettabile per l’utente in attesa dell’avvio della riproduzione. La funzione di risoluzione Lazy Ad Loading può ridurre questo ritardo di avvio. Gli annunci possono ora essere risolti a un intervallo specificato prima della posizione dell’interruzione pubblicitaria. Ciò si ottiene utilizzando un approccio basato sul doppio lettore.

**Processo di base di risoluzione e caricamento degli annunci:**

1. TVSDK scarica un manifesto (playlist) e *risolve* tutti gli annunci.
1. TVSDK *Carichi* tutti gli annunci e unisce i segmenti dell’annuncio nei manifesti.
1. TVSDK sposta il lettore nello stato READY e inizia la riproduzione del contenuto.

Il lettore utilizza gli URL nel manifesto per ottenere il contenuto dell’annuncio (creativi), si assicura che il contenuto dell’annuncio sia in un formato riproducibile da TVSDK e che TVSDK inserisca gli annunci nella timeline. Questo processo di base di risoluzione e caricamento degli annunci può causare un ritardo inaccettabilmente lungo per un utente in attesa di riprodurre il proprio contenuto, soprattutto se il manifesto contiene diversi URL di annunci.

**Risoluzione annunci lazy:**

1. TVSDK scarica la playlist.
1. TVSDK *risolve e carica* qualsiasi annuncio pre-roll, sposta il lettore nello stato READY e inizia la riproduzione del contenuto.
1. TVSDK *risolve* ogni annuncio si interrompe prima della sua posizione in base al valore definito in `PTAdMetadata::delayAdLoadingTolerance`.

Ad esempio, per impostazione predefinita `delayAdLoadingTolerance` è impostato su 5 secondi. Se un AdBreak è impostato per essere riprodotto alle 3:00, la risoluzione avverrà alle 2:55:00. Puoi aumentare questo valore se pensi che la risoluzione dell’annuncio richiederà più di 5 secondi.

>[!IMPORTANT]
>
>**Fattori da considerare con Lazy Ad Resolving:**
>* La risoluzione degli annunci lazy è supportata solo per i flussi VOD solo con modalità SERVER_MAP modalità di segnalazione degli annunci.
>* La funzione Lazy Ad Resolving non è attivata per impostazione predefinita. È necessario impostare `PTAdMetadata::delayAdLoading` = SÌ per abilitarlo.
>* Lazy Ad Resolving non è compatibile con la funzione Instant On. Per ulteriori informazioni su Instant On, vedere [Istantanea attiva](../../tvsdk-3x-ios-prog/ios-3x-instant-on-ios.md).
>* La modalità Picture-in-Picture non è supportata con Lazy Ad Resolving. Disattiva le modalità Picture-in-Picture se abiliti Lazy Ad Resolving.
>* La risoluzione lenta degli annunci non influisce sugli annunci pre-roll.
>

**Abilita lazy ad resolving**

Puoi abilitare o disabilitare la funzione Lazy Ad Resolving utilizzando il meccanismo esistente Lazy Ad Loading (Lazy Ad Resolving è disabilitato per impostazione predefinita).

Puoi abilitare Lazy Ad Resolving impostando `PTAdMetadata::delayAdLoading`= YES (SÌ) durante la configurazione dei metadati dell’annuncio.

**API rilevanti per la risoluzione lazy degli annunci:**

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
