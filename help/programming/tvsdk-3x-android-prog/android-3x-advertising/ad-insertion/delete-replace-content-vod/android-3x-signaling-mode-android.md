---
description: Potete contrassegnare, eliminare e sostituire gli intervalli di tempo nei flussi VOD utilizzando diverse combinazioni di metadati e modalità di segnalazione annunci. Diverse combinazioni di modalità di segnalazione e metadati determinano comportamenti diversi.
seo-description: Potete contrassegnare, eliminare e sostituire gli intervalli di tempo nei flussi VOD utilizzando diverse combinazioni di metadati e modalità di segnalazione annunci. Diverse combinazioni di modalità di segnalazione e metadati determinano comportamenti diversi.
seo-title: Effetto sull’inserimento e l’eliminazione di annunci dalla modalità di segnalazione e dalle combinazioni di metadati degli annunci
title: Effetto sull’inserimento e l’eliminazione di annunci dalla modalità di segnalazione e dalle combinazioni di metadati degli annunci
uuid: 49abab49-4e52-477d-b7ed-688ee63e7473
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 0%

---


# Effetto sull&#39;inserimento e l&#39;eliminazione di annunci dalla modalità di segnalazione e dalle combinazioni di metadati degli annunci {#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

Potete contrassegnare, eliminare e sostituire gli intervalli di tempo nei flussi VOD utilizzando diverse combinazioni di metadati e modalità di segnalazione annunci. Diverse combinazioni di modalità di segnalazione e metadati determinano comportamenti diversi.

>[!TIP]
>
>In caso di conflitto tra intervalli di tempo e modalità di segnalazione degli annunci, TVSDK assegna la priorità agli intervalli di tempo.

Nella tabella seguente sono riportati i dettagli relativi alla modalità di segnalazione e ai comportamenti di combinazione di metadati:

**Mappa server**

| **Aggiungi metadati** | **Risolutori creati** | **`PlacementInformations`created** | **Comportamento risultante** |
|--- |--- |--- |--- |
|  | Elimina | Elimina | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Intervalli eliminati |
| Elimina, Auditude | Elimina, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE),` <br>`PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Intervalli eliminati, Annunci inseriti |
| Auditude | Auditude | `PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Annunci inseriti |
| Replace, Auditude | Elimina, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Intervalli sostituiti |
| Contrassegna | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalli contrassegnati |
| Mark, Auditude | CustomAd, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalli contrassegnati, nessun annuncio inserito |

**Cue Manifesto**

| Aggiungi metadati | Risolutori creati | `PlacementInformations` created | Comportamento risultante |
|--- |--- |--- |--- |
| Auditude | Auditude | `PlacementInfo (Type.PRE_ROLL, Mode.INSERT)` | Annunci inseriti |
| Elimina, Auditude | Elimina, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)`<br>`PlacementInfo (Type.PRE_ROLL, Mode.INSERT)` | Intervalli eliminati, annunci inseriti |
| Mark, Auditude | Mark, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalli contrassegnati, nessun annuncio inserito |
| Elimina | Elimina | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Intervalli eliminati |
| Contrassegna | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalli contrassegnati |
| Replace, Auditude | Elimina, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Intervalli sostituiti |

**Intervallo di tempo personalizzato**

| Aggiungi metadati | Risolutori creati | `PlacementInformations` created | Comportamento risultante |
|--- |--- |--- |--- |
| Elimina | Elimina | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Intervalli eliminati |
| Elimina, Auditude | Elimina, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Intervalli eliminati, nessun annuncio inserito |
| Auditude | Auditude | None | Nessun annuncio inserito |
| Replace, Auditude | Elimina, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Intervalli sostituiti con annunci |
| Contrassegna | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalli contrassegnati |
| Mark, Auditude | Annuncio personalizzato, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalli contrassegnati, nessun annuncio inserito |

**Not set (predefinito)**

| Aggiungi metadati | Risolutori creati | `PlacementInformations` created | Comportamento risultante |
|--- |--- |--- |--- |
| Elimina | Elimina | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)` | Intervalli eliminati |
| Elimina, Auditude | Elimina, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Intervalli eliminati, annunci inseriti |
| Auditude | Auditude | `PlacementInfo (Type.SERVER_MAP, Mode.INSERT)` | Annunci inseriti |
| Replace, Auditude | Elimina, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)` | Intervalli sostituiti con annunci |
| Contrassegna | CustomAd | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalli contrassegnati |
| Mark, Auditude | CustomAd, Auditude | `PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)` | Intervalli contrassegnati |