---
title: TVSDK da 1.4 a 2.5 per Android (Java)
description: TVSDK 2.5 offre diversi vantaggi rispetto alla versione 1.4 in termini di prestazioni, sicurezza, migliori integrazioni e altro ancora.
contentOwner: vishgupt
products: SG_PRIMETIME
topic-tags: migration
exl-id: 3b7f8355-ebea-4322-aef4-5393308391b5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '2323'
ht-degree: 0%

---

# TVSDK da 1.4 a 2.5 per Android (Java) {#tvsdk-to-for-android-java}

TVSDK 2.5 offre diversi vantaggi rispetto alla versione 1.4 in termini di prestazioni, sicurezza, migliori integrazioni e altro ancora.

TVSDK risolve i problemi più grandi, sul dispositivo più importante. Android continua a dominare il mercato globale, con oltre l&#39;86% della quota di mercato. La migrazione a TVSDK su Android ottimizzerà le prestazioni di riproduzione per migliorare il coinvolgimento degli utenti e accelerare il time-to-market con il supporto per nuovi formati di contenuto.

## Vantaggi della migrazione a TVSDK v2.5 {#benefits-of-migrating-to-tvsdk-v}

TVSDK 2.5 offre diversi vantaggi rispetto alla versione 1.4 in termini di prestazioni, sicurezza, migliori integrazioni e altro ancora. Continua a leggere per scoprire rapidamente i vantaggi della migrazione a questa nuova versione.

Secondo uno studio di benchmarking di terze parti, v2.5 fornisce una riduzione del tempo di avvio pari a 5 volte e una riduzione del numero di fotogrammi saltati di 3,8 volte rispetto alla media del settore.

| Funzioni di prestazioni | Descrizione |
|--- |--- |
| Attivazione immediata per VOD e Live | Precarica i segmenti TS iniziali per la riproduzione immediata per VOD e i flussi live-lineari quando si passa da un canale all’altro, per un’esperienza simile a quella TV. |
| Caricamento annuncio lazy | Avvia la riproduzione non appena il pre-roll o il contenuto è disponibile durante la risoluzione degli annunci mid-roll in un thread parallelo. |
| Connessioni di rete persistenti | Aumento dell’efficienza e riduzione della latenza del codice di rete per prestazioni di riproduzione più veloci. |
| Logica ABR migliorata | La nuova logica ABR si basa sulla lunghezza del buffer, sul tasso di variazione della lunghezza del buffer e sulla larghezza di banda misurata. Questo assicura che l&#39;ABR scelga il bit rate corretto quando la larghezza di banda fluttua e ottimizza anche il numero di volte che l&#39;interruttore di bitrate si verifica effettivamente monitorando la velocità con cui cambia la lunghezza del buffer. |
| Download parziale dei segmenti | Avvia la riproduzione non appena sono disponibili abbastanza fotogrammi da un segmento per il rendering del video in modo affidabile sul lato client. |
| Download paralleli | TVSDK scarica segmenti audio e video in parallelo per contenuti demussi per ottimizzare le prestazioni di riproduzione. |

Le funzioni di riproduzione migliorano il coinvolgimento dei clienti offrendo l&#39;esperienza di una trasmissione lineare su dispositivi digitali. Inoltre, aiuta a sfruttare DRM nativo come Widevine per la riproduzione HD.

| Funzioni di riproduzione | Descrizione |
|--- |--- |
| Riproduzione MP4 | Non è necessario transcodificare nuovamente le clip MP4 brevi per la riproduzione in TVSDK. |
| Riproduzione contenuto VOD DASH | Sono supportati i casi di utilizzo della riproduzione VOD con DASH di base. |
| Smooth Trickplay con ABR | Supporto per l&#39;avanzamento e il riavvolgimento rapido in HLS utilizzando fotogrammi chiave a basse velocità e I-Frame a velocità più elevate. Supporto ABR per tutti i frame supportati. |

Queste caratteristiche sono importanti per soddisfare i requisiti di studio, come la riproduzione HD su DRM nativo.

| Funzioni | Descrizione |
|--- |--- |
| Protezione dell&#39;output basata sulla risoluzione | La riproduzione può essere limitata solo a determinate risoluzioni consentite dai requisiti DRM. Disponibile solo tramite DRM Primetime. |
| Supporto widevine | Supportato con flussi VOD DASH per abilitare casi d’uso DRM nativi. |

Il miglioramento della fatturazione diretta elimina la necessità di creare rapporti manuali per la fatturazione ogni mese. VHL 2.0 consente tempi di commercializzazione più rapidi grazie all’integrazione pre-build e a una maggiore precisione nel tracciamento.

| Funzioni | Descrizione |
|--- |--- |
| Integrazione Moat | Supporto per la misurazione della visualizzabilità degli annunci da Moat. |
| VHL 2.0 | La più recente integrazione della libreria heartbeat video ottimizzata per la raccolta automatica dei dati di utilizzo per Adobe Analytics. |
| Supporto failover | Sono state implementate strategie aggiuntive per continuare la riproduzione ininterrotta, nonostante gli errori dei server host, dei file delle playlist e dei segmenti. |
| Integrazione fatturazione diretta | Invia le metriche di fatturazione al backend di Adobe Analytics certificato da Adobe Primetime per i flussi utilizzati dal cliente. |

>[!NOTE]
>
>Tutte le funzioni di TVSDK v1.4 sono supportate nella versione v2.5, ad eccezione del supporto Multi-CDN.

## Panoramica del processo di migrazione {#overview-of-the-migration-process}

La migrazione fluida da TVSDK 1.4 a 2.5 comporta la modifica alle librerie della versione 2.5, la ricompilazione e l’utilizzo di questo documento per facilitare il debug di eventuali problemi.

Le librerie TVSDK v1.4 non funzionano e coesistono con le librerie v2.5. Devi utilizzare le librerie v2.5 con TVSDK 2.5 e migrare le applicazioni e le integrazioni per eseguire l’aggiornamento a TVSDK 2.5. Questo documento descrive come e cosa modificare nel codice dell’applicazione e come risolvere gli errori durante la ricompilazione.

Il file psdk.jar utilizza librerie di terze parti per supportare funzioni diverse. Per impedire la rimozione delle librerie, includi quanto segue nella `proguard.cfg` file:

```java
# Adobe TVSDK keep classes
-keep class com.adobe.** { *; }
-keep class com.google.android.exoplayer.**
{ *; }
```

In `build.gradle` , è necessario includere la direttiva di compilazione per includere i file JAR basati su TVSDK. Se la tua app include Adobe Video Analytics, devi includere la direttiva di compilazione per i file JAR aggiuntivi necessari, ad Adobe per l’integrazione di Video Analytics nell’app

```java
# Compile Adobe TVSDK jars compile files('libs/psdk-va.jar')
compile files('libs/VideoHeartbeat.jar')
```

