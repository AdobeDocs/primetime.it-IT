---
description: È possibile contrassegnare, eliminare e sostituire gli intervalli di tempo nei flussi VOD utilizzando diverse modalità di segnalazione degli annunci e combinazioni di metadati degli annunci. Diverse combinazioni di modalità di segnalazione e metadati determinano comportamenti diversi.
title: Effetto sull’inserimento e l’eliminazione degli annunci dalle combinazioni della modalità di segnalazione degli annunci e dei metadati degli annunci
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---


# Effetto sull&#39;inserimento e l&#39;eliminazione degli annunci dalle combinazioni di modalità ad Signing e metadati degli annunci {#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

È possibile contrassegnare, eliminare e sostituire gli intervalli di tempo nei flussi VOD utilizzando diverse modalità di segnalazione degli annunci e combinazioni di metadati degli annunci. Diverse combinazioni di modalità di segnalazione e metadati determinano comportamenti diversi.

>[!TIP]
>
>Quando si verifica un conflitto tra intervalli di tempo e modalità di segnalazione degli annunci, TVSDK assegna la priorità agli intervalli di tempo.

Nella tabella seguente sono riportati i dettagli relativi alla modalità di segnalazione e ai comportamenti di combinazione dei metadati:

**Mappa del server**

| **Metadati annuncio** | **Risolutori creati** | **`PlacementInformations`creato** | **Comportamento risultante** |
|--- |--- |--- |--- |
|  | Elimina | Elimina | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Intervalli eliminati |
| Elimina, Auditude | Elimina, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE),` <br>`PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Intervalli eliminati, Annunci inseriti |
| Auditude | Auditude | `PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Annunci inseriti |
| Sostituisci, Auditude | Elimina, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Intervalli sostituiti |
| Segna | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalli contrassegnati |
| Mark, Auditude | CustomAd, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalli contrassegnati, nessun annuncio inserito |

**Cue Manifesto**

| Metadati annuncio | Risolutori creati | `PlacementInformations` creato | Comportamento risultante |
|--- |--- |--- |--- |
| Auditude | Auditude | `PlacementInfo (Type.PRE_ROLL, Mode.INSERT)` | Annunci inseriti |
| Elimina, Auditude | Elimina, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)`<br>`PlacementInfo (Type.PRE_ROLL, Mode.INSERT)` | Intervalli eliminati, annunci inseriti |
| Mark, Auditude | Mark, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalli contrassegnati, nessun annuncio inserito |
| Elimina | Elimina | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Intervalli eliminati |
| Segna | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalli contrassegnati |
| Sostituisci, Auditude | Elimina, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Intervalli sostituiti |

**Intervallo di tempo personalizzato**

| Metadati annuncio | Risolutori creati | `PlacementInformations` creato | Comportamento risultante |
|--- |--- |--- |--- |
| Elimina | Elimina | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Intervalli eliminati |
| Elimina, Auditude | Elimina, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Intervalli eliminati, nessun annuncio inserito |
| Auditude | Auditude | Nessuno | Nessun annuncio inserito |
| Sostituisci, Auditude | Elimina, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Intervalli sostituiti dagli annunci |
| Segna | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalli contrassegnati |
| Mark, Auditude | Annuncio personalizzato, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalli contrassegnati, nessun annuncio inserito |

**Non impostato (predefinito)**

| Metadati annuncio | Risolutori creati | `PlacementInformations` creato | Comportamento risultante |
|--- |--- |--- |--- |
| Elimina | Elimina | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Intervalli eliminati |
| Elimina, Auditude | Elimina, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Intervalli eliminati, annunci inseriti |
| Auditude | Auditude | `PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Annunci inseriti |
| Sostituisci, Auditude | Elimina, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Intervalli sostituiti dagli annunci |
| Segna | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalli contrassegnati |
| Mark, Auditude | CustomAd, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalli contrassegnati |