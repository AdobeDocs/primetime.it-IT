---
title: TVSDK da 1.4 a 2.5 per Android (Java)
seo-title: TVSDK da 1.4 a 2.5 per Android (Java)
description: TVSDK 2.5 offre diversi vantaggi rispetto alla versione 1.4 in termini di prestazioni, sicurezza, integrazioni migliori e altro ancora.
seo-description: TVSDK 2.5 offre diversi vantaggi rispetto alla versione 1.4 in termini di prestazioni, sicurezza, integrazioni migliori e altro ancora.
uuid: aaab7aec-cb5b-4840-82e8-7112a8d98a8a
contentOwner: vishgupt
products: SG_PRIMETIME
topic-tags: migration
discoiquuid: 8d9136bf-b3ae-450c-bd8a-0bb246527886
translation-type: tm+mt
source-git-commit: e644e8497e118e2d03e72bef727c4ce1455d68d6

---


# TVSDK da 1.4 a 2.5 per Android (Java) {#tvsdk-to-for-android-java}

TVSDK 2.5 offre diversi vantaggi rispetto alla versione 1.4 in termini di prestazioni, sicurezza, integrazioni migliori e altro ancora.

TVSDK risolve le sfide più importanti sul dispositivo che conta di più. Android continua ad essere il dominio globale, con oltre l&#39;86% della quota di mercato. La migrazione a TVSDK su Android ottimizzerà le prestazioni di riproduzione per migliorare il coinvolgimento degli utenti e accelerare il time-to-market con il supporto di nuovi formati di contenuto.

## Vantaggi della migrazione a TVSDK v2.5 {#benefits-of-migrating-to-tvsdk-v}

TVSDK 2.5 offre diversi vantaggi rispetto alla versione 1.4 in termini di prestazioni, sicurezza, integrazioni migliori e altro ancora. Continua a leggere per conoscere rapidamente i vantaggi della migrazione a questa nuova versione.

Secondo uno studio di benchmarking di terze parti, v2.5 offre una riduzione di 5 volte del tempo di avvio e 3,8 volte superiore alla media del settore.

| Caratteristiche delle prestazioni | Descrizione |
|--- |--- |
| Instant On per VOD e Live | Pre-caricamento dei segmenti iniziali per la riproduzione immediata per i flussi VOD e live-lineari durante la commutazione del canale, per un&#39;esperienza simile a quella del televisore. |
| Lazy e caricamento | Avvia la riproduzione non appena è disponibile il pre-roll o il contenuto durante la risoluzione degli annunci mid-roll in un thread parallelo. |
| Connessioni di rete persistenti | Maggiore efficienza e riduzione della latenza del codice di rete per prestazioni di riproduzione più veloci. |
| Logica ABR migliorata | La nuova logica ABR si basa sulla lunghezza del buffer, sulla velocità di modifica della lunghezza del buffer e sulla larghezza di banda misurata. In questo modo, l&#39;ABR sceglie il bit rate corretto quando la larghezza di banda oscilla e ottimizza anche il numero di volte in cui l&#39;interruttore del bitrate avviene effettivamente monitorando la velocità con cui cambia la lunghezza del buffer. |
| Download parziale del segmento | Avvia la riproduzione non appena sono disponibili sufficienti fotogrammi da un segmento per il rendering video in modo affidabile sul lato client. |
| Download paralleli | TVSDK scarica segmenti audio e video in parallelo per contenuti demuxed per ottimizzare le prestazioni di riproduzione. |

Le funzioni di riproduzione migliorano il coinvolgimento dei consumatori fornendo l&#39;esperienza della trasmissione lineare sul digitale. Inoltre, consente di sfruttare il DRM nativo, come Widevine per la riproduzione HD.

| Funzioni di riproduzione | Descrizione |
|--- |--- |
| Riproduzione MP4 | Le clip brevi MP4 non devono essere transcodificate di nuovo per la riproduzione in TVSDK. |
| Riproduzione di contenuti DASH VOD | Sono supportati i casi d’uso di riproduzione DASH VOD di base. |
| Trickplay uniforme con ABR | Supporto per avanzamento rapido e riavvolgimento in HLS utilizzando fotogrammi chiave a basse frequenze e I-Frame a velocità più veloce. Supporto ABR per tutti i frame supportati. |