Le modifiche minori multiple non sono trattate in questo documento. Per le modifiche API minori, consulta [TVSDK 2.5 per API Java Android](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.5/index.html). Il riferimento API C++ corrispondente include descrizioni dettagliate. Per analoga documentazione API C++, consulta [TVSDK 2.5 per API Android C++](https://help.adobe.com/en_US/primetime/api/psdk/cpp_2.5/index.html).

Esempi multipli dell’utilizzo delle API sono trattati nell’implementazione di riferimento distribuita con TVSDK.

## Modifiche all’API in TVSDK v2.5 {#api-changes-in-tvsdk-v}

Di seguito sono documentate le API nuove, obsolete e modificate.

| TVSDK v1.4 | TVSDK v2.5 | Descrizione |
|--- |--- |--- |
| importa com.adobe.ave.drm .DRMAcquireLicenseSettings | importa com.adobe.mediacore.drm .DRMAcquireLicenseSettings; | Tutti i nomi delle classi nell’API TVSDK 2.5 iniziano con il prefisso com.adobe.mediacore. Questo è solo un esempio. |
| MediaPlayerException, IllegalStateException o IllegalArgumentException | MediaPlayerException | Nella versione 2.5, le API generano solo MediaPlayerException. |
| MediaPlayer.PlayerState (MediaPlayer.Event.PLAYBACK) | MediaPlayerStatus (MediaPlayerEvent.STATUS_CHANGED) | Nella versione 2.5, MediaPlayer.PlayerState è stato rinominato in un enum separato MediaPlayerStatus. |
| DefaultMediaPlayer.create (getActivity().getApplicationContext()) | MediaPlayer mediaPlayer = new MediaPlayer(getActivity(). getApplicationContext(); | I metodi statici utilizzati per creare gli oggetti vengono sostituiti da costruttori pubblici. |
| MediaPlayer.seekToLocalTime() | MediaPlayer.seekToLocal() | Il metodo MediaPlayer.seekToLocalTime() è ora denominato MediaPlayer.seekToLocal(). |
| closedCaptionsTrack.isActive() |  | Non disponibile |
| MetadataNode | Metadati | Nella versione 2.5, la classe Metadata sostituisce l&#39;utilizzo della classe MetadataNode v1.4. |
| DefaultMetadataKeys | Chiavi metadati | Le chiavi di metadati predefinite della versione 1.4 si trovano nelle chiavi di metadati enum della versione 2.5. |
| AdvertisingFactory | ContentFactory | AdvertisingFactory dalla versione 1.4 è stato rinominato in ContentFactory nella versione 2.5 |
| RilevatoreOpportunitàPosizionamento | OpportunityGenerator | I rilevatori vengono sostituiti con i generatori. |
| mediaPlayer.getView().notificationClick(); | mediaPlayer.notificationClick(); | Il metodo notificationClick() di MediaPlayerView è stato spostato nella classe MediaPlayer. |
| public ABRControlParameters(ABRPolicy abrPolicy, int nInitialBitRate, int nMinBitRate, int nMaxBitRate) | public ABRControlParameters(int nInitialBitRate, int nMinBitRate, int nMaxBitRate, ABRPolicy abrPolicy, int nMinTrickPlayBitRate, int nMaxTrickPlayBitRate, int nMaxTrickPlayBandwidthUsage, double dMaxPlayoutRate) |  |
| playbackInformation.getTimeToFirstFrame() |  | Non disponibile |
|  | playbackInformation.get PerceivedBandwidth() | TVSDK v2.5 QOSProvider ha una nuova proprietà per determinare la larghezza di banda percepita durante una sessione di streaming. |

### Classi rimosse {#removed-classes}

Le seguenti classi vengono rimosse e non hanno equivalenti.

* `TimeRangeCollection`
* `PSDKConfig`
* `BaseLogger`
* `DefaultLogger`
* `Log`
* `Logger`
* `LogFactory`
* `NullLogger`

Le ultime sei di queste classi sono disponibili come classi di utilità nell&#39;implementazione di riferimento.

## Modifiche allo spazio dei nomi {#namespace-changes}

L’API TVSDK 2.5 consolida gli spazi dei nomi.

Tutti i nomi delle classi nell’API TVSDK 2.5 iniziano con il prefisso com.adobe.mediacore. Alcuni nomi di classi nell’API TVSDK 1.4 iniziano con com.adobe.ave. Le corrispondenti classi 2.5 cambiano com.adobe.ave in com.adobe.mediacore. Ad esempio., si noti la modifica nelle seguenti righe di codice per 1.4 e 2.5:

```java
// TVSDK 1.4
import com.adobe.ave.drm.DRMAcquireLicenseSettings; import com.adobe.ave.drm.DRMLicense;
import com.adobe.ave.drm.DRMManager; import com.adobe.ave.drm.DRMMetadata
```

```java
// TVSDK 2.5
import com.adobe.mediacore.drm.DRMAcquireLicenseSettings; import com.adobe.mediacore.drm.DRMLicense;
import com.adobe.mediacore.drm.DRMManager; import com.adobe.mediacore.drm.DRMMetadata;
```

## Modifiche nella gestione degli eventi {#changes-in-event-handling}

Per registrare gli eventi in questa versione, passa il gestore a `addEventListener`. L’elenco degli eventi è stato sostanzialmente modificato dalla versione 1.4 alla versione 2.5.\
Ad esempio, ecco come registrare un gestore eventi per `MediaPlayerEvent.STATUS_CHANGED:`

```java
mPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED,
new StatusChangeEventListener() {
@Override
public void onStatusChanged(MediaPlayerStatusChangeEvent event) {
//Handle status change event
}
});
```

L’evento è stato registrato in 1.4 in questo modo:

```java
mPlayer.addEventListener(MediaPlayer.Event.PLAYBACK, new MediaPlayer.PlaybackEventListener() {
@Override
public void onStateChanged(MediaPlayer.PlayerState state,
MediaPlayerNotification notification) {
//Handle status change event
}
// Additional handlers
...
});
```

L&#39;enum MediaPlayerEvent contiene tutti i codici evento. I seguenti codici evento della versione 1.4 non esistono più nella versione 2.5:

* `ADBREAK_PLACEMENT_COMPLETED`
* `ADBREAK_PLACEMENT_FAILED`
* `ADBREAK_REMOVAL_COMPLETED`
* `AD_BREAK_MANIFEST_LOAD_COMPLETE`
* `AD_MANIFEST_LOAD_COMPLETE`
* `AD_MANIFEST_LOAD_FAILED`
* `AUDIO_TRACK_FAILED`
* `BACKGROUND_MANIFEST_FAILED`
* `BUFFERING_FULL, CUSTOM_AD_EVENT`
* `CONTENT_MARKER`
* `CONTENT_PLACEMENT_COMPLETE`
* `CONTENT_CHANGED`
* `ITEM_REPLACED`
* `ITEM_READY`
* `VIEW_CLICKED`
* `PREPARED`
* `UPDATED`
* `OPPORTUNITY_COMPLETED`
* `OPPORTUNITY_CREATED`
* `OPPORTUNITY_FAILED`
* `PAUSE_AT_PERIOD_END`
* `PLAYBACK_STARTED`
* `PLAYBACK_PAUSED`
* `PLAYBACK_COMPLETED`
* `PLAY_COMPLETE`
* `POST_ROLL_COMPLETE`
* `RESOURCE_LOADED`
* `TIMED_METADATA_SKIPPED`
* `VIDEO_ERROR`
* `VIDEO_STATE_CHANGED`

I seguenti codici evento sono nuovi in 2.5:

* `AD_RESOLUTION_COMPLETE`
* `BUFFER_PREPARED`
* `CAPTIONS_UPDATED`
* `MANIFEST_UPDATED`
* `PLAYBACK_RANGE_UPDATED`
* `RESERVATION_REACHED`
* `TIME_CHANGED`
* `TIMED_EVENT`
* `TIMED_METADATA_ADDED_IN_BACKGROUND`

### Eventi rinominati {#renamed-events}

| Nuovo nome | Nome precedente |
|--- |--- |
| SEEK_BEGIN | SEEK_STARTED |
| SEEK_END | SEEK_COMPLETED |
| SEEK_POSITION_ADJUSTED | SEEK_ADJUST_COMPLETED |
| INIZIO_BUFFERING | BUFFERING_STARTED |
| BUFFERING_END | BUFFERING_COMPLETED |
| AUDIO_TRACK_UPDATED | AUDIO_TRACK_CHANGED |
| STATO_MODIFICATO | STATO_MODIFICATO |
| TIMED_METADATA_AVAILABLE | TIMED_METADATA_ADDED |
| SIZE_AVAILABLE | SIZE_CHANGED |
| LOAD_INFO | LOAD_INFORMATION_AVAILABLE |

## Modifiche a MediaPlayer {#mediaplayer-changes}

Un nuovo modo di costruire `MediaPlayer` e modifiche ad alcuni metodi.

**Modifiche alla classe MediaPlayer**

Ecco le modifiche apportate a `MediaPlayer` classe:

* Il `MediaPlayerStatus` enum sostituisce `MediaPlayer.PlayerState`. Ad esempio:

```java
//TVSDK v1.4
mPlayer. addEventListener(MediaPlayer.Event.PLAYBACK, new MediaPlayer.PlaybackEventListener() {

@Override
public void onStateChanged(MediaPlayer.PlayerState state,MediaPlayerNotification notification) {
//Handle status change event
}
// Additional handlers
...
});

//TVSDK v2.5
mPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED, new StatusChangeEventListener() {
@Override
public void onStatusChanged(MediaPlayerStatusChangeEvent event) {
//Handle status change event
}
//Additional handlers.
...
});
```

* Il `MediaPlayer.seekToLocalTime()` il metodo ora è chiamato `MediaPlayer.seekToLocal`. Ad esempio:

```java
//TVSDK v1.4
public void seekToLocal(long localPosition) { mediaPlayer.seekToLocalTime(localPosition);
}

//TVSDK v2.5
public void seekToLocal(long localPosition) { mediaPlayer.seekToLocal(localPosition);
}
```

* Il `MediaPlayerView.notifyClick()` il metodo è ora `MediaPlayer.notifyClick()`. Ad esempio:

```java
//TVSDK v1.4
public void adClick() { mediaPlayer.getView().notifyClick();
}

//TVSDK v2.5
public void adClick() { mediaPlayer.notifyClick();
}
```

* Il primo `MediaPlayer.MediaPlayer.getNotificationHistory()` il metodo ora non è più disponibile e non viene sostituito.
* Il primo `MediaPlayer.replaceCurrentItem()` è suddiviso in due metodi: `replaceCurrentResource()`, che accetta un&#39;istanza di `MediaResource`, e `replaceCurrentItem()`, che accetta un&#39;istanza di `MediaPlayerItem`. Ad esempio:

```java
//TVSDK v1.4
MediaResource playerResource = MediaResource.createFromUrl(url, getAdvertisingMetadata());

mediaPlayer.replaceCurrentItem(playerResource);

//TVSDK v2.5 - replacing a resource
MediaResource playerResource = new MediaResource(url,
MediaResource.Type.HLS, getAdvertisingMetadata());
...
try {
mMediaPlayer.replaceCurrentResource(playerResource, _mediaPlayerItemConfig);
} catch (MediaPlayerException mediaPlayerException) {
// handle exception.
}
// TVSDK 2.5 - replacing an Item
MediaPlayerItemLoader itemLoader = new MediaPlayerItemLoader(context, new MediaPlayerItemLoader.LoaderListener() {

@Override
public void onError(PSDKErrorCode psdkErrorCode, String s) {
...
}
@Override
public void onLoadComplete(MediaPlayerItem mediaPlayerItem) {
...
}
@Override
public void onBufferingBegin() {
...
}
@Override
public void onBufferPrepared() {
...
}
});
MediaResource playerResource = new MediaResource(url,
MediaResource.Type.HLS, getAdvertisingMetadata());

itemLoader.load(playerResource); itemLoader.prepareBuffer();
mediaPlayer.replaceCurrentItem(itemLoader.getItem());
```

È possibile utilizzarlo per passare da un&#39;istanza MediaPlayer preinizializzata all&#39;altra, come nel caso delle sospensioni attività.

**I costruttori sostituiscono i metodi create() statici**

È possibile utilizzare i costruttori in TVSDK v2.5, invece di utilizzare `create()` metodi di TVSDK v1.4. Tutte le classi i cui nomi iniziano con Predefinito, ad esempio `DefaultMediaPlayer`, `DefaultNetworkConfig`, `DefaultContentFactory`, non sono disponibili nella versione v2.5.

In alcuni casi l’API TVSDK v1.4 utilizza il seguente pattern per la creazione delle classi:

1. Definisci un’interfaccia (ad esempio, `MediaPlayer`).
1. Fornisci una classe predefinita (ad esempio, `DefaultMediaPlayer`).
1. Fornisci un `create()` sulla classe predefinita per fornire una classe che implementa l&#39;interfaccia.

In TVSDK v2.5, tali interfacce sono classi concrete e puoi creare istanze di queste classi utilizzando i rispettivi costruttori. I seguenti snippet di codice illustrano questa differenza:

```java
//TVSDK v1.4
// Create a media player
// MediaPlayer is an interface
private MediaPlayer createMediaPlayer() { MediaPlayer mediaPlayer =
DefaultMediaPlayer.create(getActivity().getApplicationContext()); return mediaPlayer;

//TVSDK v2.5
// Create a media player
// MediaPlayer is a class that you instantiate private MediaPlayer createMediaPlayer() {
MediaPlayer mediaPlayer =
new MediaPlayer(getActivity().getApplicationContext()); return mediaPlayer;
}
```

Altre classi che non seguono questo schema ma utilizzano `create()` i metodi di cui al punto 1.4 comprendono:

* MediaResource\
   Precedentemente utilizzato `MediaResource.createFromUrl()`. Ora utilizza il costruttore, che accetta un URL, un tipo di risorsa e metadati. Ad esempio:

```java
//TVSDK v1.4
MediaResource playerResource = MediaResource.createFromUrl(url, getAdvertisingMetadata());
mediaPlayer.replaceCurrentItem(playerResource);

//TVSDK v2.5
MediaResource playerResource =
new MediaResource(url, MediaResource.Type.HLS, getAdvertisingMetadata());

try { mediaPlayer.replaceCurrentResource(playerResource,_mediaPlayerItemConfig);
} catch (MediaPlayerException mediaPlayerException) {
// handle exception.
}
```

* Annuncio
* AdAsset
* AdBreak

Alcune classi (ad esempio, `ContentFactory`) sono classi astratte senza implementazione predefinita disponibile pubblicamente (ad esempio, `DefaultContentFactory`). In questi casi puoi fornire un’implementazione predefinita tramite una funzione di convenienza, ad esempio: `mediaPlayerItemConfig.getDefaultContentFactory()`

**Modifiche ai sottotitoli**

Le seguenti modifiche interessano le classi relative ai sottotitoli:

* Quando si recuperano tracce di sottotitoli codificati, `MediaPlayerItem.getClosedCaptionTracks()` restituisce solo i brani attivi.
* `ClosedCaptionTrack` non ha più un `isActive()` metodo.

```java
//TVSDK v1.4
public List<String> getClosedCaptionTracks(String label) {
List<String> closedCaptionsTracksAsStrings = new ArrayList<String>(); MediaPlayerItem currentItem = mediaPlayer.getCurrentItem(); List<ClosedCaptionsTrack> closedCaptionsTracks =
currentItem.getClosedCaptionsTracks(); Iterator<ClosedCaptionsTrack> iterator =
closedCaptionsTracks.iterator();
if (currentItem != null) {
while (iterator.hasNext()) {
ClosedCaptionsTrack closedCaptionsTrack = iterator.next(); String isActive = closedCaptionsTrack.isActive() ? " (" + label
+ ")" : "";
closedCaptionsTracksAsStrings.add(closedCaptionsTrack.getName()
+ " : " + closedCaptionsTrack.getLanguage() + isActive);
}
}
return closedCaptionsTracksAsStrings;
}

//TVSDK v2.5
public List<String> getClosedCaptionTracks(String label) {

MediaPlayerItem currentItem = mediaPlayer.getCurrentItem(); List<ClosedCaptionsTrack> closedCaptionsTracks =
currentItem.getClosedCaptionsTracks();
Iterator<ClosedCaptionsTrack> iterator = closedCaptionsTracks.iterator();

List<String> closedCaptionsTracksAsStrings = new ArrayList<String>(); if (currentItem != null) {
while (iterator.hasNext()) {
ClosedCaptionsTrack closedCaptionsTrack = iterator.next(); closedCaptionsTracksAsStrings.
add(closedCaptionsTrack.getName() + " : ");
}
}
return closedCaptionsTracksAsStrings;
}
// Add snippet and desc for CaptionsUpdatedEventListener mediaPlayer.addEventListener(MediaPlayerEvent.CAPTIONS_UPDATED,
captionsUpdatedEventListener);

private final CaptionsUpdatedEventListener captionsUpdatedEventListener = new CaptionsUpdatedEventListener() {

@Override
public void onCaptionsUpdated(MediaPlayerItemEvent mediaPlayerItemEvent) { getActivity().findViewById(R.id.sbPlayerControlCC).setVisibility(
View.VISIBLE/*Visible*/);
}
};
```

## Modifiche pubblicitarie {#advertising-changes}

Nella versione 2.5 sono presenti diverse modifiche relative agli annunci.

**Modifiche al comportamento pubblicitario**

Il comportamento predefinito della riproduzione dell’annuncio quando un utente esegue una ricerca oltre un pod dell’annuncio cambia leggermente nella versione v2.5. Se l’interruzione pubblicitaria non viene guardata, l’annuncio viene riprodotto dopo una ricerca in avanti. Quando l’app utilizza i criteri di annuncio predefiniti, l’interruzione pubblicitaria viene rimossa al termine della riproduzione. Utilizzando TVSDK v2.5, se un utente cerca dietro un Ad pod sulla timeline e l’interruzione pubblicitaria non viene guardata, non viene riprodotto alcun annuncio.

Tuttavia, in TVSDK v1.4, per impostazione predefinita, un annuncio viene riprodotto in caso di ricerca all’indietro. Ad esempio, se esegui una ricerca all’indietro tra la terza e la quarta interruzione pubblicitaria, il comportamento predefinito per TVSDK v1.4 consiste nell’riprodurre la terza interruzione pubblicitaria.

**Modifica delle regole dell’annuncio**

Le regole dell’annuncio vengono specificate utilizzando un file JSON. Il formato del file JSON rimane lo stesso in entrambe le versioni di TVSDK. Tuttavia, in TVSDK v2.5, il file JSON delle regole dell’annuncio deve essere ospitato in una posizione accessibile tramite un URL HTTP. L&#39;applicazione può utilizzare un&#39;istanza di AuditudeSettings.

```java
//TVSDK v2.5
AuditudeSettings result = new AuditudeSettings(); result.setCRSRulesJsonURL(<http url of AdobeTVSDKConfig.json>);
```

Nella versione 1.4 di TVSDK, questo file si trova sotto la cartella delle risorse nell’applicazione e TVSDK carica il file.

**Ridenominazione della Ad Factory**

`AdvertisingFactory` è ora denominato `ContentFactory`. Con `ContentFactory` puoi creare flussi di lavoro pubblicitari personalizzati ignorando alcuni dei loro metodi. Utilizza return null per mantenere i comportamenti predefiniti, come indicato di seguito:

```java
//TVSDK v2.5
new ContentFactory() {
@Override
public AdPolicySelector retrieveAdPolicySelector(MediaPlayerItem item) { return new CustomAdPolicySelector();
}
@Override
public List<OpportunityGenerator> retrieveGenerators(MediaPlayerItem item) { return null;
}
@Override
public List<ContentResolver> retrieveResolvers(MediaPlayerItem item) { return null;
}
@Override
public List<CustomAdHandler> retrieveCustomAdPlaybackHandlers(MediaPlayerItem item) { return null;
}
};
```

**Interruzioni pubblicitarie di lunghezza zero**

TVSDK 2.5 inserisce interruzioni pubblicitarie di lunghezza zero come segnaposto quando advertising server non restituisce annunci.

La lunghezza zero delle interruzioni pubblicitarie può essere determinata rilevando il numero di annunci pari a zero nell’interruzione pubblicitaria utilizzando l’evento onAdBreakStarted e l’applicazione deve gestire tali interruzioni pubblicitarie di conseguenza.

**Modifiche ai metadati**

La classe Metadata fornisce una sostituzione più efficiente per la precedente classe MetadataNode.

* La classe Metadata può memorizzare stringhe, matrici di byte e altri oggetti Metadata:

```java
TVSDK v1.4
public AuditudeSettings createAdvertisementSettings() { Metadata advertisingParams = new MetadataNode();
advertisingParams.setValue("platform", Build.VERSION.RELEASE); advertisingParams.setValue("model", Build.MODEL);
AuditudeSettings adSettings = new AuditudeSettings();
// Set ad domain, zone id and media_id
...

// Set the target paramaters adSettings.setTargetingParameters(advertisingParams);

return adSettings;
}
//TVSDK v2.5
public AuditudeSettings createAdvertisementSettings() { Metadata advertisingParams = new Metadata();
advertisingParams.setValue("platform", Build.VERSION.RELEASE); advertisingParams.setValue("model", Build.MODEL);
AuditudeSettings adSettings = new AuditudeSettings();
// Set ad domain, zone id and media_id
...

// Set the target paramaters adSettings.setTargetingInfo(advertisingParams);

return adSettings;
}
```

* Il `MetadataKeys` enum sostituisce `DefaultMetadataKeys`. Non tutte le chiavi in `DefaultMetadataKeys` sono presenti nella nuova versione.

```java
//TVSDK v1.4
if (this.mediaPlayer != null && this.mediaPlayer.getCurrentItem() != null) { MetadataNode resourceMetadata =
(MetadataNode) this.mediaPlayer.getCurrentItem().getResource().getMetadata();
VideoAnalyticsMetadata vaMetadata = (VideoAnalyticsMetadata)
resourceMetadata.getNode(DefaultMetadataKeys.
VIDEO_ANALYTICS_METADATA_KEY.getValue());
}

//TVSDK v2.5
if (resourceMetadata.containsKey(VideoAnalyticsMetadata.
VIDEO_ANALYTICS_METADATA_KEY)) {
JSONObject vaMetadataObj =
new JSONObject(resourceMetadata.
getValue(VideoAnalyticsMetadata. VIDEO_ANALYTICS_METADATA_KEY));
vaMetadata = parseVideoAnalyticsMetadata(vaMetadataObj);
}

} catch (JSONException e) { e.printStackTrace();
}
```

* I metadati pubblicitari sono ora rappresentati da `AdvertisingMetadata` è una sottoclasse di metadati ed è ora memorizzata in `MediaPlayerItemConfig` anziché `MediaResource`.

```java
//TVSDK v1.4
MetadataNode mediaMetadata = new MetadataNode();

if (stream.live) { mediaMetadata.setNode(DefaultMetadataKeys.AUDITUDE_METADATA_KEY.getValue(),
getAdSettingsForLive());
} else {
mediaMetadata.setNode(DefaultMetadataKeys.AUDITUDE_METADATA_KEY.getValue(), getAdSettingsForVod());
}
MediaResource playerResource = MediaResource.createFromUrl(url, mediaMetadata);

//TVSDK v2.5
MediaPlayerItemConfig mediaItemConfig = new MediaPlayerItemConfig(context);

if (stream.live) {
AuditudeSettings adSettings = getAdSettingsForLive(); adSettings.setLivePreroll(true); mediaItemConfig.setAdvertisingMetadata(adSettings);
} else {
// Set the advertising parameters for VOD. mediaItemConfig.setAdvertisingMetadata(getAuditudeSettingsForVod());
}

// Create advertising metadata node Metadata mediaMetadata = new Metadata();

// Asset Url
MediaResource playerResource =
new MediaResource(url, MediaResource.Type.HLS, mediaMetadata);
try {
mediaPlayer.replaceCurrentResource(playerResource, mItemConfig);
} catch (MediaPlayerException mediaPlayerException) {
//handle exception.
}
```

Metadati di configurazione di rete, in precedenza membri del `MediaResource` classe, è ora rappresentato da `NetworkConfiguration` ed è ora memorizzato in `MediaPlayerItemConfig` anziché `MediaResource`.

```java
//TVSDK v1.4
MediaResource playerResource = MediaResource.createFromUrl(url, mediaMetadata);
...

//TVSDK v2.5
MediaPlayerItemConfig mediaItemConfig = new MediaPlayerItemConfig(context);

NetworkConfiguration mediaNetworkConfiguration = mediaItemConfig.getNetworkConfiguration();
```

**Modifiche all’analisi TimedMetadata**

Analisi di `TimedMetadata` è stato modificato nella versione 2.5 in relazione ai tipi di dati per l’analisi del tag ID3.

```java
//TVSDK v1.4
public void onTimedMetadata(TimedMetadata timedMetadata) { TimedMetadata.Type type = timedMetadata.getType();
if (type.equals(TimedMetadata.Type.ID3)){ PMPDemoApp.logger.i(LOG_TAG + "#onTimedMetadata",
"New ID3 tag detected at time = " + timedMetadata.getTime());
Metadata metadata = timedMetadata.getMetadata(); Set<String> keys = metadata.keySet();
for (String key : keys) {
String value = metadata.getValue(key); PMPDemoApp.logger.i(LOG_TAG + "#onTimedMetadata",
"Key = " + key + " Value = " + value);
}
} else if (_mediaPlayer.getPlaybackRange() != null &&
_mediaPlayer.getPlaybackRange().getDuration() > 0) { displayRanges();
PMPDemoApp.logger.i(LOG_TAG +
"#onTimedMetadata",
"New timed metadata. Name " + timedMetadata.getName() +
", time " + timedMetadata.getTime() + ", id " + timedMetadata.getId() + ", metadata " +
timedMetadata.getMetadata() + ".");
/*if (!_timedMetadataList.contains(timedMetadata)) {
_timedMetadataList.add(timedMetadata);
}*/
/* scte35 */
if (timedMetadata.getName().equalsIgnoreCase("#EXT-OATCLS-SCTE35")) { parseSCTE35Tag(timedMetadata);
}
}
}

//TVSDK v2.5
public void onTimedMetadata(TimedMetadataEvent timedMetadataEvent) { PMPDemoApp.logger.i(LOG_TAG + " inside"," ontimedmetadata"); TimedMetadata timedMetadata = timedMetadataEvent.getTimedMetadata();

TimedMetadata.Type type = timedMetadata.getType(); if (type.equals(TimedMetadata.Type.ID3)) {
PMPDemoApp.logger.i(LOG_TAG +
"#onTimedMetadata",
"New ID3 tag detected at time = " + timedMetadata.getTime());
Metadata metadata = timedMetadata.getMetadata();
if (metadata != null) { PMPDemoApp.logger.i(LOG_TAG +
"::expandID3Metadata", "isEmpty " + metadata.isEmpty());
Set<String> keys = metadata.keySet(); PMPDemoApp.logger.i(LOG_TAG + "::expandID3Metadata",
"No of keys=" + keys.size());
String s;
for (String key : keys) {
byte[] value = metadata.getByteArray(key); s = new String(value);
if (key.equalsIgnoreCase("APIC"))
s = "SUPPRESSING BINARY DATA FOR ATTACHED PICTURE.";
PMPDemoApp.logger.i(LOG_TAG + "::expandID3Metadata",
"Key=" + key + ", Length=" + value.length + ", Value=" + s.trim());
}
}
} else if (_mediaPlayer.getPlaybackRange() != null &&
_mediaPlayer.getPlaybackRange().getDuration() > 0) { displayRanges();
PMPDemoApp.logger.i(LOG_TAG +
"#onTimedMetadata",
"New timed metadata. Name " + timedMetadata.getName() +
", time " + timedMetadata.getTime() + ", id " + timedMetadata.getId() + ", metadata " +
timedMetadata.getMetadata() + ".");
/*if (!_timedMetadataList.contains(timedMetadata)) {
_timedMetadataList.add(timedMetadata);
}*/
/* scte35 */
if (timedMetadata.getName().equalsIgnoreCase("#EXT-OATCLS-SCTE35")) { PMPDemoApp.logger.i(LOG_TAG +
" inside ontimedmetadata"," ext"); parseSCTE35Tag(timedMetadata);
}
}
}
```

**Altre modifiche**

Nella versione 2.5 sono disponibili le seguenti modifiche aggiuntive:

* Il `notifyClick()` il metodo è stato spostato da `MediaPlayerView` a `MediaPlayer`.

* `AdPolicySelector` è un’interfaccia, non una classe. Implementa tutti i relativi metodi.
* `AdPolicyInfo` ora contiene un elenco di `AdBreakTimelineItem`, non `AdBreakPlacement`.

* Nome API di `ContentResolver` la classe astratta è stata modificata.
* `PlacementOpportunityDetector` non è più disponibile. Piuttosto, estendi il `OpportunityGenerator` classe astratta. L’implementazione di riferimento ne è un esempio.

* I parametri della `AdBreakPlacement` costruttrice sono uguali, ma in un ordine diverso. Per un esempio di implementazione, consulta l’implementazione del Lettore di riferimento in bundle con il prodotto.

## Modifiche in DRM {#changes-in-drm}

La maggior parte delle modifiche in questa versione si trovano nel livello DRM. La tabella seguente mostra ulteriori modifiche tra le versioni 1.4 e 2.5:

| DRMManager, metodo | Callback riuscito in 1.4 | Errore di callback in 1.4 | Listener in 2.5 |
|--- |--- |--- |--- |
| acquisitionLicense | DRMLicenseAcquiredCallback | DRMOperationErrorCallback | DRMAcquireLicenseListener |
| acquisitionPreviewLicense | DRMLicenseAcquiredCallback | DRMOperationErrorCallback | DRMAcquireLicenseListener |
| autenticare | DRMAuthenticationCompleteCallback | DRMOperationErrorCallback | DRMAuthenticateListener |
| createMetadataFromBytes | NA | DRMOperationErrorCallback | DRMErrorListener |
| inizializzare | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |
| joinLicenseDomain | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |
| leaveLicenseDomain | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |
| resetDRM | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |
| returnLicense | DRMLicenseReturnCompleteCallback | DRMOperationErrorCallback | DRMReturnLicenseListener |
| setAuthenticationToken | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |
| storeLicenseBytes | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |

```java
//TVSDK 1.4
private final MediaPlayer.DRMEventListener _drmEventListener = new MediaPlayer.DRMEventListener() {

@Override
public void onDRMMetadata(final DRMMetadataInfo drmMetadataInfo) { PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.DRMEventListener#onDRMMetadata",
"DRM metadata available: " + drmMetadataInfo + ".");
if (getSuppressAutoPlayPreference() && drmMetadataInfo != null) {
// if suppress play setting, then the user is a tester who
// wishes to manually intervene between the metadata available
// event and the play event, so launch the metadata interface
// and give it the loaded metadata bytes, but only once
_drmMetadata = drmMetadataInfo.getDRMMetadata();
}
if (drmMetadataInfo == null ||
!DRMHelper.isAuthNeeded(drmMetadataInfo.getDRMMetadata())) { PMPDemoApp.logger.i(LOG_TAG + "#onDRMMetadata", "DRM auth is not needed."); return;
}
// Perform DRM auth.
// Possible logic might take into consideration a threshold
// between the current player time and the DRM metadata start
// time. For the time being, we resolve it as soon as we receive
// the DRM metadata.

DRMManager drmManager = _mediaPlayer.getDRMManager(); if (drmManager == null) {
PMPDemoApp.logger.e(LOG_TAG + "#onDRMMetadata", "DRMManager is null."); return;
}
SharedPreferences sharedPreferences =
PreferenceManager.getDefaultSharedPreferences(getActivity()); String authUser =
sharedPreferences.getString(PMPDemoApp.SETTINGS_DRM_USERNAME,
getResources().getString(R.string.drmUsername));
String authPass = sharedPreferences.getString(PMPDemoApp.SETTINGS_DRM_PASSWORD,
getResources().getString(R.string.drmPassword));
DRMHelper.performDrmAuthentication(drmManager,
drmMetadataInfo.getDRMMetadata(), authUser,
authPass,
new DRMAuthenticationListener() {
@Override
public void onAuthenticationStart() { PMPDemoApp.logger.i(LOG_TAG + "#onAuthenticationStart",
"DRM authentication started for DRM metadata at [" + drmMetadataInfo.getPrefetchTimestamp() + "].");
}
@Override
public void onAuthenticationError(long majorCode,
long minorCode, Exception e) {
if (getActivity() == null) { return;
}
PMPDemoApp.logger.e(LOG_TAG +
"#onAuthenticationError",
"DRM authentication failed. " + majorCode + " 0x" + Long.toHexString(minorCode));
_handler.post(new Runnable() {
@Override
public void run() { showToast(getString(R.string.drmAuthenticationError)); getActivity().finish();
}
});
}
@Override
public void onAuthenticationComplete(byte[] authenticationToken) { PMPDemoApp.logger.i(LOG_TAG +
"#onAuthenticationComplete",
"Auth successful for DRM metadata at [" + drmMetadataInfo.getPrefetchTimestamp() + "].");
}
});
}
};

//TVSDK 2.5
private final DRMMetadataInfoEventListener drmMetadataInfoEventListener = new DRMMetadataInfoEventListener() {
@Override
public void onDRMMetadataInfo(DRMMetadataInfoEvent drmMetadataInfoEvent) { final DRMMetadataInfo drmMetadataInfo =
drmMetadataInfoEvent.getDRMMetadataInfo();
PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.DRMEventListener#onDRMMetadata",
"DRM metadata available: " + drmMetadataInfo + ".");
if (getSuppressAutoPlayPreference() && drmMetadataInfo != null) {
// if suppress play setting, then the user is a tester who
// wishes to manually intervene between the metadata
// available event and the play event, so launch the
// metadata interface and give it the loaded metadata
// bytes, but only once
drmMetadata = drmMetadataInfo.getDRMMetadata();
}
if (drmMetadataInfo ==
null || !DRMHelper.isAuthNeeded(drmMetadataInfo.getDRMMetadata())) { PMPDemoApp.logger.i(LOG_TAG +
"#onDRMMetadata",
"DRM auth is not needed.");
return;
}
// Perform DRM auth.
// Possible logic might take into consideration a threshold between
// the current player time and the DRM metadata start time. For the
// time being, we resolve it as soon as we receive the DRM metadata.

DRMManager drmManager = _mediaPlayer.getDRMManager(); if (drmManager == null) {
PMPDemoApp.logger.e(LOG_TAG +
"#onDRMMetadata", "DRMManager is null.");
return;
}

SharedPreferences sharedPreferences = PreferenceManager.getDefaultSharedPreferences(getActivity());
String authUser = sharedPreferences.getString(PMPDemoApp.SETTINGS_DRM_USERNAME,
getResources().getString(R.string.drmUsername));
String authPass = sharedPreferences.getString(PMPDemoApp.SETTINGS_DRM_PASSWORD,
getResources().getString(R.string.drmPassword));
DRMHelper.performDrmAuthentication(drmManager,
drmMetadataInfo.getDRMMetadata(), authUser,
authPass,
new DRMAuthenticationListener() {
@Override
public void onAuthenticationStart() { PMPDemoApp.logger.i(LOG_TAG +
"#onAuthenticationStart",
"DRM authentication started for DRM metadata at [" + drmMetadataInfo.getPrefetchTimestamp() + "].");
}
@Override
public void onAuthenticationError(int major,
int minor,
String erroString, String serverErrorURL) {
if (getActivity() == null) { return;
}
PMPDemoApp.logger.e(LOG_TAG +
"#onAuthenticationError",
"DRM authentication failed. " + major +
" 0x" +
Long.toHexString(minor));
_handler.post(new Runnable() {
@Override
public void run() { showToast(getString(R.string.drmAuthenticationError)); getActivity().finish();
}
});
}
@Override
public void onAuthenticationComplete(byte[] authenticationToken) { PMPDemoApp.logger.i(LOG_TAG +
"#onAuthenticationComplete",
"Auth successful for DRM metadata at [" + drmMetadataInfo.getPrefetchTimestamp() + "].");
}
});
}
};
```

Statico `DRMManager` l&#39;istanza disponibile nella versione 1.4 dopo la creazione di mediaplayer è ora disponibile dopo `onDRMMetadataInfo` listener di eventi attivato.

## Modifiche correlate al bitrate adattivo (ABR) {#adaptive-bitrate-abr-related-changes}

**Modifiche nelle costanti**

Molte costanti hanno cambiato tipo da `String` a `int`. Ad esempio: `MediaResourceType`, `ABRControlParameters`, e `MediaPlayerStatusChangeEvent`.

```java
//TVSDK v1.4
ABRControlParameters
private void setAbrControlParams() { SharedPreferences sharedPreferences =
PreferenceManager.getDefaultSharedPreferences(getActivity());
if (sharedPreferences.getBoolean(PMPDemoApp.SETTINGS_ABR_CTRL_ENABLED,
PMPDemoApp.DEFAULT_ABR_ENABLED)) {
int initialBitRate = getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_INITIAL_BITRATE, 0);
int minBitRate = getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MIN_BITRATE, 0);
int maxBitRate = getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MAX_BITRATE, PMPDemoApp.DEFAULT_MAX_BIT_RATE);
int mbrPolicyAsInt =
getIntPreference(sharedPreferences, PMPDemoApp.SETTINGS_ABR_POLICY, 0); ABRControlParameters.ABRPolicy abrPolicy = policyFromInt(mbrPolicyAsInt); abrPolicy = abrPolicy != null ?
abrPolicy : ABRControlParameters.ABRPolicy.ABR_MODERATE;
_mediaPlayer.setABRControlParameters(new ABRControlParameters(initialBitRate,
minBitRate, maxBitRate, abrPolicy));
}
}

//TVSDK v2.5
ABRControlParameters
private void setAbrControlParams() { ABRControlParametersBuilder abrBuilder =
new ABRControlParametersBuilder();

if (sharedPreferences.getBoolean(PMPDemoApp.SETTINGS_ABR_CTRL_ENABLED, PMPDemoApp.DEFAULT_ABR_ENABLED)) {

abrBuilder.setInitialBitRate(getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_INITIAL_BITRATE,
ABRControlParameters.DEFAULT_ABR_INITIAL_BITRATE)); abrBuilder.setMinBitRate(getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MIN_BITRATE,
ABRControlParameters.DEFAULT_ABR_MIN_BITRATE)); abrBuilder.setMaxBitRate(getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MAX_BITRATE,
ABRControlParameters.DEFAULT_ABR_MAX_BITRATE)); abrBuilder.setMaxPlayoutRate(getDoublePreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MAX_PLAYOUT_RATE,
ABRControlParameters.DEFAULT_MAX_PLAYOUT_RATE)); abrBuilder.setMinTrickPlayBitRate(getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MIN_TRICKPLAY_BITRATE,
ABRControlParameters.DEFAULT_ABR_MIN_BITRATE)); abrBuilder.setMaxTrickPlayBitRate(getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MAX_TRICKPLAY_BITRATE,
ABRControlParameters.DEFAULT_ABR_MAX_BITRATE)); abrBuilder.setMaxTrickPlayBandwidthUsage(getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MAX_TRICKPLAY_BANDWIDTH,
ABRControlParameters.DEFAULT_ABR_MAX_BITRATE));

switch (getIntPreference(sharedPreferences, PMPDemoApp.SETTINGS_ABR_POLICY, -1)) {
case 0: abrBuilder.setPolicy(ABRControlParameters.ABRPolicy.ABR_CONSERVATIVE); break;
case 1: abrBuilder.setPolicy(ABRControlParameters.ABRPolicy.ABR_MODERATE); break;
case 2: abrBuilder.setPolicy(ABRControlParameters.ABRPolicy.ABR_AGGRESSIVE); break;
default: abrBuilder.setPolicy(ABRControlParameters.DEFAULT_ABR_POLICY);
}
}
_mediaPlayer.setABRControlParameters(abrBuilder.toABRControlParameters());
}
```

**Modifiche al costruttore ABRControlParameters**

Sono stati aggiunti alcuni parametri, alcuni rinominati e altri spostati. Di seguito sono riportate la firma del costruttore nella versione v1.4 e la nuova firma nella versione 2.5:

```java
//TVSDK v1.4
public ABRControlParameters(ABRPolicy abrPolicy,
int nInitialBitRate, int nMinBitRate,
int nMaxBitRate)

//TVSDK v2.5
public ABRControlParameters(int nInitialBitRate,
int nMinBitRate, int nMaxBitRate,
ABRPolicy abrPolicy,
int nMinTrickPlayBitRate, int nMaxTrickPlayBitRate,
int nMaxTrickPlayBandwidthUsage, double dMaxPlayoutRate)
```

## Eventi di errore e gestione {#error-events-and-handling}

**Modifiche nella gestione degli errori**

Il `MediaError` la classe è stata sostituita con la `Notification` classe. L&#39;unica differenza tra le classi `MediaError` e `Notification` è che quest’ultimo non contiene un attributo description. I codici di errore TVSDK 1.4 con valori 101xxx, 102xxx,104xxx,106xxx,107xxx,109xxx non esistono in TVSDK 2.5. Per i codici di riproduzione in TVSDK 2.5, vedi [Errore nativo - valori di riproduzione video](assets/psdk_android_2.5.pdf).

Di seguito sono riportati alcuni esempi di gestione degli errori in TVSDK 1.4 e 2.5:

```java
//TVSDK v1.4
@Override
public void onStateChanged(MediaPlayer.PlayerState state, MediaPlayerNotification notification) {
PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.PlayerStateEventListener#onStateChanged()", "Player state changed to [" + state
+ "].");

switch (state) {
// Non recoverable state - either reset player and reinitialize
// or release the player and create a new one.
case ERROR: PMPDemoApp.logger.e(LOG_TAG +
"::MediaPlayer.PlayerStateEventListener#onStateChanged()", "Error: " + notification + "."); getActivity().finish();
break;
default:
// do nothing
}
}

//TVSDK v2.5
private final StatusChangeEventListener statusChangeEventListener = new StatusChangeEventListener() {
@Override
public void onStatusChanged(MediaPlayerStatusChangeEvent mediaPlayerStatusChangeEvent)
{
MediaPlayerStatus state = mediaPlayerStatusChangeEvent.getStatus(); PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.PlayerStateEventListener#onStateChanged()", "Player state changed to [" + state
+ "].");
switch (state) {
// Non recoverable state - either reset player and reinitialize
// or release the player and create a new one.
case ERROR:
PMPDemoApp.logger.e(LOG_TAG + "::MediaPlayer.PlayerStateEventListener#onStateChanged()", "Error: ");
printErrorMetadata(mediaPlayerStatusChangeEvent.getMetadata()); showToast("MediaPlayer status ERROR: Look at the logs for details"); getActivity().finish();
break;
default:
// do nothing
}
}
};
```

Tutti gli errori recuperabili vengono trattati come avvisi e vengono gestiti utilizzando `NotificationEventListener` in TVSDK 2.5. Gli avvisi vengono visualizzati come notifiche con `onOperationFailed` Listener nel gestore QOS in TVSDK 1.4, dove come in TVSDK 2.5 la notifica è un evento separato. L’avvertenza di cui ai punti 1.4 e 2.5 è la seguente:

```java
//TVSDK v1.4
private final MediaPlayer.QOSEventListener _qosEventListener = new MediaPlayer.QOSEventListener()
{
@Override
public void onBufferStart() {
PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.QOSEventListener#onBufferStart()", "Buffering started.");
}
@Override
public void onBufferComplete() {
PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.QOSEventListener#onBufferComplete()", "Buffering complete.");
}
@Override
public void onSeekStart() {
PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.QOSEventListener#onSeekStart()", "Seek starting.");
}
@Override
public void onSeekComplete(long adjustedTime) {
PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.QOSEventListener#onSeekComplete()", "Seek complete at position: " + adjustedTime + ".");
}
@Override
public void onLoadInfo(LoadInfo loadInfo) {
PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.QOSEventListener#onLoadInfo()", "Url: " + loadInfo.getUrl() + ", size: "
+ loadInfo.getSize() + " bytes, media duration: " + loadInfo.getMediaDuration() + "ms, download duration: " + loadInfo.getDownloadDuration() + "ms");
}
@Override
public void onOperationFailed(MediaPlayerNotification.Warning warning) {

StringBuffer sb = new StringBuffer("Player operation failed: "); sb.append(warning.getCode()).append(" - ").append(warning.getDescription()); if (warning.getMetadata() != null) {
sb.append("Warning metadata: ").append(warning.getMetadata().toString());
}

MediaPlayerNotification innerNotification = warning.getInnerNotification(); registerFailedAudioTrackIndex(innerNotification); handleFailedSeekEvent(innerNotification);

while (innerNotification != null) { sb.append("Inner notification: ");
sb.append(innerNotification.getCode()).append(" - ").append(innerNotification.getDescription());
Metadata metadata = innerNotification.getMetadata(); if (metadata != null) {
for (String key : metadata.keySet()) { sb.append(" - ").append

//TVSDK v2.5
private final NotificationEventListener notificationEventListener = new NotificationEventListener() {
/**
* An example of dumping the information within a Notification. Here, we don't handle the event in
* any way except to print a log message.
* @param event The NotificationEvent
*/
@Override
public void onNotification(NotificationEvent event) { Notification notification = event.getNotification(); Notification.Type type = notification.getType(); StringBuilder sb = new StringBuilder(); sb.append("[").append(type).append("]");
sb.append(" Player operation failed (").append(notification.getCode()).append(")"); Metadata metadata = notification.getMetadata();
if (metadata != null)
{
for (String key : metadata.keySet())
{
sb.append(", ").append(key).append(" = ").append(metadata.getValue(key));
}
}
Notification inner = notification.getInnerNotification(); if (inner != null) {
sb.append(" :: Inner Notification [").append(inner.getType()).append("](").append(inner.getCode()).append(")");
Metadata innerMetadata = inner.getMetadata(); if (innerMetadata != null) {
for (String iKey : innerMetadata.keySet()) { sb.append(", ").append(iKey).append(" =
").append(innerMetadata.getValue(iKey));
}
}
}
switch(type)
{
case ERROR:
PMPDemoApp.logger.e(LOG_TAG, sb.toString()); break;
case WARNING:
PMPDemoApp.logger.w(LOG_TAG, sb.toString()); break;
default:
PMPDemoApp.logger.i(LOG_TAG, sb.toString()); break;
}
showToast(sb.toString()); PMPDemoApp.logger.d(LOG_TAG, sb.toString());
}
};
```

**Nuove eccezioni**

Mentre TVSDK v1.4 utilizzava una combinazione di valori Null, restituiva errori e una serie di eccezioni ( `MediaPlayerException`, `IllegalStateException`, e `IllegalArgumentException`), TVSDK v2.5 `generatesMediaPlayerException` per tutti gli errori.

>[!NOTE]
>
>Per ottenere dettagli su un’eccezione MediaPlayerException, puoi utilizzare `getErrorCode()`.

Di seguito è riportato un esempio di modifica:

```java
//TVSDK v1.4
public void setBufferControlParams() { try {
mediaPlayer.setBufferControlParameters(getBufferParamsFromSettings());
} catch (IllegalArgumentException e) { PrimetimeReference.logger.w(LOG_TAG +
"#setBufferControlParams",
"Unable to apply buffering params: " + e.getMessage() + ".");
}
}

//TVSDK v2.5
public void setBufferControlParams() { try {
mediaPlayer.setBufferControlParameters(getBufferParamsFromSettings());
} catch (MediaPlayerException e) { PrimetimeReference.logger.w(LOG_TAG + "#setBufferControlParams", "Unable to apply buffering params: " + e.getMessage() + ".");
}
}
```

## Modifiche ai parametri QOS {#changes-to-qos-parameters}

Sono presenti modifiche minori alle proprietà dell&#39;oggetto QOSProvider:

* Il `TimeToFirstFrame` non è disponibile in TVSDK 2.5.
* TVSDK 2.5 QOSProvider ha una nuova proprietà per determinare la larghezza di banda percepita durante una sessione di streaming.

```java
//TVSDK v1.4
public void updateQosInformation(PlaybackInformation playbackInformation) { if (playbackInformation == null) {
return;
}
setQosItem("Frame rate", (int) playbackInformation.getFrameRate() +
" (" + (int) playbackInformation.getDroppedFrameCount() + " dropped)"); setQosItem("Bitrate", (int) playbackInformation.getBitrate()); setQosItem("Buffering time", (long) playbackInformation.getBufferingTime()); setQosItem("Buffer length", (long) playbackInformation.getBufferLength()); setQosItem("Buffer time", (long) playbackInformation.getBufferTime()); setQosItem("Empty buffer count", (int) playbackInformation.getEmptyBufferCount()); setQosItem("Time to load", (int) playbackInformation.getTimeToLoad()); setQosItem("Time to start", (int) playbackInformation.getTimeToStart()); setQosItem("Time to first frame", (int) playbackInformation.getTimeToFirstFrame()); setQosItem("Time to prepare", (int) playbackInformation.getTimeToPrepare()); setQosItem("Last seek time", (int) playbackInformation.getLastSeekTime());
}

//TVSDK v2.5
public void updateQosInformation(PlaybackInformation playbackInformation) { if (playbackInformation == null) {
return;
}
setQosItem("Frame rate", (int) playbackInformation.getFrameRate() +
" (" + (int) playbackInformation.getDroppedFrameCount() + " dropped)"); setQosItem("Bitrate", (int) playbackInformation.getBitRate()); setQosItem("Buffering time", (long) playbackInformation.getBufferingTime()); setQosItem("Buffer length", (long) playbackInformation.getBufferLength()); setQosItem("Buffer time", (long) playbackInformation.getBufferTime()); setQosItem("Empty buffer count", (int) playbackInformation.getEmptyBufferCount()); setQosItem("Time to load", (int) playbackInformation.getTimeToLoad()); setQosItem("Time to start", (int) playbackInformation.getTimeToStart());
setQosItem("Time to prepare", (int) playbackInformation.getTimeToPrepare());
setQosItem("Perceived Bandwidth", (int) playbackInformation.getPerceivedBandwidth());
```

* Il `QOSEventListener::onOperationFailed()` non esiste più in TVSDK 2.5. Le avvertenze che prima venivano visualizzate in questo listener di eventi ora vengono visualizzate nel `NotificationEventListener::onNotification()` listener di eventi.

* Il `QOSProvider event listeners onBufferStart()`, `onBufferComplete()`, `onSeekStart()`, `onSeekComplete()`, e `onLoadInfo()` sono singoli listener di eventi associati a un’istanza mediaPlayer.

```java
//TVSDK v1.4
private final MediaPlayer.QOSEventListener _qosEventListener = new MediaPlayer.QOSEventListener() {

@Override
public void onBufferStart() { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onBufferStart()", "Buffering started.");
showBufferingSpinner();
}
@Override
public void onBufferComplete() { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onBufferComplete()", "Buffering complete.");
hideBufferingSpinner();
}
@Override
public void onSeekStart() { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onSeekStart()", "Seek starting.");
inTrickPlayMode = false;
}
@Override
public void onSeekComplete(long adjustedTime) { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onSeekComplete()", "Seek complete at position: " +
adjustedTime + ".");
_controlBar.setPosition(adjustedTime);
if (adjustedTime == _mediaPlayer.getPlaybackRange().getEnd() &&
_mediaPlayer.getStatus() == MediaPlayer.PlayerState.COMPLETE) {
// Show the replay button. showReplayButton();
}
if (_mediaPlayer.getStatus() == MediaPlayer.PlayerState.PAUSED) {
// Show the pause icon.
_controlBar.pause();
}
}
@Override
public void onLoadInfo(LoadInfo loadInfo) { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onLoadInfo()", "Url: " +
loadInfo.getUrl() + ", size: " + loadInfo.getSize() +
" bytes, media duration: " +
loadInfo.getMediaDuration() + "ms, download duration: " +
loadInfo.getDownloadDuration() + "ms");
 
public void onOperationFailed(MediaPlayerNotification.Warning warning) {

StringBuffer sb = new StringBuffer("Player operation failed: "); sb.append(warning.getCode()).append(" - ").append(warning.getDescription()); if (warning.getMetadata() != null) {
sb.append("Warning metadata: ").append(warning.getMetadata().toString());
}

MediaPlayerNotification innerNotification = warning.getInnerNotification(); registerFailedAudioTrackIndex(innerNotification); handleFailedSeekEvent(innerNotification);

while (innerNotification != null) { sb.append("Inner notification: ");
sb.append(innerNotification.getCode()).append(" - "). append(innerNotification.getDescription());
Metadata metadata = innerNotification.getMetadata(); if (metadata != null) {
for (String key : metadata.keySet()) { sb.append(" - ").append(key).append(": ").
append(metadata.getValue(key));
}
}
innerNotification = innerNotification.getInnerNotification();
}
String errMsg = sb.toString(); PMPDemoApp.logger.w(LOG_TAG +
"::MediaPlayer.QOSEventListener#onOperationFailed()", errMsg);
showToast(errMsg);
}
};

//TVSDK v2.5
mediaPlayer.addEventListener(MediaPlayerEvent.LOAD_INFORMATION_AVAILABLE,
loadInfoEventListener); mediaPlayer.addEventListener(MediaPlayerEvent.BUFFERING_BEGIN,
bufferingBeginEventListener); mediaPlayer.addEventListener(MediaPlayerEvent.BUFFERING_END,
bufferingEndEventListener); mediaPlayer.addEventListener(MediaPlayerEvent.SEEK_BEGIN,
seekBeginEventListener); mediaPlayer.addEventListener(MediaPlayerEvent.SEEK_END,
seekEndEventListener);
// Buffering events.
BufferingBeginEventListener bufferingBeginEventListener = new BufferingBeginEventListener() {
@Override
public void onBufferingBegin(BufferEvent bufferEvent) { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onBufferStart()", "Buffering started.");
showBufferingSpinner();
}
};

BufferingEndEventListener bufferingEndEventListener = new BufferingEndEventListener() {
@Override
public void onBufferingEnd(BufferEvent bufferEvent) { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onBufferComplete()",
"Buffering complete."); hideBufferingSpinner();
}
};

BufferPreparedEventListener bufferPreparedEventListener = new BufferPreparedEventListener() {
@Override
public void onBufferPrepared() {
}
};
// seek events.
SeekBeginEventListener seekBeginEventListener = new SeekBeginEventListener() {

@Override
public void onSeekBegin(SeekEvent seekEvent) { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onSeekStart()", "Seek starting.");
inTrickPlayMode = false;
}
};
SeekEndEventListener seekEndEventListener = new SeekEndEventListener() {
@Override
public void onSeekEnd(SeekEvent seekEvent) {
double adjustedTime = seekEvent.getActualPosition();
PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onSeekComplete()", "Seek complete at position: " + adjustedTime + ".");
_controlBar.setPosition((long) adjustedTime);
if (adjustedTime == _mediaPlayer.getPlaybackRange().getEnd() &&
_mediaPlayer.getStatus() == MediaPlayerStatus.COMPLETE) {
// Show the replay button. showReplayButton();
}
if (_mediaPlayer.getStatus() == MediaPlayerStatus.PAUSED) {
// Show the pause icon.
_controlBar.pause();
}
}
};
/**
* LoadInformationEventListener that intercepts PSDK load info events
*/
private final LoadInformationEventListener loadInfoEventListener = new LoadInformationEventListener() {

@Override
public void onLoadInformation(LoadInformationEvent event) { LoadInformation loadInfo = event.getLoadInfomation(); PMPDemoApp.logger.i(
LOG_TAG + "::LoadInformationEventListener#onLoadInfomation()", "Url: " + loadInfo.getUrl() + ", size: "
+ loadInfo.getSize()
+ " bytes, download duration: "
+ loadInfo.getDownloadDuration() + "ms");
}
};
```

## Risorse utili {#helpful-resources}

* Consulta la documentazione completa dell’Aiuto all’indirizzo [Informazioni e supporto per Adobe Primetime](https://helpx.adobe.com/support/primetime.html) pagina.
