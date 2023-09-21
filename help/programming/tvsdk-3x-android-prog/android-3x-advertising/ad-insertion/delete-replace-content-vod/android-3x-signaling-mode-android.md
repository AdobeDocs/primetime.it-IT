---
description: Puoi contrassegnare, eliminare e sostituire gli intervalli di tempo nei flussi VOD utilizzando diverse combinazioni di metadati e modalità di segnalazione degli annunci. Diverse combinazioni di modalità di segnalazione e metadati determinano comportamenti diversi.
title: Effetto sull’inserimento e l’eliminazione di annunci dalla modalità di segnalazione degli annunci e dalle combinazioni di metadati di annunci
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# Effetto sull’inserimento e l’eliminazione di annunci dalla modalità di segnalazione degli annunci e dalle combinazioni di metadati di annunci {#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

Puoi contrassegnare, eliminare e sostituire gli intervalli di tempo nei flussi VOD utilizzando diverse combinazioni di metadati e modalità di segnalazione degli annunci. Diverse combinazioni di modalità di segnalazione e metadati determinano comportamenti diversi.

>[!TIP]
>
>In caso di conflitto tra gli intervalli di tempo e le modalità di segnalazione degli annunci, TVSDK assegna la priorità agli intervalli di tempo.

La tabella seguente fornisce i dettagli relativi alla modalità di segnalazione e ai comportamenti di combinazione dei metadati:

**Mappa server**

| **Metadati annuncio** | **Resolver creati** | **`PlacementInformations`creato** | **Comportamento risultante** |
|--- |--- |--- |--- |
|  | Elimina | Elimina | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Intervalli eliminati |
| Elimina, Auditude | Elimina, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE),` <br>`PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Intervalli eliminati, annunci inseriti |
| Auditude | Auditude | `PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Annunci inseriti |
| Sostituisci, Auditude | Elimina, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Intervalli sostituiti |
| Contrassegna | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalli contrassegnati |
| Contrassegna, Auditude | CustomAd, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalli contrassegnati, nessun annuncio inserito |

**Cue manifesto**

| Metadati annuncio | Resolver creati | `PlacementInformations` creato | Comportamento risultante |
|--- |--- |--- |--- |
| Auditude | Auditude | `PlacementInfo (Type.PRE_ROLL, Mode.INSERT)` | Annunci inseriti |
| Elimina, Auditude | Elimina, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)`<br>`PlacementInfo (Type.PRE_ROLL, Mode.INSERT)` | Intervalli eliminati, annunci inseriti |
| Contrassegna, Auditude | Contrassegna, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalli contrassegnati, nessun annuncio inserito |
| Elimina | Elimina | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Intervalli eliminati |
| Contrassegna | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalli contrassegnati |
| Sostituisci, Auditude | Elimina, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Intervalli sostituiti |

**Intervallo di tempo personalizzato**

| Metadati annuncio | Resolver creati | `PlacementInformations` creato | Comportamento risultante |
|--- |--- |--- |--- |
| Elimina | Elimina | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Intervalli eliminati |
| Elimina, Auditude | Elimina, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Intervalli eliminati, nessun annuncio inserito |
| Auditude | Auditude | Nessuno | Nessun annuncio inserito |
| Sostituisci, Auditude | Elimina, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Intervalli sostituiti con annunci |
| Contrassegna | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalli contrassegnati |
| Contrassegna, Auditude | Annuncio personalizzato, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalli contrassegnati, nessun annuncio inserito |

**Non impostato (impostazione predefinita)**

| Metadati annuncio | Resolver creati | `PlacementInformations` creato | Comportamento risultante |
|--- |--- |--- |--- |
| Elimina | Elimina | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Intervalli eliminati |
| Elimina, Auditude | Elimina, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Intervalli eliminati, annunci inseriti |
| Auditude | Auditude | `PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Annunci inseriti |
| Sostituisci, Auditude | Elimina, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Intervalli sostituiti con annunci |
| Contrassegna | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalli contrassegnati |
| Contrassegna, Auditude | CustomAd, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalli contrassegnati |