Le funzioni sono importanti per soddisfare le restrizioni dello studio, come la riproduzione HD su DRM nativo.

| Caratteristiche | Descrizione |
|--- |--- |
| Protezione dell&#39;uscita basata sulla risoluzione | la riproduzione può essere limitata a determinate risoluzioni consentite dai requisiti DRM. Disponibile solo tramite Primetime DRM. |
| Supporto per Widevine | Supportato con flussi DASH VOD per abilitare i casi di utilizzo DRM nativi. |

Il miglioramento della fatturazione diretta elimina la necessità di creare rapporti manuali per la fatturazione ogni mese. VHL 2.0 consente di commercializzare più rapidamente i dati grazie all&#39;integrazione pre-build e a una migliore precisione nel monitoraggio.

| Caratteristiche | Descrizione |
|--- |--- |
| Integrazione con Moat | Supporto per la misurazione della visibilità degli annunci da Moat. |
| VHL 2.0 | L&#39;integrazione della libreria heartbeat video ottimizzata più recente per la raccolta automatica dei dati di utilizzo per Adobe Analytics. |
| Supporto per failover | Strategie aggiuntive implementate per continuare la riproduzione ininterrotta, nonostante gli errori dei server host, dei file playlist e dei segmenti. |
| Integrazione fatturazione diretta | Invia le metriche di fatturazione al back-end di Adobe Analytics, certificato da Adobe Primetime per i flussi utilizzati dal cliente. |

>[!NOTE]
>
>Tutte le funzionalità di TVSDK v1.4 sono supportate nella release v2.5, ad eccezione del supporto per più CDN.

## Panoramica del processo di migrazione {#overview-of-the-migration-process}

La migrazione da TVSDK 1.4 a 2.5 comporta la modifica delle librerie della versione 2.5, la ricompilazione e quindi l&#39;utilizzo di questo documento per risolvere eventuali problemi.

Le librerie TVSDK v1.4 non funzionano con le librerie v2.5 e non coesistono con esse. Devi usare le librerie v2.5 con TVSDK 2.5 e migrare le tue applicazioni e integrazioni per eseguire l&#39;aggiornamento a TVSDK 2.5. Questo documento descrive come e cosa modificare il codice dell&#39;applicazione e come risolvere gli errori durante la ricompilazione.

Il file psdk.jar utilizza librerie di terze parti per supportare funzioni diverse. Per impedire la rimozione delle librerie, includete quanto segue nel `proguard.cfg` file:

```java
# Adobe TVSDK keep classes
-keep class com.adobe.** { *; }
-keep class com.google.android.exoplayer.**
{ *; }
```

Nel `build.gradle` file, è necessario includere la direttiva di compilazione per includere i file JAR basati su TVSDK. Se la vostra app include Adobe Video Analytics, dovete includere la direttiva di compilazione per gli JAR aggiuntivi richiesti per l&#39;integrazione di Adobe Video Analytics nell&#39;app

```java
# Compile Adobe TVSDK jars compile files('libs/psdk-va.jar')
compile files('libs/VideoHeartbeat.jar')
```

