---
description: Puoi decidere se risolvere solo gli annunci che si verificano dopo il live point dell'utente o anche risolvere quelli che si verificano prima del live point corrente.
seo-description: Puoi decidere se risolvere solo gli annunci che si verificano dopo il live point dell'utente o anche risolvere quelli che si verificano prima del live point corrente.
seo-title: Carica annuncio per una finestra DVR
title: Carica annuncio per una finestra DVR
uuid: 3ae1fbf6-deae-4f39-a17d-43d1fe3cb975
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Carica annuncio per una finestra DVR {#load-ad-for-a-dvr-window}

Puoi decidere se risolvere solo gli annunci che si verificano dopo il live point dell&#39;utente o anche risolvere quelli che si verificano prima del live point corrente.

Quando un utente inizia a visualizzare il contenuto all&#39;inizio di un flusso DVR, TVSDK risolve tutti gli annunci per il flusso in quel momento. Tuttavia, quando l&#39;utente inizia a visualizzare il contenuto in un punto successivo all&#39;inizio del flusso, potete decidere se risolvere solo gli annunci che si verificano dopo il punto attivo corrente dell&#39;utente o anche risolvere gli annunci che si sono verificati prima del punto attivo corrente.

>[!TIP]
>
>La risoluzione degli annunci dopo il punto attivo corrente è più rapida, ma se l&#39;utente cerca all&#39;indietro, questa opzione impedisce al lettore di riprodurre gli annunci visualizzati in precedenza.

## Controllo e caricamento per una finestra DVR {#section_2D93E2E947644D66B6F6ED1DD6742C25}

Per controllare e caricare una finestra DVR:

    Per caricare tutti gli annunci per l&#39;intero flusso, imposta la proprietà `PTAdMetadata.enableDVRAds` su `YES`.

>[!NOTE]
>
>Il valore predefinito è `NO`, e questa opzione carica gli annunci solo dal punto attivo corrente.

Ad esempio:

```
PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
 
PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init] autorelease];  
adMetadata.zoneId = <ZoneId>; 
adMetadata.domain = <Domain>; 
 
// Enable DVR Ads by setting to YES the enableDVRAds property on PTAdMetadata  
// (PTAuditudeMetadata is a subclass of PTAdMetadata)  
adMetadata.enableDVRAds = YES; 
 
[metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey]; 
 
//Create PTMediaPlayerItem with the previously prepared metadata    
playerItem = [[PTMediaPlayerItem alloc] initWithUrl:url mediaId:yourMediaID metadata:metadata]; 
```
