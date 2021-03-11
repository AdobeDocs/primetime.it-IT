---
description: Queste modifiche in TVSDK supportano e cancellano e sostituiscono gli annunci.
title: Modifiche all’API di cancellazione e sostituzione degli annunci
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---


# Modifiche API di cancellazione e sostituzione degli annunci {#ad-deletion-and-replacement-api-changes}

Queste modifiche in TVSDK supportano e cancellano e sostituiscono gli annunci.

* `AdSignalingMode` È stata aggiunta la modalità  `CUSTOM_RANGES` di segnalazione.

* `OpportunityGenerator`  `extractAdSignalingMode()` - Imposta  `AdSignalingMode.CUSTOM_RANGES` se gli intervalli di sostituzione si trovano nei metadati.

* `PlacementType` È stato aggiunto  `CUSTOM_RANGE` il tipo .

* `PlacementMode`

   * È stata aggiunta la modalità `DELETE` .
   * È stata aggiunta la modalità `MARK`
   * È stata aggiunta la modalità `FreeReplace` : questa modalità ha una durata ma è un inserimento puro

* `TimeRange` Non più una  `final` classe

* È stato aggiunto il metodo `ReplaceTimeRange()`

   Estende `TimeRange` per avere una proprietà `replacementDuration`. Per i casi MARK e DELETE, `replacementDuration` è 0.

* `TimeRangeCollection`

   * È stata aggiunta la funzione di utilità `toReplaceMetadata()` per estrarre `timeRanges`.

   * Modificato per funzionare con `DELETE` e `REPLACE`

   * `METADATA_KEY_CUSTOM_MARK_RANGES`,  `METADATA_KEY_CUSTOM_DELETE_RANGES`,  `METADATA_KEY_CUSTOM_REPLACE_RANGES`

* `CatalogItem`

   * Aggiunto `createCustomTimeRangesFrom()` - Crea metadati per i casi d’uso MARK/DELETE/REPLACE dal file JSON.
   * Rimosso `createCustomAdMarkersMetadataFrom()`

* `DefaultMetadataKeys`

   * Aggiunto `CUSTOM_DELETE_RANGES_METADATA_KEY`
   * Aggiunto `CUSTOM_REPLACE_RANGES_METADATA_KEY`
   * `CUSTOM_AD_MARKERS_METADATA_KEY` (non modificato)

* `DefaultContentFactory`

   * `doRetrieveGenerators()`

      * Aggiunto `CustomRangesOpportunityGenerator` per quando i metadati contengono intervalli personalizzati
   * `doRetrieveResolvers()`

      * Aggiungi `CustomRangeResolver` per quando gli intervalli personalizzati di DELETE e SOSTITUISCI sono presenti nei metadati
      * Spostato `CustomAdMarkerResolver` davanti a `AuditudeResolver`


* Aggiunto `CustomRangeOpportunityGenerator`

   * `doUpdate()` Lascia vuoto - nessun aggiornamento, VOD
   * `doProcess()` Crea una nuova posizione di un nuovo tipo  `Placement.Delete_Range`

   * Aggiunto `CustomRangeOppotunityGenerator` nella parte superiore dell’elenco dei generatori in `DefaultContentFactory`, gli intervalli di eliminazione vengono elaborati prima degli inserimenti degli annunci.

   * È stato aggiunto `createCustomRangeOpportunities` per creare tutte le opportunità

      MARK - Un&#39;opportunità per ogni intervallo di marchi valido di `PlacementType.CUSTOM_RANGE` e `PlacementMode.MARK`

      DELETE - Un&#39;opportunità per ogni intervallo di eliminazione valido di `PlacementType.CUSTOM_RANGE` e `PlacementMode.DELETE`

      SOSTITUZIONE - Due opportunità per ogni intervallo di sostituzione valido:

      1. Un’opportunità di eliminazione dell’intervallo tra `PlacementType.CUSTOM_RANGE` e `PlacementMode.DELETE`.

      1. Un&#39;opportunità pubblicitaria Primetime di `PlacementType.MID_ROLL` o `PlacementType.PRE_ROLL` e `PlacementMode.FREEREPLACE`

* È stato aggiunto `CustomRangeResolver`:

   * `doCanResolve()` restituisce  `true` gli intervalli di eliminazione.

   * È stato aggiunto `createDeleteRangeOperation()` per creare `DeleteRange` per il posizionamento

* È stato aggiunto `CustomRangeHelper`:

   * Classe di utilità comune per estrarre Mark/Delete/Replace `timeRanges` ed elaborarli.
   * Aggiunto `extractCustomRangesMetadata()`
   * Aggiunto `extractCustomRanges()`
   * Aggiunto `mergeRanges()` - Risolve conflitti e sottoinsiemi/unioni

* `MediaPlayerTimeline`:

   * &quot;>In `executeOperation()`, se l&#39;operazione è `DeleteRange`, è stata aggiunta una chiamata per rimuovere il metodo nell&#39;operazione

   * In `executeOperation()`, se l&#39;operazione è `NOPTimelineOperation` (vuoto `AdBreaks` proveniente dal server), è stata aggiunta una chiamata per cancellare.

   * Aggiunto `onDeleteRangeComplete()`
   * Aggiunto `removeRange()`
   * In `adjustPlacement()`, per la modalità `PlacementMode.FREEREPLACE`, la durata è stata azzerata. Questa durata è necessaria in precedenza quando si richiede `AdBreaks`, a questo punto deve essere zero per essere un inserimento puro.

* `VideoEngineTimeline` Aggiunta  `removeC3Ad()` - chiamata  `removeByLocalTime()` per intervalli di eliminazione

* `AdSignalingModeGenerator`

   * `doConfigure()` - Non risolvere se non viene generata alcuna opportunità
   * `createInitialOpportunity()` - Non generare opportunità iniziali per  `AdSignalingMode.CUSTOM_RANGE`. Il `CustomRangeOpportunityGenerator` lo copre già.

* `DeleteRange`

   * Estende `TimelineOperation`.
   * Creato da `CustomRangeResolver` per eliminare e sostituire (la parte di eliminazione della sostituzione)

* `AuditudeConstant`

   * `MAX_PLACEMENTS_PER_REQUEST 1->5` - consentire l&#39;imballaggio
   * `MINIMUM_AD_DURATION 10->5`

* `AuditudeRequest` Il  `accepts()` metodo è stato modificato per consentire l&#39;imballaggio di diversi tipi di posizionamento (pre-roll, mid-roll, post-roll)

* `AuditudeRequestHelper` Correzioni di bug per consentire la sostituzione del server con i parametri degli annunci

* `AuditudeResolver` Il  `canBePacked()` metodo è stato modificato per consentire l&#39;imballaggio

* `CustomAdResolver` Le funzioni di  `timeRange` estrazione sono state rimosse. Otteniamo un posizionamento alla volta e lo trasformiamo in un `AdBreakPlacement timelineOperation`.