Più modifiche secondarie non sono incluse in questo documento. Per le modifiche minori alle API, fai riferimento a [TVSDK 2.5 per Android Java API](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.5/index.html). Il riferimento API C++ corrispondente ha descrizioni dettagliate. Per la documentazione relativa alle API C++, consultate [TVSDK 2.5 per le API](https://help.adobe.com/en_US/primetime/api/psdk/cpp_2.5/index.html)Android C++.

Numerosi esempi dell’utilizzo dell’API sono trattati nell’implementazione di riferimento distribuita con TVSDK.

## Modifiche API in TVSDK v2.5 {#api-changes-in-tvsdk-v}

Le nuove API obsolete e modificate sono documentate di seguito.

| TVSDK v1.4 | TVSDK v2.5 | Descrizione |
|--- |--- |--- |
| import com.adobe.ave.drm.DRMAcquireLicenseSettings | import com.adobe.mediacore.drm.DRMAcquireLicenseSettings; | Tutti i nomi di classe nell’API TVSDK 2.5 iniziano con il prefisso com.adobe.mediacore. Questo è solo un esempio. |
| MediaPlayerException, IllegalStateException o IllegalArgumentException | MediaPlayerException | In 2.5, le API generano solo MediaPlayerException. |
| MediaPlayer.PlayerState (MediaPlayer.Event.PLAYBACK) | MediaPlayerStatus (MediaPlayerEvent.STATUS_CHANGED) | Nella release v2.5, MediaPlayer.PlayerState è stato rinominato in un enum MediaPlayerStatus separato. |
| DefaultMediaPlayer.create (getActivity().getApplicationContext() | MediaPlayer mediaPlayer = new MediaPlayer(getActivity(). getApplicationContext(); | I metodi statici utilizzati per creare gli oggetti vengono sostituiti dai costruttori pubblici. |
| MediaPlayer.searchToLocalTime() | MediaPlayer.searchToLocal() | Il metodo MediaPlayer.searchToLocalTime() ora è denominato MediaPlayer.searchToLocal(). |
| closedCaptionsTrack.isActive() |  | Non disponibile |
| MetadataNode | Metadati | Nella release v2.5, la classe Metadata sostituisce l&#39;uso della classe v1.4 MetadataNode. |
| DefaultMetadataKeys | MetadataKeys | Le chiavi DefaultMetadataKeys della versione 1.4 sono in metadataKeys enum v2.5. |
| AdvertisingFactory | ContentFactory | AdvertisingFactory da v1.4 è stato rinominato in ContentFactory in v2.5 |
| PlacementOpportunityDetector | OpportunityGenerator | I rilevatori vengono sostituiti con Generatori. |
| mediaPlayer.getView().notificationClick(); | mediaPlayer.notificationClick(); | Il metodo notificationClick() di MediaPlayerView è stato spostato nella classe MediaPlayer. |
| public ABRControlParameters(ABRPolicy abrPolicy, int nInitialBitRate, int nMinBitRate, int nMaxBitRate) | public ABRControlParameters(int nInitialBitRate, int nMinBitRate, int nMaxBitRate, ABRPolicy abrPolicy, int nMinTrickPlayBitRate, int nMaxTrickPlayBitRate, int nMaxTrickPlayBandwidthUsage, doppio dMaxPlayout Rate) |  |
| playInformation.getTimeToFirstFrame() |  | Non disponibile |
|  | playInformation.get PerceededBandwidth() | TVSDK v2.5 QOSProvider dispone di una nuova proprietà per determinare la larghezza di banda percepita durante una sessione di streaming. |

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

## Modifiche dello spazio dei nomi {#namespace-changes}

L’API TVSDK 2.5 consolida gli spazi dei nomi.

Tutti i nomi di classe nell’API TVSDK 2.5 iniziano con il prefisso com.adobe.mediacore. Alcuni nomi di classe nell’API TVSDK 1.4 iniziano con com.adobe.ave. Le classi corrispondenti 2.5 cambiano com.adobe.ave in com.adobe.mediacore. Ad esempio, prendere nota delle modifiche apportate alle seguenti righe di codice per 1.4 e 2.5:

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

Per registrare gli eventi in questa versione, passare il gestore a `addEventListener`. L&#39;elenco degli eventi è stato sostanzialmente modificato dalla versione 1.4 alla versione 2.5.\
Ad esempio, di seguito viene illustrato come registrare un gestore eventi per `MediaPlayerEvent.STATUS_CHANGED:`

```java
mPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED,
new StatusChangeEventListener() {
@Override
public void onStatusChanged(MediaPlayerStatusChangeEvent event) {
//Handle status change event
}
});
```

Questo è il modo in cui l’evento è stato registrato in 1.4:

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

L&#39;enum MediaPlayerEvent contiene tutti i codici evento. I seguenti codici evento dalla versione 1.4 non esistono più in 2.5:

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

I seguenti codici evento sono stati introdotti in 2.5:

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
| BUFFERING_BEGIN | BUFFERING_STARTED |
| BUFFERING_END | BUFFERING_COMPLETED |
| AUDIO_TRACK_UPDATED | AUDIO_TRACK_CHANGED |
| STATUS_CHANGED | STATE_CHANGED |
| TIMED_METADATA_AVAILABLE | TIMED_METADATA_ADDED |
| SIZE_AVAILABLE | SIZE_CHANGED |
| LOAD_INFO | LOAD_INFORMATION_AVAILABLE |

## Modifiche a MediaPlayer {#mediaplayer-changes}

Un nuovo metodo di costruzione `MediaPlayer` e modifiche ad alcuni metodi.

**Modifiche alla classe MediaPlayer**

Di seguito sono riportate le modifiche apportate alla `MediaPlayer` classe:

* L&#39; `MediaPlayerStatus` enum sostituisce `MediaPlayer.PlayerState`. Ad esempio:

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

* Ora viene chiamato `MediaPlayer.seekToLocalTime()` il metodo `MediaPlayer.seekToLocal`. Ad esempio:

```java
//TVSDK v1.4
public void seekToLocal(long localPosition) { mediaPlayer.seekToLocalTime(localPosition);
}

//TVSDK v2.5
public void seekToLocal(long localPosition) { mediaPlayer.seekToLocal(localPosition);
}
```

* Il `MediaPlayerView.notifyClick()` metodo ora è `MediaPlayer.notifyClick()`. Ad esempio:

```java
//TVSDK v1.4
public void adClick() { mediaPlayer.getView().notifyClick();
}

//TVSDK v2.5
public void adClick() { mediaPlayer.notifyClick();
}
```

* Il precedente `MediaPlayer.MediaPlayer.getNotificationHistory()` metodo ora è andato e non è stato sostituito.
* Il primo `MediaPlayer.replaceCurrentItem()` è suddiviso in due metodi: `replaceCurrentResource()`, che prende un&#39;istanza di `MediaResource`, e `replaceCurrentItem()`, che prende un&#39;istanza di `MediaPlayerItem`. Ad esempio:

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

È possibile utilizzare questa opzione per alternare tra le istanze di MediaPlayer preinizializzate, come nel caso di blackout.

**I costruttori sostituiscono i metodi statici create()**

È possibile utilizzare i costruttori in TVSDK v2.5, invece di utilizzare `create()` i metodi di TVSDK v1.4. Tutte le classi con nomi che iniziano con Predefinito, ad esempio `DefaultMediaPlayer`, `DefaultNetworkConfig`, `DefaultContentFactory`, non sono disponibili nella release v2.5.

In alcuni casi, l&#39;API TVSDK v1.4 utilizza il seguente pattern per la creazione delle classi:

1. Definire un&#39;interfaccia (ad esempio, `MediaPlayer`).
1. Specificare una classe predefinita (ad esempio, `DefaultMediaPlayer`).
1. Fornire un `create()` metodo sulla classe predefinita per fornire una classe che implementa l&#39;interfaccia.

In TVSDK v2.5, tali interfacce sono classi concrete e si creano istanze di queste classi utilizzando i rispettivi costruttori. I seguenti snippet di codice illustrano questa differenza:

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

Altre classi che non seguono questo pattern ma utilizzano `create()` metodi in 1.4 includono:

* MediaResource\
   Questo precedentemente utilizzato `MediaResource.createFromUrl()`. Ora utilizzate il costruttore, che richiede un URL, un tipo di risorsa e metadati. Ad esempio:

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

Alcune classi (ad esempio, `ContentFactory`) sono classi astratte senza implementazione predefinita accessibile al pubblico (ad esempio, `DefaultContentFactory`). In questi casi è possibile fornire un&#39;implementazione predefinita tramite una funzione di comodità, ad esempio: `mediaPlayerItemConfig.getDefaultContentFactory()`

**Modifiche apportate ai sottotitoli codificati**

Le seguenti modifiche interessano le classi correlate ai sottotitoli codificati:

* Quando si recuperano le tracce di didascalie chiuse, `MediaPlayerItem.getClosedCaptionTracks()` restituisce solo le tracce attive.
* `ClosedCaptionTrack` non dispone più di un `isActive()` metodo.

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

## Modifiche alla pubblicità {#advertising-changes}

La versione 2.5 contiene diverse modifiche relative agli annunci.

**Modifiche al comportamento pubblicitario**

Il comportamento predefinito della riproduzione dell&#39;annuncio quando un utente esegue una ricerca oltre un contenitore Annuncio cambia leggermente nella v2.5. Se l&#39;interruzione dell&#39;annuncio non è vista, l&#39;annuncio viene riprodotto dopo una ricerca in avanti. Quando l&#39;app utilizza il criterio di annunci predefinito, l&#39;interruzione dell&#39;annuncio viene rimossa al termine della riproduzione. Con TVSDK v2.5, se un utente cerca dietro un contenitore Annuncio sulla timeline e l&#39;interruzione dell&#39;annuncio non viene guardata, non viene riprodotto alcun annuncio.

Tuttavia, in TVSDK v1.4, per impostazione predefinita, viene riprodotto un annuncio nel caso di una ricerca indietro. Ad esempio, se cerchi indietro tra la terza e la quarta interruzione di annuncio, il comportamento predefinito per TVSDK v1.4 consiste nel riprodurre la terza interruzione di annuncio.

**Modifica delle regole di annuncio**

Le regole di annuncio vengono specificate utilizzando un file JSON. Il formato del file JSON rimane lo stesso in entrambe le versioni di TVSDK. Tuttavia, in TVSDK v2.5, il file JSON delle regole pubblicitarie deve essere ospitato in una posizione accessibile tramite un URL HTTP. L&#39;applicazione può utilizzare un&#39;istanza di AuditudeSettings.

```java
//TVSDK v2.5
AuditudeSettings result = new AuditudeSettings(); result.setCRSRulesJsonURL(<http url of AdobeTVSDKConfig.json>);
```

Nella versione 1.4 di TVSDK, questo file viene posizionato sotto la cartella assets nell’applicazione e TVSDK carica il file.

**Ridenominazione di annunci**

`AdvertisingFactory` è ora denominato `ContentFactory`. Con `ContentFactory` questo potete creare flussi di lavoro pubblicitari personalizzati ignorandone alcuni metodi. Utilizzate return null per mantenere i comportamenti predefiniti, come illustrato di seguito:

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

**Lunghezza zero interruzioni annuncio**

TVSDK 2.5 inserisce interruzioni pubblicitarie di lunghezza zero come segnaposto quando il server pubblicitario non restituisce annunci.

Le interruzioni di annunci con lunghezza zero possono essere determinate rilevando il numero di annunci che deve essere zero nell&#39;interruzione di annuncio utilizzando l&#39;evento onAdBreakStarted e l&#39;applicazione deve gestire tali interruzioni di annuncio di conseguenza.

**Modifiche apportate ai metadati**

La classe Metadata fornisce una sostituzione più efficace per la precedente classe MetadataNode.

* La classe Metadata può memorizzare stringhe, array di byte e altri oggetti Metadata:

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

* L&#39; `MetadataKeys` enum sostituisce `DefaultMetadataKeys`. Non tutte le chiavi in `DefaultMetadataKeys` sono presenti nella nuova versione.

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

* I metadati della pubblicità sono ora rappresentati dalla `AdvertisingMetadata` classe, una sottoclasse di Metadati, e ora sono memorizzati in `MediaPlayerItemConfig` piuttosto che `MediaResource`.

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

I metadati di configurazione della rete, precedentemente un membro della `MediaResource` classe, ora sono rappresentati dalla `NetworkConfiguration` classe e ora vengono memorizzati in `MediaPlayerItemConfig` anziché `MediaResource`.

```java
//TVSDK v1.4
MediaResource playerResource = MediaResource.createFromUrl(url, mediaMetadata);
...

//TVSDK v2.5
MediaPlayerItemConfig mediaItemConfig = new MediaPlayerItemConfig(context);

NetworkConfiguration mediaNetworkConfiguration = mediaItemConfig.getNetworkConfiguration();
```

**Modifiche all’analisi TimedMetadata**

L&#39;analisi di `TimedMetadata` è cambiata in 2.5 rispetto ai tipi di dati per l&#39;analisi del tag ID3.

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

* Il `notifyClick()` metodo è stato spostato da `MediaPlayerView` a `MediaPlayer`.

* `AdPolicySelector` è un&#39;interfaccia, non una classe. Implementa tutti i relativi metodi.
* `AdPolicyInfo` ora contiene un elenco di `AdBreakTimelineItem`, non `AdBreakPlacement`.

* Il nome API della classe `ContentResolver` astratta viene modificato.
* `PlacementOpportunityDetector` non è più disponibile. Estendete invece la classe `OpportunityGenerator` astratta. L&#39;implementazione di riferimento ne è un esempio.

* I parametri del `AdBreakPlacement` costruttore sono gli stessi, ma in un ordine diverso. Per un esempio di implementazione, vedi l’implementazione di Reference Player inclusa nel pacchetto con il prodotto.

## Modifiche in DRM {#changes-in-drm}

La maggior parte delle modifiche in questa versione si trova nel livello DRM. La tabella seguente mostra ulteriori modifiche tra le versioni 1.4 e 2.5:

| Metodo DRMManager | Callback di completamento in 1.4 | Callback di errore in 1.4 | Listener in 2.5 |
|--- |--- |--- |--- |
| acquisitionLicense | DRMLicenseAcquisredCallback | DRMOperationErrorCallback | DRMAcquireLicenseListener |
| acquisitionPreviewLicense | DRMLicenseAcquisredCallback | DRMOperationErrorCallback | DRMAcquireLicenseListener |
| autenticare | DRMAuthenticationCompleteCallback | DRMOperationErrorCallback | DRMAuthenticateListener |
| createMetadataFromBytes | NA | DRMOperationErrorCallback | DRMErrorListener |
| initialize | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |
| joinLicenseDomain | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |
| leftLicenseDomain | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |
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

L&#39; `DRMManager` istanza statica disponibile in 1.4 dopo la creazione di mediaplayer è ora disponibile dopo l&#39;attivazione del listener di `onDRMMetadataInfo` eventi.

## Modifiche relative al bitrate adattivo (ABR) {#adaptive-bitrate-abr-related-changes}

**Modifiche alle costanti**

Molte costanti hanno cambiato il tipo da `String` a `int`. Ad esempio: `MediaResourceType`, `ABRControlParameters`, e `MediaPlayerStatusChangeEvent`.

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

Sono stati aggiunti alcuni parametri, alcuni rinominati e altri spostati. Di seguito è riportata la firma del costruttore nella versione 1.4 e la nuova firma nella versione 2.5:

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

La `MediaError` classe è stata sostituita con la `Notification` classe. L&#39;unica differenza tra le classi `MediaError` e `Notification` è che queste non contengono un attributo description. I codici di errore TVSDK 1.4 con valori 101xxx, 102xxx,104xxx,106xxx,107xxx,109xxx non esistono in TVSDK 2.5. Per i codici di riproduzione di TVSDK 2.5, consultate Errore [nativo - valori](assets/psdk_android_2.5.pdf)di riproduzione video.

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

Tutti gli errori recuperabili vengono trattati come avvisi e vengono gestiti utilizzando l&#39; `NotificationEventListener` in TVSDK 2.5. Gli avvisi vengono visualizzati come notifiche con il `onOperationFailed` listener nel gestore QOS in TVSDK 1.4, dove come in TVSDK 2.5 l&#39;evento Notification è separato. L&#39;avviso trattato ai punti 1.4 e 2.5 è il seguente:

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

Mentre TVSDK v1.4 utilizzava una combinazione di valori Null, restituisce un errore e una serie di eccezioni ( `MediaPlayerException`, `IllegalStateException`e `IllegalArgumentException`), TVSDK v2.5 `generatesMediaPlayerException` per tutti gli errori.

>[!NOTE]
>
>Per ottenere informazioni dettagliate su MediaPlayerException, potete utilizzare `getErrorCode()`.

Esempio di modifica:

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

Sono state apportate lievi modifiche alle proprietà dell&#39;oggetto QOSProvider:

* L’opzione non `TimeToFirstFrame` è disponibile in TVSDK 2.5.
* TVSDK 2.5 QOSProvider dispone di una nuova proprietà per determinare la larghezza di banda percepita durante una sessione di streaming.

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

* Non `QOSEventListener::onOperationFailed()` esiste più in TVSDK 2.5. Gli avvisi che venivano visualizzati in questo listener di eventi ora vengono visualizzati nel listener di `NotificationEventListener::onNotification()` eventi.

* I `QOSProvider event listeners onBufferStart()`, `onBufferComplete()`, `onSeekStart()`, `onSeekComplete()`e `onLoadInfo()` sono singoli listener di eventi associati a un&#39;istanza mediaPlayer.

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

* Consulta la documentazione completa della guida nella pagina Informazioni e supporto [di](https://helpx.adobe.com/support/primetime.html) Adobe Primetime.