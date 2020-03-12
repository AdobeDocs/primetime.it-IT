---
description: Queste modifiche nel supporto TVSDK e nella sostituzione degli annunci.
seo-description: Queste modifiche nel supporto TVSDK e nella sostituzione degli annunci.
seo-title: Modifiche alle API di eliminazione e sostituzione degli annunci
title: Modifiche alle API di eliminazione e sostituzione degli annunci
uuid: 9d208d3b-6459-4aaf-bc56-53c405ccc1b6
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Modifiche alle API di eliminazione e sostituzione degli annunci {#ad-deletion-and-replacement-api-changes}

Queste modifiche nel supporto TVSDK e nella sostituzione degli annunci.

* `AdSignalingMode` È stata aggiunta la modalità `CUSTOM_RANGES` di segnalazione.

* `OpportunityGenerator`  `extractAdSignalingMode()` - Impostate `AdSignalingMode.CUSTOM_RANGES` se nei metadati sono presenti intervalli di sostituzione.

* `PlacementType` Aggiunto `CUSTOM_RANGE` tipo.

* `PlacementMode`

   * Aggiunta `DELETE` modalità.
   * Aggiunta `MARK` modalità
   * Modalità aggiunta: `FreeReplace` questa modalità ha una durata ma è un inserimento puro

* `TimeRange` Non più una `final` classe

* Aggiunto `ReplaceTimeRange()` metodo

   Estende `TimeRange` ad avere una `replacementDuration` proprietà. Per i casi MARK ed DELETE, `replacementDuration` è 0.

* `TimeRangeCollection`

   * È stata aggiunta la funzione `toReplaceMetadata()` di utilità per l&#39;estrazione `timeRanges`.

   * Modificato per lavorare con `DELETE` e `REPLACE`

   * `METADATA_KEY_CUSTOM_MARK_RANGES`, `METADATA_KEY_CUSTOM_DELETE_RANGES`, `METADATA_KEY_CUSTOM_REPLACE_RANGES`

* `CatalogItem`

   * Aggiunto `createCustomTimeRangesFrom()` - Crea metadati per i casi di utilizzo MARK/DELETE/REPLACE dal file JSON.
   * Rimosso `createCustomAdMarkersMetadataFrom()`

* `DefaultMetadataKeys`

   * Aggiunto `CUSTOM_DELETE_RANGES_METADATA_KEY`
   * Aggiunto `CUSTOM_REPLACE_RANGES_METADATA_KEY`
   * `CUSTOM_AD_MARKERS_METADATA_KEY` (non modificato)

* `DefaultContentFactory`

   * `doRetrieveGenerators()`

      * Aggiunto `CustomRangesOpportunityGenerator` per quando i metadati contengono intervalli personalizzati
   * `doRetrieveResolvers()`

      * Aggiungi `CustomRangeResolver` per quando nei metadati sono presenti intervalli personalizzati DELETE e REPLACE
      * Spostato `CustomAdMarkerResolver` prima di `AuditudeResolver`


* Aggiunto `CustomRangeOpportunityGenerator`

   * `doUpdate()` Lascia vuoto - nessun aggiornamento, VOD
   * `doProcess()` Crea una nuova posizione di un nuovo tipo `Placement.Delete_Range`

   * Aggiunto `CustomRangeOppotunityGenerator` all’inizio dell’elenco dei generatori in `DefaultContentFactory`, gli intervalli di eliminazione vengono elaborati prima degli inserimenti degli annunci.

   * Aggiunta `createCustomRangeOpportunities` per creare tutte le opportunità

      MARK - Un&#39;opportunità per ogni intervallo di marchi valido `PlacementType.CUSTOM_RANGE` e `PlacementMode.MARK`

      DELETE - Un&#39;opportunità per ogni intervallo di eliminazione valido `PlacementType.CUSTOM_RANGE` e `PlacementMode.DELETE`

      SOSTITUZIONE - Due opportunità per ogni intervallo di sostituzione valido:

      1. Un&#39;opportunità di eliminazione intervallo di `PlacementType.CUSTOM_RANGE` e `PlacementMode.DELETE`.

      1. Un annuncio Primetime e l&#39;opportunità di `PlacementType.MID_ROLL` o `PlacementType.PRE_ROLL` e `PlacementMode.FREEREPLACE`

* Aggiunto `CustomRangeResolver`:

   * `doCanResolve()` restituisce `true` gli intervalli di eliminazione.

   * Aggiunto `createDeleteRangeOperation()` per creare `DeleteRange` per il posizionamento

* Aggiunto `CustomRangeHelper`:

   * Classe di utilità comune per estrarre Mark/Delete/Replace `timeRanges` ed elaborarli.
   * Aggiunto `extractCustomRangesMetadata()`
   * Aggiunto `extractCustomRanges()`
   * Aggiunto `mergeRanges()` - Risolve conflitti e sottoinsiemi/unioni

* `MediaPlayerTimeline`:

   * &quot;>In `executeOperation()`, se l&#39;operazione è `DeleteRange`, è stata aggiunta una chiamata al metodo remove nell&#39;operazione

   * In `executeOperation()`, se l’operazione è `NOPTimelineOperation` (vuota `AdBreaks` proveniente dal server), è stata aggiunta una chiamata per cancellare.

   * Aggiunto `onDeleteRangeComplete()`
   * Aggiunto `removeRange()`
   * In `adjustPlacement()`, per `PlacementMode.FREEREPLACE` la modalità, azzerata la durata. Questa durata è necessaria in precedenza quando viene richiesto `AdBreaks`, a questo punto deve essere zero per essere un inserimento puro.

* `VideoEngineTimeline` Aggiunta `removeC3Ad()` - richiesta `removeByLocalTime()` di eliminazione degli intervalli

* `AdSignalingModeGenerator`

   * `doConfigure()` - Non risolvere se non viene generata alcuna opportunità
   * `createInitialOpportunity()` - Non generare opportunità iniziali per `AdSignalingMode.CUSTOM_RANGE`. La `CustomRangeOpportunityGenerator` copertura è già prevista.

* `DeleteRange`

   * Si Estende `TimelineOperation`.
   * Creato da `CustomRangeResolver` per eliminazione e sostituzione (la parte di eliminazione della sostituzione)

* `AuditudeConstant`

   * `MAX_PLACEMENTS_PER_REQUEST 1->5` - consenti imballaggio
   * `MINIMUM_AD_DURATION 10->5`

* `AuditudeRequest` Il `accepts()` metodo è stato modificato per consentire l&#39;imballaggio di tipo diverso (pre-roll, mid-roll, post-roll)

* `AuditudeRequestHelper` Correzioni di bug per consentire l&#39;override del server dei parametri di annuncio

* `AuditudeResolver` Il `canBePacked()` metodo è stato modificato per consentire l&#39;imballaggio

* `CustomAdResolver` Le funzioni `timeRange` di estrazione sono state rimosse. Prendiamo un posto alla volta, e lo trasformiamo in `AdBreakPlacement timelineOperation`.

