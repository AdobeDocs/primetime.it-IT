---
description: Queste modifiche nell’API TVSDK per Android supportano l’eliminazione e la sostituzione degli annunci.
title: Modifiche all’API di cancellazione e sostituzione degli annunci
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 0%

---


# Modifiche all&#39;API di cancellazione e sostituzione degli annunci{#ad-deletion-and-replacement-api-changes}

Queste modifiche nell’API TVSDK per Android supportano l’eliminazione e la sostituzione degli annunci.

* `AdSignalingMode` Nuova modalità di segnalazione degli intervalli di tempo personalizzati

* `AdvertisingMetadata` Nuovo  `setTimeRanges(TimeRangeCollection timeRanges, Metadata options)`: Imposta gli intervalli di tempo da contrassegnare, eliminare o sostituire durante l’elaborazione dei metadati

* `ContentResolver`

   * Nuovo `public final boolean canResolve(PlacementOpportunity placementOpportunity)`
   * Nuovo `protected abstract boolean doCanResolve(PlacementOpportunity placementOpportunity)`

* Nuova classe `ContentRemoval`

   `TimelineOperation` Classe che definisce l’intervallo di tempo da rimuovere dalla timeline

* `AuditudeResolver`

   * Nuovo `private LinkedList<AuditudeRequest> _requestQueue`
   * Nuovo `void startConsumer()`: Avvia l&#39;elaborazione della coda di richiesta Primetime ad Decioning e assicura che ogni richiesta venga emessa a intervalli `MIN_INIT_REQUEST_INTERVAL`

   * Nuovo `processReplacementRange()`: Estrae intervalli di tempo dai metadati dell&#39;annuncio e genera `PlacementInformations`, e crea una richiesta di Ad Decioning Primetime contenente il tag `PlacementInformations`.

   * Nuovo `canDoResolver()`: Controlla se le opportunità di posizionamento hanno metadati Primetime e decisioning

* Nuova classe Helper `CustomRangeHelper` che estrae i metadati dell&#39;intervallo di tempo dai metadati dell&#39;annuncio e rimuove sottoinsiemi/sovrapposizioni/intervalli di tempo non validi.

* Nuovo `DeleteContentResolver` risolutore di contenuti che risolve le opportunità di posizionamento di `PlacementInformation.Mode.DELETE`

* Nuova `NopTimelineOperation` operazione timeline per i casi in cui non è necessario effettuare la sostituzione o il posizionamento di un annuncio. Questa classe viene utilizzata per distinguere tra questo e quando si verifica un errore durante il processo di risoluzione.

* `TimelineOperationQueue` Controlla se l&#39;operazione Timeline è una  `NopTimelineOperation` prima dell&#39;elaborazione.

* `CustomAdMarkersContentResolver` Nuovo  `canDoResolve()`: Controlla se un&#39;opportunità di posizionamento è di tipo  `Mode.MARK`

* `MetadataResolver` Nuovo  `canDoResolve()`: Controlla se un&#39;opportunità di posizionamento è di tipo  `Mode.INSERT`

* `DefaultMetadataKeys` Nuovo  `TIME_RANGES_METADATA_KEY("time_ranges_metadata_key")`

* `PlacementInformation`

   * Nuova modalità `enum (INSERT, DELETE, REPLACE, MARK)`
   * Nuovo tipo `CUSTOM_TIME_RANGES`

* `TimeRange` Nuovo  `compareTo(TimeRange timeRange)`: Quindi può ordinare TimeRanges in base all&#39;ora di inizio

* Il nuovo `ReplacementTimeRange` estende la classe `TimeRange` che rappresenta un intervallo temporale di sostituzione con un parametro `begin`, `end` e `replacement-duration`.

* `TimeRangeCollection`

   * Nuovo `MARK_RANGES, DELETE_RANGES, REPLACE_RANGES`
   * È stato rinominato `CUSTOM_AD_MARKERS` in `MARK_RANGES`

   * Modificato `toMetadata(Metadata options)` per inserire intervalli di eliminazione/contrassegno/sostituzione nei metadati dell&#39;annuncio.

* `MediaPlayerNotification`

   * Nuovo `UNDEFINED_TIME_RANGES`: Quando la modalità di segnalazione degli annunci è Mappa server o Cue manifest e gli intervalli di sostituzione sono anche nei metadati dell&#39;annuncio, gli intervalli di sostituzione vengono ignorati.
   * Nuovo `REPLACE_RANGES_NOT_AVAILABLE`: Quando la modalità di segnalazione degli annunci è impostata su Intervalli di tempo personalizzati e gli intervalli di sostituzione non sono disponibili, viene inviato un avviso.

* `AdvertisingFactory` Nuovo  `public abstract List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultAdvertisingFactory` Nuovo  `public List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultContentResolverFactory` Nuovo  `public static List<ContentResolver> createContentResolvers(MediaResource resource, Context context)`

* `DefaultMediaPlayer`

   * In `prepareToPlay()`: Rende una ricerca iniziale pari a 0, perché se l’intervallo `[0,n]` viene eliminato, il lettore multimediale non viene riprodotto automaticamente.

   * In `prepareToPlay()`: Passa in rassegna l’elenco delle informazioni di posizionamento iniziale da risolvere per `mediaplayerclient` .

   * In `extractAdSignalingMode()`: Adatta alla nuova modalità Intervallo temporale personalizzato.
   * Nuovo `private static List<PlacementInformation> createInitalPlacementInformations()`: Genera le informazioni di posizionamento iniziale per la modalità di segnalazione degli annunci e i resolver dei contenuti (derivati dai metadati degli annunci).
   * In `ContentPlacementCompletedListener`: Controlla se `mediaPlayerClient` è `doneInitialResolving` prima di chiamare `endAdResolving`.

* `MediaPlayerClient`

   * Nuovo `List<ContentResolver> _contentResolvers`
   * Nuovo `int _reservations`
   * Nuovo `lookupContentResolver(PlacementOpportunity placementOpportunity)`: Cerca quale risolutore può risolvere il `PlacementOpportunity`.

   * Codice modificato per creare più resolver di contenuti.
   * Nuovo `public boolean doneInitialResolving()`: Controlla se ci sono opportunità da risolvere.

* `VideoEngineTimeline`

   * Nuovo `removeContent(TimelineOperation timelineOperation)`: Rimuove dalla timeline un determinato intervallo di contenuti.
   * Nuovo `removeContentByLocalTime(long begin, long end)`: Rimuove il contenuto per l’ora locale indicata da `begin` e `end`.

* `DefaultOpportunityDetectorFactory` Modificato  `createOpportunityDetector`: Per i flussi VOD, restituisce un nuovo valore solo  `SpliceOutOpportunityDetector` se non sono presenti intervalli MARK o REPLACE (in quanto tali intervalli hanno priorità rispetto alla modalità di segnalazione).

