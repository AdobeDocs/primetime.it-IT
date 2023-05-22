---
description: Puoi decidere se risolvere solo gli annunci che si verificano dopo il punto di attivazione corrente dell’utente o anche gli annunci che si verificano prima del punto di attivazione corrente.
title: Carica annuncio per una finestra DVR
exl-id: 3e8542a8-0912-4023-904d-0fdb28411a9d
source-git-commit: 0019a95fa9ca6d21249533d559ce844897ab67cf
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# Carica annuncio per una finestra DVR {#load-ad-for-a-dvr-window}

Puoi decidere se risolvere solo gli annunci che si verificano dopo il punto di attivazione corrente dell’utente o anche gli annunci che si verificano prima del punto di attivazione corrente.

Quando un utente inizia a visualizzare il contenuto all’inizio di un flusso DVR, TVSDK risolve tutti gli annunci per il flusso in quel momento. Tuttavia, quando l’utente inizia a visualizzare il contenuto in un punto successivo all’inizio del flusso, puoi decidere se risolvere solo gli annunci che si verificano dopo il punto di attivazione corrente dell’utente o anche gli annunci che si sono verificati prima del punto di attivazione corrente.

>[!TIP]
>
>La risoluzione degli annunci dopo il punto live corrente è più veloce, ma se l’utente cerca all’indietro, questa opzione impedisce al lettore di riprodurre gli annunci apparsi in precedenza.

## Controllo e caricamento di una finestra DVR {#section_2D93E2E947644D66B6F6ED1DD6742C25}

Per controllare il caricamento di annunci per una finestra DVR:

Per caricare tutti gli annunci per l’intero flusso, imposta `PTAdMetadata.enableDVRAds` proprietà a `YES`.

>[!NOTE]
>
>Il valore predefinito è `NO`, e questa opzione carica gli annunci solo dal punto di attivazione corrente.

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
