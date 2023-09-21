---
description: Queste modifiche in TVSDK supportano l’eliminazione e la sostituzione degli annunci.
title: Modifiche all’API di eliminazione e sostituzione dell’annuncio
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# Modifiche all’API di eliminazione e sostituzione dell’annuncio {#ad-deletion-and-replacement-api-changes}

Queste modifiche in TVSDK supportano l’eliminazione e la sostituzione degli annunci.

* `AdSignalingMode` Aggiunto `CUSTOM_RANGES` modalità di segnalazione.

* `OpportunityGenerator`  `extractAdSignalingMode()` - Imposta `AdSignalingMode.CUSTOM_RANGES` se i metadati contengono intervalli di sostituzione.

* `PlacementType` Aggiunto `CUSTOM_RANGE` tipo.

* `PlacementMode`

   * Aggiunto `DELETE` modalità.
   * Aggiunto `MARK` modalità
   * Aggiunto `FreeReplace` modalità: questa modalità ha una durata ma è un inserimento puro

* `TimeRange` Non più un `final` classe

* Aggiunto `ReplaceTimeRange()` metodo

  Estende `TimeRange` avere un `replacementDuration` proprietà. Per le cause MARK e DELETE: `replacementDuration` è 0.

* `TimeRangeCollection`

   * Aggiunto `toReplaceMetadata()` funzione di utilità da estrarre `timeRanges`.

   * Modificato per funzionare con `DELETE` e `REPLACE`

   * `METADATA_KEY_CUSTOM_MARK_RANGES`, `METADATA_KEY_CUSTOM_DELETE_RANGES`, `METADATA_KEY_CUSTOM_REPLACE_RANGES`

* `CatalogItem`

   * Aggiunto `createCustomTimeRangesFrom()` : crea metadati per i casi d’uso MARK/DELETE/REPLACE dal file JSON.
   * Rimosso `createCustomAdMarkersMetadataFrom()`

* `DefaultMetadataKeys`

   * Aggiunto `CUSTOM_DELETE_RANGES_METADATA_KEY`
   * Aggiunto `CUSTOM_REPLACE_RANGES_METADATA_KEY`
   * `CUSTOM_AD_MARKERS_METADATA_KEY` (non modificato)

* `DefaultContentFactory`

   * `doRetrieveGenerators()`

      * Aggiunto `CustomRangesOpportunityGenerator` per specificare quando i metadati contengono intervalli personalizzati

   * `doRetrieveResolvers()`

      * Aggiungi `CustomRangeResolver` per quando gli intervalli personalizzati DELETE e REPLACE sono presenti nei metadati
      * Spostato `CustomAdMarkerResolver` prima di `AuditudeResolver`

* Aggiunto `CustomRangeOpportunityGenerator`

   * `doUpdate()` Foglie vuote - nessun aggiornamento, VOD
   * `doProcess()` Crea un nuovo posizionamento di un nuovo tipo `Placement.Delete_Range`

   * Aggiunto `CustomRangeOppotunityGenerator` all&#39;inizio dell&#39;elenco dei generatori in `DefaultContentFactory`Pertanto, gli intervalli di eliminazione vengono elaborati prima degli inserimenti di annunci.

   * Aggiunto `createCustomRangeOpportunities` per creare tutte le opportunità

     MARK: un&#39;opportunità per ogni intervallo di marchi valido di `PlacementType.CUSTOM_RANGE` e `PlacementMode.MARK`

     DELETE: un’opportunità per ogni intervallo di eliminazione valido di `PlacementType.CUSTOM_RANGE` e `PlacementMode.DELETE`

     SOSTITUISCI: due opportunità per ogni intervallo di sostituzione valido:

      1. Opportunità di eliminazione intervallo di `PlacementType.CUSTOM_RANGE` e `PlacementMode.DELETE`.

      1. Un’opportunità di ad decisioning di Primetime di `PlacementType.MID_ROLL` o `PlacementType.PRE_ROLL` e `PlacementMode.FREEREPLACE`

* Aggiunto `CustomRangeResolver`:

   * `doCanResolve()` restituisce `true` per eliminare gli intervalli.

   * Aggiunto `createDeleteRangeOperation()` per creare `DeleteRange` per il posizionamento

* Aggiunto `CustomRangeHelper`:

   * Classe di utilità comune per estrarre le opzioni Contrassegna/Elimina/Sostituisci `timeRanges` ed elaborarli.
   * Aggiunto `extractCustomRangesMetadata()`
   * Aggiunto `extractCustomRanges()`
   * Aggiunto `mergeRanges()` - Risoluzione di conflitti e sottoinsiemi/unioni

* `MediaPlayerTimeline`:

   * &quot;>In `executeOperation()`, se l&#39;operazione è `DeleteRange`, aggiunta chiamata al metodo remove nell&#39;operazione

   * In entrata `executeOperation()`, se l&#39;operazione è `NOPTimelineOperation` (vuoto `AdBreaks` dal server), aggiunta chiamata a clear.

   * Aggiunto `onDeleteRangeComplete()`
   * Aggiunto `removeRange()`
   * In entrata `adjustPlacement()`, per `PlacementMode.FREEREPLACE` , azzerata la durata. Questa durata è necessaria prima quando si richiede `AdBreaks`, a questo punto deve essere zero per essere un&#39;inserzione pura.

* `VideoEngineTimeline` Aggiunto `removeC3Ad()` - chiama `removeByLocalTime()` per eliminare intervalli

* `AdSignalingModeGenerator`

   * `doConfigure()` - Non risolvere se non viene generata alcuna opportunità
   * `createInitialOpportunity()` - Non generare opportunità iniziale per `AdSignalingMode.CUSTOM_RANGE`. Il `CustomRangeOpportunityGenerator` già copre questo aspetto.

* `DeleteRange`

   * Estende `TimelineOperation`.
   * Creato da `CustomRangeResolver` per la cancellazione e la sostituzione (la parte di eliminazione della sostituzione)

* `AuditudeConstant`

   * `MAX_PLACEMENTS_PER_REQUEST 1->5` - Consenti imballaggio
   * `MINIMUM_AD_DURATION 10->5`

* `AuditudeRequest` Il `accepts()` il metodo è stato modificato per consentire l’imballaggio di diversi tipi di posizionamento (pre-roll, mid-roll, post-roll)

* `AuditudeRequestHelper` Correzioni di bug per consentire l’override del server sui parametri dell’annuncio

* `AuditudeResolver` Il `canBePacked()` il metodo è stato modificato per consentire l&#39;imballaggio

* `CustomAdResolver` Il `timeRange` le funzioni di estrazione sono state rimosse. Otteniamo un posizionamento alla volta, e lo trasformiamo in un `AdBreakPlacement timelineOperation`.
