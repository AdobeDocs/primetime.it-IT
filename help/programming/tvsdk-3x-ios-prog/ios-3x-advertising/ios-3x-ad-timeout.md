---
description: Puoi inserire annunci nel VOD e nel contenuto live/lineare utilizzando l’interfaccia di Adobe Primetime ad decisioning.
title: Requisiti pubblicitari
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# Timeout annuncio {#ad-timeout}

## Requisiti di base AV {#av-foundation-requirements}

In caso di contenuti VOD, l’unione delle playlist, che comporta il caricamento del manifesto del contenuto principale, la risoluzione degli annunci e il caricamento del manifesto degli annunci, deve essere completata entro 35 secondi.

Nel caso di contenuti live, ad ogni aggiornamento della playlist, l’unione delle playlist deve essere completata entro 20 secondi

**API relative al timeout di AdResolution**

```
/** @name Properties */
/** The default timeout value (in seconds) for resolution of ad requests is 15 seconds.
*
*/
*
@property (notatomic, assign) double adResolutionTimeout;
```

È possibile impostare adResolutionTimeout impostando PTAdMetadata::adResolutionTimeout durante la configurazione dei metadati dell&#39;annuncio.

```
// Create an instance of PTAuditudeMetadata and set its property
PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init]autorelease];;
adMetadata.adResolutionTimeout = 15 seconds
```

In seguito, segui la sezione: [Metadati di Primetime ad server](/help/programming/tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-primetime-ad-serving-metadata/ios-3x-primetime-ad-serving-metadata.md).

**API relative al timeout di AdManifest**

```
/** @name Properties */
 /** The default timeout value (in seconds) for loading of ad manifests is 5 seconds.
 *
 */
 *
 @property (notatomic, assign) double adManifestTimeout; 
```

È possibile impostare adManifestTimeout impostando PTAdMetadata::adManifestTimeout durante la configurazione dei metadati dell’annuncio.


```
// Create an instance of PTAuditudeMetadata and set its property
PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init]autorelease];;
adMetadata.adManifestTimeout = 5 seconds
```

In seguito, segui la sezione: [Metadati di Primetime ad server](/help/programming/tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-primetime-ad-serving-metadata/ios-3x-primetime-ad-serving-metadata.md).
