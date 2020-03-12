---
description: Queste modifiche nell’API TVSDK per Android supportano l’eliminazione e la sostituzione degli annunci.
seo-description: Queste modifiche nell’API TVSDK per Android supportano l’eliminazione e la sostituzione degli annunci.
seo-title: Modifiche alle API di eliminazione e sostituzione degli annunci
title: Modifiche alle API di eliminazione e sostituzione degli annunci
uuid: 2bb8a331-6851-4442-99de-b01500a0e1e2
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Modifiche alle API di eliminazione e sostituzione degli annunci{#ad-deletion-and-replacement-api-changes}

Queste modifiche nell’API TVSDK per Android supportano l’eliminazione e la sostituzione degli annunci.

* `AdSignalingMode` Nuova modalità di indicazione dell&#39;intervallo di tempo personalizzato

* `AdvertisingMetadata` Nuovo `setTimeRanges(TimeRangeCollection timeRanges, Metadata options)`: Imposta gli intervalli di tempo da contrassegnare, eliminare o sostituire durante l&#39;elaborazione dei metadati

* `ContentResolver`

   * Nuovo `public final boolean canResolve(PlacementOpportunity placementOpportunity)`
   * Nuovo `protected abstract boolean doCanResolve(PlacementOpportunity placementOpportunity)`

* Nuova `ContentRemoval` classe

   `TimelineOperation` che definisce l&#39;intervallo di tempo da rimuovere dalla timeline

* `AuditudeResolver`

   * Nuovo `private LinkedList<AuditudeRequest> _requestQueue`
   * Nuovo `void startConsumer()`: Avvia l&#39;elaborazione della coda di richieste di decisioni pubblicitarie Primetime e assicura che ogni richiesta venga rilasciata a `MIN_INIT_REQUEST_INTERVAL` intervalli regolari

   * Nuovo `processReplacementRange()`: Estrae gli intervalli di tempo dai metadati dell&#39;annuncio e genera `PlacementInformations`e crea una richiesta di decisione annunci Primetime contenente il `PlacementInformations`.

   * Nuovo `canDoResolver()`: Controlla se le opportunità di posizionamento dispongono di metadati Primetime e di decisioni per gli annunci

* Nuova classe `CustomRangeHelper` Helper che estrae i metadati dell&#39;intervallo di tempo dai metadati degli annunci e rimuove sottoinsiemi/sovrapposizioni/intervalli di tempo non validi.

* Nuovo risolutore di `DeleteContentResolver` contenuti che risolve le opportunità di posizionamento `PlacementInformation.Mode.DELETE`

* Nuova `NopTimelineOperation` funzione della timeline per i casi in cui non è necessario inserire o sostituire un annuncio. Questa classe viene utilizzata per distinguere tra questo e quando si verifica un errore durante il processo di risoluzione.

* `TimelineOperationQueue` Controlla se l&#39;operazione della timeline è impostata su `NopTimelineOperation` prima dell&#39;elaborazione.

* `CustomAdMarkersContentResolver` Nuovo `canDoResolve()`: Controlla se un&#39;opportunità di posizionamento è di tipo `Mode.MARK`

* `MetadataResolver` Nuovo `canDoResolve()`: Controlla se un&#39;opportunità di posizionamento è di tipo `Mode.INSERT`

* `DefaultMetadataKeys` Nuovo `TIME_RANGES_METADATA_KEY("time_ranges_metadata_key")`

* `PlacementInformation`

   * Nuova modalità `enum (INSERT, DELETE, REPLACE, MARK)`
   * Nuovo tipo `CUSTOM_TIME_RANGES`

* `TimeRange` Nuovo `compareTo(TimeRange timeRange)`: È quindi possibile ordinare gli intervalli di tempo in base all&#39;ora di inizio

* Nuovo `ReplacementTimeRange` Estende la `TimeRange` classe che rappresenta un intervallo temporale di sostituzione, con un `begin`, `end`e `replacement-duration` parametro.

* `TimeRangeCollection`

   * Nuovo `MARK_RANGES, DELETE_RANGES, REPLACE_RANGES`
   * Rinominato `CUSTOM_AD_MARKERS` in `MARK_RANGES`

   * Modificato `toMetadata(Metadata options)` per inserire gli intervalli di eliminazione/contrassegno/sostituzione nei metadati degli annunci.

* `MediaPlayerNotification`

   * Nuovo `UNDEFINED_TIME_RANGES`: Quando la modalità di segnalazione degli annunci è Mappa server o Cue manifesto e gli intervalli di sostituzione sono presenti anche nei metadati dell’annuncio, gli intervalli di sostituzione vengono ignorati.
   * Nuovo `REPLACE_RANGES_NOT_AVAILABLE`: Quando la modalità di segnalazione degli annunci è Custom Time Ranges (Intervalli di tempo personalizzati) e gli intervalli di sostituzione non sono disponibili, viene inviato un avviso.

* `AdvertisingFactory` Nuovo `public abstract List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultAdvertisingFactory` Nuovo `public List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultContentResolverFactory` Nuovo `public static List<ContentResolver> createContentResolvers(MediaResource resource, Context context)`

* `DefaultMediaPlayer`

   * In `prepareToPlay()`: Esegue una ricerca iniziale su 0, perché se l&#39;intervallo `[0,n]` viene eliminato, il lettore multimediale non viene riprodotto automaticamente.

   * In `prepareToPlay()`: Esegue un ciclo tra l&#39;elenco delle informazioni di posizionamento iniziali `mediaplayerclient` da risolvere.

   * In `extractAdSignalingMode()`: Ideale per la nuova modalità Intervallo di tempo personalizzato.
   * Nuovo `private static List<PlacementInformation> createInitalPlacementInformations()`: Genera le informazioni di posizionamento iniziali per la modalità di segnalazione degli annunci e i risolutori di contenuti (derivati dai metadati degli annunci).
   * In `ContentPlacementCompletedListener`: Controlla se `mediaPlayerClient` è `doneInitialResolving` prima della chiamata `endAdResolving`.

* `MediaPlayerClient`

   * Nuovo `List<ContentResolver> _contentResolvers`
   * Nuovo `int _reservations`
   * Nuovo `lookupContentResolver(PlacementOpportunity placementOpportunity)`: Cerca quale risolutore può risolvere il `PlacementOpportunity`.

   * Codice modificato per creare più risolutori di contenuti.
   * Nuovo `public boolean doneInitialResolving()`: Controlla se sono rimaste altre opportunità da risolvere.

* `VideoEngineTimeline`

   * Nuovo `removeContent(TimelineOperation timelineOperation)`: Rimuove un determinato intervallo di contenuti dalla timeline.
   * Nuovo `removeContentByLocalTime(long begin, long end)`: Rimuove il contenuto per ora locale specificata `begin` e `end`.

* `DefaultOpportunityDetectorFactory` Modificato `createOpportunityDetector`: Per i flussi VOD, restituisce un nuovo valore solo `SpliceOutOpportunityDetector` se non sono presenti intervalli MARK o REPLACE (poiché tali intervalli hanno priorità rispetto alla modalità di segnalazione).

