---
description: Queste modifiche nell'API Android TVSDK supportano l'eliminazione e la sostituzione degli annunci.
title: Modifiche all’API di eliminazione e sostituzione dell’annuncio
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 0%

---

# Modifiche all’API di eliminazione e sostituzione dell’annuncio{#ad-deletion-and-replacement-api-changes}

Queste modifiche nell&#39;API Android TVSDK supportano l&#39;eliminazione e la sostituzione degli annunci.

* `AdSignalingMode` Nuova modalità di segnalazione annuncio intervallo di tempo personalizzato

* `AdvertisingMetadata` Nuovo `setTimeRanges(TimeRangeCollection timeRanges, Metadata options)`: imposta gli intervalli di tempo da contrassegnare, eliminare o sostituire durante l’elaborazione dei metadati

* `ContentResolver`

   * Nuovo `public final boolean canResolve(PlacementOpportunity placementOpportunity)`
   * Nuovo `protected abstract boolean doCanResolve(PlacementOpportunity placementOpportunity)`

* Nuovo `ContentRemoval` classe

  `TimelineOperation` classe che definisce l’intervallo di tempo da rimuovere dalla timeline

* `AuditudeResolver`

   * Nuovo `private LinkedList<AuditudeRequest> _requestQueue`
   * Nuovo `void startConsumer()`: avvia l’elaborazione della coda di richieste di Primetime ad decisioning e assicura che ogni richiesta venga inviata in `MIN_INIT_REQUEST_INTERVAL` intervalli

   * Nuovo `processReplacementRange()`: estrae intervalli di tempo dai metadati dell’annuncio e genera `PlacementInformations`e crea una richiesta di Ad Decisioning di Primetime contenente `PlacementInformations`.

   * Nuovo `canDoResolver()`: controlla se l’opportunità di posizionamento ha metadati di Primetime ad decisioning

* Nuovo `CustomRangeHelper` Classe helper che estrae i metadati dell’intervallo di tempo dai metadati dell’annuncio e rimuove sottoinsiemi/sovrapposizioni/intervalli di tempo non validi.

* Nuovo `DeleteContentResolver` Risolutore di contenuti che risolve le opportunità di posizionamento di `PlacementInformation.Mode.DELETE`

* Nuovo `NopTimelineOperation` Nuova operazione della timeline quando non è necessario eseguire il posizionamento o la sostituzione di un’interruzione pubblicitaria. Questa classe viene utilizzata per distinguere tra questo e quando si verifica un errore durante il processo di risoluzione.

* `TimelineOperationQueue` Controlla se l&#39;operazione della sequenza temporale è `NopTimelineOperation` prima dell’elaborazione.

* `CustomAdMarkersContentResolver` Nuovo `canDoResolve()`: controlla se un’opportunità di posizionamento è di tipo `Mode.MARK`

* `MetadataResolver` Nuovo `canDoResolve()`: controlla se un’opportunità di posizionamento è di tipo `Mode.INSERT`

* `DefaultMetadataKeys` Nuovo `TIME_RANGES_METADATA_KEY("time_ranges_metadata_key")`

* `PlacementInformation`

   * Nuova modalità `enum (INSERT, DELETE, REPLACE, MARK)`
   * Nuovo tipo `CUSTOM_TIME_RANGES`

* `TimeRange` Nuovo `compareTo(TimeRange timeRange)`: può ordinare gli intervalli di tempo in base all’ora di inizio

* Nuovo `ReplacementTimeRange` Estende il `TimeRange` classe che rappresenta un intervallo di tempo di sostituzione, con un `begin`, `end`, e `replacement-duration` parametro.

* `TimeRangeCollection`

   * Nuovo `MARK_RANGES, DELETE_RANGES, REPLACE_RANGES`
   * Rinominato `CUSTOM_AD_MARKERS` a `MARK_RANGES`

   * Modificato `toMetadata(Metadata options)` per inserire intervalli di eliminazione, contrassegnazione e sostituzione nei metadati di annunci.

* `MediaPlayerNotification`

   * Nuovo `UNDEFINED_TIME_RANGES`: quando la modalità di segnalazione dell’annuncio è Mappa server o Cue manifesto e gli intervalli di sostituzione sono presenti anche nei metadati dell’annuncio, gli intervalli di sostituzione vengono ignorati.
   * Nuovo `REPLACE_RANGES_NOT_AVAILABLE`: quando la modalità di segnalazione degli annunci è Intervalli di tempo personalizzati e gli intervalli di sostituzione non sono disponibili, viene inviato un avviso.

* `AdvertisingFactory` Nuovo `public abstract List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultAdvertisingFactory` Nuovo `public List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultContentResolverFactory` Nuovo `public static List<ContentResolver> createContentResolvers(MediaResource resource, Context context)`

* `DefaultMediaPlayer`

   * In entrata `prepareToPlay()`: effettua una ricerca iniziale a 0, perché se l’intervallo `[0,n]` viene eliminato, il lettore multimediale non viene riprodotto automaticamente.

   * In entrata `prepareToPlay()`: scorre l’elenco delle informazioni di posizionamento iniziale per `mediaplayerclient` per risolvere.

   * In entrata `extractAdSignalingMode()`: soddisfa la nuova modalità Intervallo di tempo personalizzato.
   * Nuovo `private static List<PlacementInformation> createInitalPlacementInformations()`: genera le informazioni sul posizionamento iniziale per la modalità di segnalazione degli annunci e i resolver di contenuto (derivati dai metadati degli annunci).
   * In entrata `ContentPlacementCompletedListener`: verifica se `mediaPlayerClient` è `doneInitialResolving` prima della chiamata `endAdResolving`.

* `MediaPlayerClient`

   * Nuovo `List<ContentResolver> _contentResolvers`
   * Nuovo `int _reservations`
   * Nuovo `lookupContentResolver(PlacementOpportunity placementOpportunity)`: cerca il risolutore che può risolvere il `PlacementOpportunity`.

   * È stato modificato il codice per creare più risolutori di contenuto.
   * Nuovo `public boolean doneInitialResolving()`: controlla se sono rimaste opportunità da risolvere.

* `VideoEngineTimeline`

   * Nuovo `removeContent(TimelineOperation timelineOperation)`: rimuove un dato intervallo di contenuto dalla timeline.
   * Nuovo `removeContentByLocalTime(long begin, long end)`: rimuove il contenuto in base all’ora locale specificata `begin` e `end`.

* `DefaultOpportunityDetectorFactory` Modificato `createOpportunityDetector`: per i flussi VOD, restituisce solo un nuovo `SpliceOutOpportunityDetector` se non sono presenti intervalli MARK o REPLACE (in quanto tali intervalli hanno priorità rispetto alla modalità di segnalazione).
