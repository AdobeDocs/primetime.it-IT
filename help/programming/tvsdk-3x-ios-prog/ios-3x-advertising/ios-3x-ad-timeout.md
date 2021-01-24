---
description: Puoi inserire annunci nel tuo VOD e contenuti live/lineari utilizzando l'interfaccia  Adobe Primetime e decisionali.
seo-description: Puoi inserire annunci nel tuo VOD e contenuti live/lineari utilizzando l'interfaccia  Adobe Primetime e decisionali.
seo-title: Requisiti di pubblicità
title: Requisiti di pubblicità
uuid: 0287f1e4-746f-42e5-b811-409064dd9b13
translation-type: tm+mt
source-git-commit: 48ad8aad89701f8414e752a4d4e41da252d28d62
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---


# Timeout annuncio {#ad-timeout}

## Requisiti di AV Foundation {#av-foundation-requirements}

In caso di contenuto VOD, la cucitura della playlist, che comporta il caricamento del manifesto del contenuto principale, la risoluzione e il caricamento del manifesto dell&#39;annuncio, deve essere completata entro 35 secondi.

Nel caso di contenuti live, ogni volta che la playlist viene aggiornata, la cucitura della playlist deve essere completata entro 20 secondi

**API relative al timeout di AdResolution**

```
/** @name Properties */
/** The default timeout value (in seconds) for resolution of ad requests is 15 seconds.
*
*/
*
@property (notatomic, assign) double adResolutionTimeout;
```

Potete impostare adResolutionTimeout impostando PTAdMetadata::adResolutionTimeout durante la configurazione dei metadati dell’annuncio.

```
// Create an instance of PTAuditudeMetadata and set its property
PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init]autorelease];;
adMetadata.adResolutionTimeout = 15 seconds
```

Seguite la sezione: [Metadati del server di annunci Primetime](/help/programming/tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-primetime-ad-serving-metadata/ios-3x-primetime-ad-serving-metadata.md).

**API relative al timeout di AdManifest**

```
/** @name Properties */
 /** The default timeout value (in seconds) for loading of ad manifests is 5 seconds.
 *
 */
 *
 @property (notatomic, assign) double adManifestTimeout; 
```

Puoi impostare adManifestTimeout impostando PTAdMetadata::adManifestTimeout durante la configurazione dei metadati dell’annuncio.


```
// Create an instance of PTAuditudeMetadata and set its property
PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init]autorelease];;
adMetadata.adManifestTimeout = 5 seconds
```

Seguite la sezione: [Metadati del server di annunci Primetime](/help/programming/tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-primetime-ad-serving-metadata/ios-3x-primetime-ad-serving-metadata.md).
