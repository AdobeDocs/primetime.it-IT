---
description: Puoi inserire annunci nel tuo VOD e contenuti live/lineari utilizzando l'interfaccia Adobe Primetime ad Decioning.
title: Requisiti in materia di pubblicità
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# Timeout annuncio {#ad-timeout}

## Requisiti di base AV {#av-foundation-requirements}

Nel caso di contenuti VOD, la combinazione di playlist, che comporta il caricamento principale del manifesto di contenuto, la risoluzione degli annunci e il caricamento del manifesto di annunci, deve essere completata entro 35 secondi.

In caso di contenuti live, ogni volta che la playlist viene aggiornata, la cucitura della playlist deve essere completata entro 20 secondi

**API rilevanti per il timeout di AdResolution**

```
/** @name Properties */
/** The default timeout value (in seconds) for resolution of ad requests is 15 seconds.
*
*/
*
@property (notatomic, assign) double adResolutionTimeout;
```

Puoi impostare adResolutionTimeout impostando PTAdMetadata::adResolutionTimeout durante la configurazione dei metadati dell&#39;annuncio.

```
// Create an instance of PTAuditudeMetadata and set its property
PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init]autorelease];;
adMetadata.adResolutionTimeout = 15 seconds
```

Quindi segui la sezione: [Metadati di Primetime ad server](/help/programming/tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-primetime-ad-serving-metadata/ios-3x-primetime-ad-serving-metadata.md).

**API rilevanti per il timeout di AdManifest**

```
/** @name Properties */
 /** The default timeout value (in seconds) for loading of ad manifests is 5 seconds.
 *
 */
 *
 @property (notatomic, assign) double adManifestTimeout; 
```

Puoi impostare adManifestTimeout impostando PTAdMetadata::adManifestTimeout durante la configurazione dei metadati dell&#39;annuncio.


```
// Create an instance of PTAuditudeMetadata and set its property
PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init]autorelease];;
adMetadata.adManifestTimeout = 5 seconds
```

Quindi segui la sezione: [Metadati di Primetime ad server](/help/programming/tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-primetime-ad-serving-metadata/ios-3x-primetime-ad-serving-metadata.md).
