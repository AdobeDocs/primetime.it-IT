---
title: Conversione TVSDK - da 1.3 a 2.0 per JavaScript
seo-title: Conversione TVSDK - da 1.3 a 2.0 per JavaScript
description: Molte firme di metodo e i nomi degli elementi API sono cambiati per 2.0. Esaminate queste tabelle per visualizzare tutti i dettagli sulle modifiche API.
seo-description: Molte firme di metodo e i nomi degli elementi API sono cambiati per 2.0. Esaminate queste tabelle per visualizzare tutti i dettagli sulle modifiche API.
uuid: d2d1742d-c90c-43f5-94fc-8c4a57cb8ed4
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: migration
discoiquuid: c732f54d-116c-43f3-bec4-5e71af208426
translation-type: tm+mt
source-git-commit: cfd6da49e85e13e29e8458ee98231a8b476867db
workflow-type: tm+mt
source-wordcount: '5058'
ht-degree: 0%

---


# Conversione TVSDK - da 1.3 a 2.0 per JavaScript {#tvsdk-conversion-to-for-javascript}

Molte firme di metodo e i nomi degli elementi API sono cambiati per 2.0. Esaminate queste tabelle per visualizzare tutti i dettagli sulle modifiche API.

## Implementare le funzioni di callback in JavaScript {#implement-callback-functions-in-javascript}

I commenti presenti nella documentazione relativa ai metodi suggeriscono la firma per le callback da implementare.

Per JavaScript, la sintassi API si basa sull&#39;ID Web. Per un&#39;interfaccia TVSDK, i nomi dei metodi sono denominati *methodName*(). Affinché i metodi possano essere implementati dall&#39;applicazione, all&#39;interfaccia viene aggiunto un attributo di lettura/scrittura denominato ** methodNameCallbackFunc, che deve essere impostato come punto di una funzione che implementa il metodo. Ad esempio:

```shell
// An app implementable interface
interface ContentFactory
{
    /*
     * AdPolicySelector retrieveAdPolicySelector(MediaPlayerItem item);
     */
    attribute Object retrieveAdPolicySelectorCallbackFunc;
 
    /*
     * ContentResolverList retrieveResolvers(MediaPlayerItem item);
     */
    attribute Object retrieveResolversCallbackFunc;
 
    /*
     * OpportunityGeneratorList retrieveGenerators(MediaPlayerItem item);
     */
    attribute Object retrieveGeneratorsCallbackFunc;
};

// this is how to implement it
var factory = new AdobePSDK.ContentFactory();
factory.retrieveAdPolicySelectorCallbackFunc = function(item)
{
    // return your adPolicySelector according to the item
    return adPolicySelector;
}
 
mediaPlayerItemConfig = new AdobePSDK.MediaPlayerItemConfig ();
playerConfig.adFactory = factory;
// Use this config to load new MediaResource
```

## Modifiche dell&#39;elemento API del flusso di lavoro pubblicitario per la versione 2.0 {#advertising-workflow-api-element-changes-for}

Queste tabelle confrontano gli elementi API del flusso di lavoro pubblicitario per l’SDK JavaScript TVSDK tra le versioni 1.3 e 2.0.

Tabelle in questo argomento:

* TimedMetadata
* AdSignalingMode
* AdvertisingMetadata
* CustomRangeMetadata
* ReplaceTimeRange
* Posizionamento
* Opportunità
* Prenotazione
* Timeline / ElementoTimeline / IndicatoreTimeline
* AdBreak
* Ad / AdAsset / AdClick / AdList / AdAssetList / AdBannerAsset
* AdBreakTimelineItem / AdTimelineItem
* AdBreakPolicy / AdBreakWatchedPolicy / AdPolicy / AdPolicyMode / AdPolicyInfo / AdPolicySelector
* TimelineOperation
* AdBreakPlacement
* AuditudeSettings

### TimedMetadata {#timedmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p> <strong>TimedMetadata</strong>: interfaccia TimedMetadata {<br /> const unsigned short METADATA_TYPE_TAG = 0 ; <br /> const unsigned short METADATA_TYPE_ID3 = 1 ; <br /> readonly attributo short type non firmato; <br /> readonly attributo long time;<br /> readonly attribute DomString id;<br /> readonly attribute DomString name;<br /> readonly attribute DomString content; <br /> metadata Object dell'attributo readonly;<br /> }; </p> </td> 
   <td><p>interfaccia TimedMetadata {<br /> const unsigned short METADATA_TYPE_TAG = 0 ;<br /> const unsigned short METADATA_TYPE_ID3 = 1 ;<br /> readonly attributo unsigned short metadataType;<br /> readonly attributo long time;<br /> readonly attribute long id;<br /> readonly attribute DomString name;<br /> <br /> metadata Object dell'attributo readonly;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>TimedMetadataList</strong>: (Nessuna modifica per 2.0)</td> 
   <td><p>interfaccia TimedMetadataList {<br /> attributo readonly lunghezza lunga senza segno;<br /> getter TimedMetadata(indice lungo non firmato);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### AdSignalingMode {#adsignalingmode}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>Interface AdSignalingMode { <br /> const unsigned short MODE_DEFAULT, <br /> const unsigned short MODE_MANIFEST_CUES , <br /> const unsigned short MODE_SERVER_MAP , <br /> const unsigned short MODE_CUSTOM_RANGES <br /> };</p> </td> 
   <td>Questo sostituisce la chiave MetadataKeys::MANIFEST_CUES.</td> 
  </tr> 
 </tbody> 
</table>

### AdvertisingMetadata {#advertisingmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>Interface AdvertisingMetadata { <br /> attribute AdSignalingMode mode; <br /> attribute AdBreakWatchedPolicy adBreakAsWatched; <br /> attribute boolean livePreroll; <br /> attribute boolean delayAdLoading ; <br /> };</p> </td> 
   <td>Questa funzionalità è stata fornita da<p>MetadataKeys:ADVERTISING_METADATA</p> key.</td> 
  </tr> 
 </tbody> 
</table>

### CustomRangeMetadata {#customrangemetadata}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>Interface CustomRangeMetadata { <br /> const unsigned short TYPE_MARK_RANGE; <br /> const unsigned short TYPE_DELETE_RANGE; <br /> const unsigned short TYPE_REPLACE_RANGE; <br /> attributo tipo breve non firmato; <br /> attribute boolean adjustSeekPosition; <br /> timeRangeList attributo timeRangeList; <br /> };</p> </td> 
   <td>(Novità per 2.0)</td> 
  </tr> 
 </tbody> 
</table>

### ReplaceTimeRange {#replacetimerange}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface ReplaceTimeRange { <br /> attributo long begin non firmato; <br /> readonly attribute unsigned long end; <br /> la durata dell'attributo non firmato; <br /> attribute long replaceDuration non firmato; <br /> };</p> </td> 
   <td>(Novità per 2.0)</td> 
  </tr> 
 </tbody> 
</table>

### Posizionamento {#placement}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>Posizione interfaccia { <br /> const unsigned short TYPE_MID_ROLL; <br /> const unsigned short TYPE_PRE_ROLL; <br /> const unsigned short TYPE_POST_ROLL; <br /> const unsigned short TYPE_SERVER_MAP; <br /> const unsigned short TYPE_CUSTOM_RANGE;<br /> readonly attributo short type non firmato; <br /> readonly attributo long time; <br /> readonly: lunga durata attributo; <br /> const unsigned short MODE_DEFAULT; <br /> const unsigned short MODE_INSERT; <br /> const unsigned short MODE_REPLACE; <br /> const unsigned short MODE_DELETE; <br /> const unsigned short MODE_MARK; <br /> const unsigned short MODE_FREE_REPLACE; <br /> readonly attributo unsigned short mode; <br /> readonly attribute TimeRange; <br /> };</p> </td> 
   <td>(Novità per 2.0)</td> 
  </tr> 
 </tbody> 
</table>

### Opportunità {#opportunity}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface Opportunity { <br /> readonly attribute DomString id; <br /> posizionamento dell'attributo readonly; <br /> readonly attribute Object settings; <br /> readonly attribute Object customParameters; <br /> }; </p> </td> 
   <td>(Novità per 2.0)</td> 
  </tr> 
 </tbody> 
</table>

### Prenotazione {#reservation}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface Reservation { <br /> readonly attributo intervallo TimeRange; <br /> readonly attribute long hold; <br /> }; </p> </td> 
   <td> (Novità per 2.0)</td> 
  </tr> 
 </tbody> 
</table>

### Timeline / ElementoTimeline / IndicatoreTimeline {#timeline-timelineitem-timelinemarker}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p><strong>Timeline</strong>: interfaccia Timeline <br /> { attributo readonly TimelineMarkerList timelineMarkers; <br /> readonly attribute TimelineItemList timelineItems; <br /> double convertToLocalTime( double time); <br /> double convertToVirtualTime( double time); <br /> };</p> </td> 
   <td><p>cronologia interfaccia {<br /> attributo readonly TimelineMarkerList timelineMarkers;<br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p> <strong>TimelineItem</strong>: interface TimelineItem :<br /> TimelineMarker {<br /> readonly attribute long id; <br /> readonly attribute TimeRange virtualRange; <br /> readonly attribute TimeRange localRange; <br /> readonly attributo boolean guardato; <br /> readonly attribute boolean temporary; <br /> }; </p> </td> 
   <td>(Novità per 2.0)</td> 
  </tr> 
  <tr> 
   <td><strong>TimelineMarker</strong>: (Nessuna modifica per 2.0)</td> 
   <td><p>interface TimelineMarker {<br /> readonly attributo double time;<br /> readonly attributo doppia durata;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### AdBreak {#adbreak}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface AdBreak {<br /> } <br /> attributo <br /> <br /> readonly doppia durata;<br /> readonly attribute AdList ads;<br /> <br /> <br /> readonly attribute AdInsertionType InsertType;<br /> }; </p> </td> 
   <td><p>interface AdBreak {<br /> attributo readonly double time;<br /> readonly attribute double replaceDuration;<br /> <br /> readonly attributo doppia durata;<br /> readonly attribute AdList adList;<br /> <br /> readonly attributo DomString data;<br /> <br /> }; </p> </td> 
  </tr> 
 </tbody> 
</table>

### Ad / AdAsset / AdClick / AdList / AdAssetList / AdBannerAsset {#ad-adasset-adclick-adlist-adassetlist-adbannerasset}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p> <strong>Annuncio</strong>: interface Ad {<br /> readonly attribute AdAsset PrimaryAsset;<br /> readonly attribute AdAssetList companionAssets;<br /> <br /> readonly attributo doppia durata;<br /> readonly attribute DomString id;<br /> const unsigned short ADTYPE_LINEAR = 0 ;<br /> const unsigned short ADTYPE_NONLINEAR = 1 ;<br /> <br /> readonly attribute unsigned short adType;<br /> readonly attribute AdInsertionType adInsertionType; <br /> <br /> readonly attribute boolean click; <br /> readonly attribute boolean isCustomAdMarker;<br /> }; </p> </td> 
   <td><p>interface Ad {<br /> readonly attribute AdAsset PrimaryAsset;<br /> readonly attribute AdAssetList companionAssets;<br /> <br /> readonly attributo doppia durata;<br /> readonly attribute DomString id;<br /> const unsigned short ADTYPE_LINEAR = 0 ;<br /> const unsigned short ADTYPE_NONLINEAR = 1 ;<br /> <br /> readonly attributo short type non firmato;<br /> readonly attribute AdInsertionType InsertType; <br /> readonly attribute Object tracker;<br /> <br /> <br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAsset</strong>: (Nessuna modifica per 2.0)</td> 
   <td><p>interface AdAsset {<br /> readonly attribute DomString id;<br /> readonly attributo doppia durata;<br /> readonly attribute MediaResource resource;<br /> attributo di sola lettura AdClick adClick;<br /> metadata Object dell'attributo readonly;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdClick</strong>: (Nessuna modifica per 2.0)</td> 
   <td><p>interface AdClick {<br /> readonly attribute DomString id;<br /> readonly attribute DomString title;<br /> readonly attribute DomString url;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdList</strong>: (Nessuna modifica per 2.0)</td> 
   <td><p>interface AdList {<br /> attributo readonly lunghezza non firmata;<br /> getter Ad(indice lungo non firmato);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAssetList</strong>: (Nessuna modifica per 2.0)</td> 
   <td><p>interface AdAssetList {<br /> attributo readonly lunghezza lunga senza segno;<br /> getter AdAsset(indice lungo senza segno);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBannerAsset</strong>: interface AdBannerAsset: Attributo AdAsset<br /> {<br /> readonly in larghezza;<br /> readonly attribute int height;<br /> readonly attribute DomString staticUrl;<br /> readonly attribute DomString height;<br /> readonly attribute DomString width;<br /> };</p> </td> 
   <td> Novità in 2.0</td> 
  </tr> 
 </tbody> 
</table>

### AdBreakTimelineItem / AdTimelineItem {#adbreaktimelineitem-adtimelineitem}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p> <strong>AdBreakTimelineItem</strong>: interface AdBreakTimelineItem : TimelineItem { attributo <br /> readonly AdBreak adBreak; <br /> elementi AdTimelineItemList di attributi readonly; <br /> }; </p> </td> 
   <td> (Novità per 2.0)</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdTimelineItem</strong>: interface AdTimelineItem : TimelineItem { attributo <br /> readonly AdBreak adBreak; <br /> readonly attribute Ad ad; <br /> }; </p> </td> 
   <td> (Novità per 2.0)</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBreakTimelineItemList</strong>: interface AdBreakTimelineItemList { attributo <br /> readonly lunghezza lunga non firmata; <br /> getter AdBreakTimelineItem (indice ng non firmato); <br /> };</p> </td> 
   <td> (Novità per 2.0)</td> 
  </tr> 
 </tbody> 
</table>

### AdBreakPolicy / AdBreakWatchedPolicy / AdPolicy / AdPolicyMode / AdPolicyInfo / AdPolicySelector {#adbreakpolicy-adbreakwatchedpolicy-adpolicy-adpolicymode-adpolicyinfo-adpolicyselector}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface AdBreakPolicy {<br /> attributo readonly short AD_BREAK_POLICY_SKIP;<br /> readonly attributo short AD_BREAK_POLICY_PLAY;<br /> readonly attribute short AD_BREAK_POLICY_REMOVE;<br /> readonly attributo short AD_BREAK_POLICY_REMOVE_AFTER_PLAY;<br /> };</p> </td> 
   <td><p> interface AdPolicyConstants {<br /> attributo readonly short AD_BREAK_POLICY_SKIP;<br /> readonly attributo short AD_BREAK_POLICY_PLAY;<br /> readonly attribute short AD_BREAK_POLICY_REMOVE;<br /> readonly attributo short AD_BREAK_POLICY_REMOVE_AFTER_PLAY;}<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p> interface AdBreakWatchedPolicy {<br /> attributo readonly short AD_BREAK_AS_WATCHED_ON_BEGIN;<br /> readonly attributo short AD_BREAK_AS_WATCHED_ON_END;<br /> readonly attributo short AD_BREAK_AS_WATCHED_NEVER;<br /> }; </p> </td> 
   <td><p> ...<br /> readonly attributo short AD_BREAK_AS_WATCHED_ON_BEGIN;<br /> readonly attributo short AD_BREAK_AS_WATCHED_ON_END;<br /> readonly attributo short AD_BREAK_AS_WATCHED_NEVER;<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicy {<br /> readonly attribute short AD_POLICY_PLAY;<br /> readonly attributo short AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> readonly attributo short AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN; readonly attributo short AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK;<br /> <br /> readonly attributo short AD_POLICY_SKIP_AD_BREAK;<br /> };</p> </td> 
   <td><p> ... <br /> readonly attribute short AD_POLICY_PLAY;<br /> readonly attributo short AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> readonly attributo short AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN;<br /> readonly attributo short AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK;<br /> readonly attributo short AD_POLICY_SKIP_AD_BREAK;<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicyMode {<br /> readonly attributo short AD_POLICY_MODE_PLAY;<br /> readonly attribute short AD_POLICY_MODE_SEEK;<br /> readonly attribute short AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
   <td><p> ...<br /> {readonly attribute short AD_POLICY_MODE_PLAY;<br /> readonly attribute short AD_POLICY_MODE_SEEK;<br /> readonly attribute short AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicyInfo {<br /> attributo AdBreakTimelineItemList e <br /> BreakTimelineItems di sola lettura;<br /> adarTimelineItem eTimelineItem di attributi readonly;<br /> readonly attribute double currentTime;<br /> readonly attributo double searchToTime;<br /> readonly attribute double rate;<br /> readonly attribute short mode; //AdPolicyMode<br /> };</p> </td> 
   <td><p>interface AdPolicyInfo {<br /> attributo AdBreakPlacementList <br /> adBreakPlacements di readonly;<br /> readonly attribute Ad ad;<br /> readonly attribute double currentTime;<br /> readonly attributo double searchToTime;<br /> readonly attribute double rate;<br /> readonly attribute short mode; //AdPolicyMode<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> attributo Object selectPolicyForAdBreakCallbackFunc;<br /> /**<br /> * AdBreakTimelineItemList selectAdBreaksToPlay(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> attributo Object selectAdBreaksToPlayCallbackFunc;<br /> /**<br /> * AdPolicy selectPolicyForSeekIntoAd(AdPolicyInfo adPolicyInfo);<br /> */<br /> attributo Object selectPolicyForSeekIntoAdCallbackFunc; <br /> /**<br /> * AdBreakWatchedPolicy selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> attributo Object selectWatchedPolicyForAdBreakCallbackFunc;<br /> };</p> </td> 
   <td><p>interface AdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> attributo Object selectPolicyForAdBreakFuncCallback;<br /> /**<br /> * AdBreakPlacementList selectAdBreaksToPlay(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> attributo Object selectAdBreaksToPlayCallback;<br /> /**<br /> * AdPolicy selectPolicyForSeekIntoAd(AdPolicyInfo adPolicyInfo);<br /> */<br /> attributo Object selectPolicyForSeekIntoAdCallback; <br /> /**<br /> * AdBreakAsWatched selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> attributo Object selectWatchedPolicyForAdBreakCallback;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### TimelineOperation {#timelineoperation}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface TimelineOperation { posizionamento <br /> dell'attributo readonly; <br /> };</p> </td> 
   <td> (Novità per 2.0)</td> 
  </tr> 
 </tbody> 
</table>

### AdBreakPlacement {#adbreakplacement}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface AdBreakPlacement : TimelineOperation {<br /> attributo di sola lettura AdBreak adBreak;<br /> posizionamento dell'attributo readonly; // Da TimelineOperation<br /> attributo readonly doppio time;<br /> readonly attributo doppia durata;<br /> };</p> </td> 
   <td><p>interface AdBreakPlacement {<br /> attributo di sola lettura AdBreak adBreak;<br /> posizionamento dell'attributo readonly;<br /> readonly attributo double time;<br /> readonly attributo doppia durata;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### AuditudeSettings {#auditudesettings}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interfaccia AuditudeSettings : AdvertisingMetadata { <br /> attribute DomString zoneId; <br /> attribute DomString mediaId; <br /> attribute DomString defaultMediaId ; <br /> dominio DomString attributo; <br /> attribute Object targetingInfo; <br /> attribute Object customParameters; <br /> attribute Boolean creativePackingEnabled;<br /> attribute Boolean showStaticBanners ;<br /> };</p> </td> 
   <td>La funzionalità è stata fornita daMetadataKeys::AUDITUDE_METADATA_KEY key.</td> 
  </tr> 
 </tbody> 
</table>

## Modifiche dell&#39;elemento API di personalizzazione per 2.0 {#customization-api-element-changes-for}

Queste tabelle confrontano gli elementi dell&#39;API di personalizzazione per l&#39;SDK JavaScript TVSDK tra le versioni 1.3 e 2.0.

Tabelle in questo argomento:

* MediaPlayerItemConfig
* ContentFactory
* NetworkConfiguration

### MediaPlayerItemConfig {#mediaplayeritemconfig}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface MediaPlayerItemConfig {<br /> attribute ContentFactory adFactory;<br /> attribute StringList subscriptionTags;<br /> <br /> attribute StringList adTags;<br /> <br /> <br /> attribute AdSignalingMode adSignalingMode;<br /> attribute CustomRangeMetadata customRangeMetadata;<br /> attribute NetworkConfiguration networkConfiguration;<br /> attribute AdvertisingMetadata advertisingMetadata;<br /> attribute Boolean useHardwareDecoder;<br /> };</p> </td> 
   <td><p>interface MediaPlayerConfig {<br /> <br /> attributo <br /> <br /> StringList adTags;<br /> attribute StringList subscribedTags;<br /> attribute MediaPlayerClientFactory clientFactory;<br /> <br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### ContentFactory {#contentfactory}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface ContentFactory {<br /> /*<br /> * AdPolicySelector retrieveAdPolicySelector(<br /> * elemento MediaPlayerItem);<br /> */<br /> attributo Object retrieveAdPolicySelectorCallbackFunc;<br /> };</p> </td> 
   <td><p>interface MediaPlayerClientFactory {<br /> /*<br /> * AdPolicySelector retrieveAdPolicySelector(<br /> * elemento MediaPlayerItem);<br /> */<br /> attributo Object retrieveAdPolicySelectorFunc;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### NetworkConfiguration {#networkconfiguration}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface NetworkConfiguration<br /> {<br /> attribute boolean forceNativeNetworking;<br /> attribute boolean useRedirectUrl;<br /> attribute Object cookieHeader;<br /> attribute boolean readSetCookieHeader;<br /> attribute int masterUpdateInterval; <br /> attribute boolean useCookieHeaderForAllRequests;<br /> attribute int readLimit;<br /> };</p> </td> 
   <td>Nella versione 1.3, alcune di queste funzionalità erano fornite da MetadataKeys</td> 
  </tr> 
 </tbody> 
</table>

## Modifiche dell&#39;elemento API DRM per 2.0 {#drm-api-element-changes-for}

Queste tabelle confrontano gli elementi DRM API per l’SDK JavaScript TVSDK tra le versioni 1.3 e 2.0.

Tabelle in questo argomento:

* Inizializzazione flusso di lavoro DRM
* DRMAcquireLicenseSettings / DRMAuthenticationMethod
* DRMMetadata
* DRMPlaybackTimeWindow
* DRMLicense
* DRMLicenseDomain
* DRMPolicy
* DRMManager

### Inizializzazione flusso di lavoro DRM {#drm-workflow-initialization}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>Per avviare il flusso di lavoro DRM, l’applicazione deve chiamare AdobePSDK.startDRMWorkflow. Senza questa chiamata, i video DRM non verranno riprodotti.<p>interfaccia AdobePSDK<br /> {<br /> void startDRMWorkFlow(<br /> DomString appStoratePath, <br /> DomString publisherId, <br /> DomString appId, <br /> DomString appVersion, <br /> booleano privacyModeOn);<br /> };</p> </td> 
   <td>L'inizializzazione è stata eseguita internamente e non è stata richiesta alcuna chiamata esplicita.</td> 
  </tr> 
 </tbody> 
</table>

### DRMAcquireLicenseSettings/DRMAuthenticationMethod {#drmacquirelicensesettings-drmauthenticationmethod}

| API 2.0 | 1.3 API |
|--- |--- |
| **DRMAcquireLicenseSettings** |  |
| Nessuna modifica per 2.0. | enum DRMAcquireLicenseSettings <br>{<br> const unsigned int FORCE_REFRESH = 0;<br> const unsigned int LOCAL_ONLY = 1;<br> const unsigned int ALLOW_SERVER = 2;<br> }; |
| **DRMAuthenticationMethod** |  |
| Nessuna modifica per 2.0. | enum DRMAuthenticationMethod <br>{<br> const unsigned int UNKNOWN = 0;<br> const unsigned int ANONYMOUS = 1;<br> const unsigned int USERNAME_AND_PASSWORD = 2;<br> } |

### DRMMetadata {#drmmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>Nessuna modifica per 2.0.</td> 
   <td><p>interfaccia DRMMetadata<br /> {<br /> readonly attributo DomString serverUrl;<br /> readonly attribute DomString licenseId;<br /> readonly attributo DRMPolicyArray policy; <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMPlaybackTimeWindow {#drmplaybacktimewindow}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interfaccia DRMPlaybackTimeWindow {<br /> attributo readonly in riproduzionePeriodInSeconds;<br /> readonly attributo long playStartDate;<br /> readonly attributo long playEndDate;<br /> };</p> </td> 
   <td><p>interfaccia DRMPlaybackTimeWindow {<br /> attributo readonly int pointInSeconds;<br /> readonly attribute int startDate;<br /> readonly attribute int endDate;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMLicense {#drmlicense}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>Nessuna modifica per 2.0.</td> 
   <td><p>interfacce DRMLicense {<br /> readonly attributo Uint8Array byte;<br /> readonly attribute Date licenseStartDate;<br /> readonly attribute Date licenseEndDate;<br /> readonly attribute Date offlineStorageStartDate;<br /> readonly attributo Date offlineStorageEndDate; <br /> readonly attribute DomString serverUrl;<br /> readonly attribute DomString licenseID;<br /> readonly attribute DomString policyID;<br /> readonly attribute DRMPlaybackTimeWindow playTimeWindow;<br /> readonly attribute Object customProperties;<br /> }; </p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMLicenseDomain {#drmlicensedomain}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interfaccia DRMLicenseDomain {<br /> readonly attributo DomString authenticationDomain;<br /> readonly attribute DRMAuthenticationMethod authenticationMethod; <br /> readonly attribute DomString serverUrl;<br /> };</p> </td> 
   <td><p>interfaccia DRMLicenseDomain {<br /> readonly attributo DomString authDomain;<br /> readonly attribute DRMAuthenticationMethod authMethod; <br /> readonly attribute DomString serverURL;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMPolicy {#drmpolicy}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interfaccia DRMPolicy<br /> {<br /> readonly attributo DomString authenticationDomain;<br /> readonly attribute DRMAuthenticationMethod authenticationMethod;<br /> <br /> readonly attribute DomString displayName;<br /> readonly attributo DRMLicenseDomain licenseDomain;<br /> };</p> </td> 
   <td><p>interfaccia DRMPolicy<br /> {<br /> readonly attributo DomString authDomain;<br /> readonly attribute DRMAuthenticationMethod authMethod;<br /> readonly attribute DomString dispName;<br /> readonly attributo DRMLicenseDomain licenseDomain;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMManager {#drmmanager}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface DRMManager : EventTarget {<br /> void acquisitionLicense(metadati DRMMetadata, impostazione <br /> DRMAcquireLicenseSettings, listener <br /> DRMAquireLicenseListener);<br /> void acquisitionPreviewLicense(metadati DRMMetadata, listener <br /> DRMAquireLicenseListener);<br /> void authenticate(metadati DRMMetadata, URL <br /> DomString,<br /> DomString &amp;authenticationDomain, utente <br /> DomString, password <br /> DomString, listener <br /> DRMAuthenticateListener);<br /> <br /> DRMMetadata createMetadataFromBytes(array<br /> Uint8Array, listener DRMErrorListener);<br /> void initialize(listener DRMOperationCompleteListener);<br /> attribute long maxOperationTime;<br /> <br /> void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> boolean forceRefresh, <br /> DRMOperationCompleteListener listener);<br /> void leftLicenseDomain(<br /> DRMLicenseDomain licenseDomain, listener <br /> DRMOperationCompleteListener);<br /> <br /> void resetDRM(DRMOperationCompleteListener listener);<br /> void returnLicense(DomString serverURL, <br /> DomString licenseID, <br /> DomString policyID, commitImmediatamente <br /> booleano,<br /> listener DRMReturnLicenseListener);<br /> void setAuthenticationToken(<br /> metadati DRMMetadata, <br /> DomString authenticationDomain, token <br /> Uint8Array, listener <br /> DRMOperationCompleteListener);<br /> void storeLicenseBytes(Uint8Array licenseBytes, listener <br /> DRMOperationCompleteListener);<br /> };</p> </td> 
   <td><p>interface DRMManager : EventTarget {<br /> void acquisitionLicense(metadati DRMMetadata, impostazione <br /> DRMAcquireLicenseSettings, <br /> EventContext eventContext);<br /> void acquisitionPreviewLicense(metadati DRMMetadata, <br /> EventContext eventContext);<br /> void authenticate(metadati DRMMetadata, URL <br /> DomString,<br /> DomString &amp;authenticationDomain, utente <br /> DomString, password <br /> DomString, <br /> EventContext eventContext);<br /> <br /> DRMMetadata createMetadataFromBytes(array<br /> Uint8Array, EventContext eventContext);<br /> void initialize(EventContext eventContext);<br /> attribute long maxOperationTime;<br /> <br /> void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> boolean forceRefresh, <br /> EventContext eventContext);<br /> void leftLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> EventContext eventContext);<br /> <br /> void resetDRM(EventContext eventContext);<br /> void returnLicense(DomString serverURL, <br /> DomString licenseID,<br /> DomString policyID, <br /> booleano commitImmediatamente,<br /> EventContext eventContext);<br /> void setAuthenticationToken(<br /> metadati DRMMetadata, <br /> DomString authenticationDomain, token <br /> Uint8Array, eventoContext <br /> EventContext);<br /> void storeLicenseBytes(Uint8Array licenseBytes, <br /> EventContext eventContext);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>class DRMErrorListener : <br /> public psdkutils::PSDKInterfaceWithUserData {<br /> public:<br /> void virtuale onDRMError(uint32_t major, <br /> uint32_t minor, <br /> const psdkutils: PSDKString&amp; errorString, <br /> const psdkutils::PSDKString&amp; errorServerUrl) = 0;<br /> <br /> protected:<br /> virtual ~DRMErrorListener() {}<br /> }</p> </td> 
   <td>Evento / Interfaccia / Descrizione 
    <ul> 
     <li>kEventDRMOperationError<p>/ DRMOperationErrorEvent</p> <p>Quando si verifica un errore durante uno dei metodi asincroni di DRMManger.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>class DRMOperationCompleteListener : <br /> public DRMErrorListener {<br /> public:<br /> void virtuale onDRMOperationComplete() = 0;<br /> <br /> protected:<br /> virtual ~DRMOperationCompleteListener() {}<br /> };</p> </td> 
   <td>Evento / Interfaccia / Descrizione 
    <ul> 
     <li>kEventDRMInitializationComplete<p>/ PSDKEvent</p> <p>Quando l'inizializzazione di DRM è completa.</p> </li> 
     <li>kEventDRMJoinLicenseDomainComplete<p>/ PSDKEvent</p> <p>Al completamento dell'azione joinLicenseDomain().</p> </li> 
     <li>kEventDRMLeaveLicenseDomainComplete<p>/ PSDKEvent</p> <p>Quando l'azione leftLicenseDomain() viene completata correttamente.</p> </li> 
     <li>kEventDRMResetCompletePSDKEvent<p>/ PSDKEvent</p> <p>Quando l'azione resetDRM() viene completata correttamente.</p> </li> 
     <li>kEventDRMAuthenticationTokenSet<p>/ PSDKEvent</p> <p>Quando l'azione setAuthenticationTokenSet() viene completata correttamente.</p> </li> 
     <li>kEventDRMLicenseStored<p>/ PSDKEvent</p> <p>Quando l'azione storeLicenseBytes() viene completata correttamente.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>class DRMAuthenticateListener : <br /> public DRMErrorListener {<br /> public:<br /> void virtuale onAuthenticationComplete(<br /> psdkutils::PSDKImmutableByteArray* <br /> authenticationToken) = 0;<br /> <br /> protected:<br /> virtual ~DRMAuthenticateListener() {}<br /> }</p> </td> 
   <td>Evento / Interfaccia / Descrizione 
    <ul> 
     <li>kEventDRMAuthenticationComplete<p>/ DRMAuthenticationCompleteEvent</p> <p>Quando la chiamata del metodo DRMManager::authenticate ha esito positivo.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>classe DRMAquireLicenseListener: <br /> public DRMErrorListener {<br /> public:<br /> void virtuale onLicenseAcquired(const DRMLicense*) = 0;<br /> <br /> protected:<br /> virtual ~DRMAquireLicenseListener() {}<br /> };</p> </td> 
   <td>Evento / Interfaccia / Descrizione 
    <ul> 
     <li>kEventDRMPreviewLicenseAcquisred<p>/ DRMLicenseAcquisredEvent</p> <p>Quando la chiamata del metodo DRMManager::acquisitionPreviewLicense ha esito positivo.</p> </li> 
     <li>kEventDRMLicenseAcquired<p>/ DRMLicenseAcquisredEvent</p> <p>Quando la chiamata del metodo DRMManager::acquisitionLicense ha esito positivo.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>class DRMReturnLicenseListener: <br /> public DRMErrorListener {<br /> public:<br /> void virtuale onLicenseReturnComplete(uint32_t numReturn ) = 0;<br /> <br /> protected:<br /> virtual ~DRMReturnLicenseListener() {}<br /> };</p> </td> 
   <td>Evento / Interfaccia / Descrizione 
    <ul> 
     <li>kEventDRMLicenseReturnComplete<p>/ DRMLicenseReturnCompleteEvent</p> <p>Quando la chiamata del metodo DRMManager::returnLicense ha esito positivo.</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## Modifiche generiche all&#39;elemento API di riproduzione per 2.0 {#generic-playback-api-element-changes-for}

Queste tabelle confrontano gli elementi API di riproduzione generici tra JavaScript TVSDK 1.3 e 2.0.

Tabelle in questo argomento:

* MediaResource
* MediaPlayer
* ABRControlParameters
* BufferControlParameters
* TextFormat
* MediaPlayerItemLoader

### MediaResource {#mediaresource}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface MediaResource {<br /> attribute DomString url; <br /> attributo tipo breve non firmato;<br /> metadata dell'oggetto attribute;<br /> const unsigned short TYPE_HLS;<br /> const unsigned short TYPE_HDS;<br /> const unsigned short TYPE_DASH;<br /> const unsigned short TYPE_CUSTOM;<br /> const unsigned short TYPE_UNKNOWN;<br /> };</p> </td> 
   <td><p>interface MediaResource {<br /> attribute DomString url;<br /> tipo DomString attributo;<br /> metadata dell'oggetto attribute;<br /> <br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### MediaPlayer {#mediaplayer}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface MediaPlayer : EventTarget<br /> {<br /> void PrepareToPlay( doppia posizione);<br /> void play();<br /> void pause();<br /> void search( doppia posizione);<br /> void searchToLocal( doppia posizione);<br /> void reset();<br /> void release();<br /> void replaceCurrentItem(MediaPlayerItem item);<br /> void replaceCurrentResource(MediaResource source, configurazione <br /> MediaPlayerItemConfig); <br /> void suspension();<br /> void restore();<br /> void notificationClick();<br /> <br /> readonly attribute TimeRange playRange;<br /> readonly attribute TimeRange, ricerkableRange;<br /> readonly attribute double currentTime;<br /> readonly attributo double localTime;<br /> readonly attribute TimeRange bufferedRange;<br /> readonly attribute DRMManager drmManager;<br /> readonly attribute MediaPlayerItem currentItem;<br /> <br /> // PlayerStatus<br /> <br /> <br /> const unsigned short PLAYER_STATUS_INITIALIZED;<br /> const unsigned short PLAYER_STATUS_PREPARING;<br /> const unsigned short PLAYER_STATUS_PREPARED;<br /> const short PLAYER_STATUS_PLAYING non firmato;<br /> const short PLAYER_STATUS_PAUSED;<br /> const unsigned short PLAYER_STATUS_SEEKING;<br /> const short PLAYER_STATUS_COMPLETE;<br /> const unsigned short PLAYER_STATUS_ERROR;<br /> const short PLAYER_STATUS_RELEASED;<br /> <br /> Attributo readonly status short non firmato;<br /> <br /> attributo volume breve non firmato;<br /> attribute ABRControlParameters abrControlParameters;<br /> attribute BufferControlParameters bufferControlParameters;<br /> <br /> const unsigned short VISIBILE; //Per i contenuti di visibilità CC<br /> non firmati short INVISIBIBILE; //Per l'attributo di visibilità<br /> CC non firmata ccVisibility breve;<br /> attribute TextFormat ccStyle;<br /> readonly attribute PlaybackMetrics PlaybackMetrics;<br /> <br /> doppia tariffa attributo;<br /> attribuire la visualizzazione MediaPlayerView;<br /> timeline attributo readonly<br /> attribute double currentTimeUpdateInterval; <br /> // l'impostazione non sarà supportata per 2.0<br /> };</p> </td> 
   <td><p>interface MediaPlayer : EventTarget<br /> {<br /> void PrepareToPlay( posizione int);<br /> void play();<br /> void pause();<br /> void search( int position);<br /> void searchToLocalTime( posizione int);<br /> void reset();<br /> void release();<br /> void replaceCurrentItem(origine MediaResource);<br /> <br /> <br /> <br /> <br /> <br /> <br /> readonly attribute TimeRange playRange;<br /> readonly attribute TimeRange, ricerkableRange;<br /> readonly attribute double currentTime;<br /> readonly attributo double localTime;<br /> readonly attribute TimeRange bufferedRange;<br /> readonly attribute DRMManager drmManager;<br /> readonly attribute MediaPlayerItem currentItem;<br /> <br /> // PlayerState<br /> const unsigned short PLAYER_STATE_IDLE;<br /> const unsigned short PLAYER_STATE_INITIALIZING;<br /> const unsigned short PLAYER_STATE_INITIALIZED;<br /> const unsigned short PLAYER_STATE_PREPARING;<br /> const unsigned short PLAYER_STATE_PREPARED;<br /> const unsigned short PLAYER_STATE_PLAYING;<br /> const unsigned short PLAYER_STATE_PAUSED;<br /> const unsigned short PLAYER_STATE_SEEKING;<br /> const unsigned short PLAYER_STATE_COMPLETE;<br /> const unsigned short PLAYER_STATE_ERROR;<br /> const short PLAYER_STATE_RELEASED;<br /> const short PLAYER_STATUS_SUSPENDED;<br /> readonly attributo unsigned short state;<br /> <br /> attributo volume breve non firmato;<br /> attribute ABRControlParameters abrControlParameters;<br /> attribute BufferControlParameters bufferControlParameters;<br /> <br /> readonly unsigned short VISIBILE; //Per la visibilità<br /> CC, leggete solo la breve invisibile non firmata; //Per l'attributo di visibilità<br /> CC non firmata ccVisibility breve;<br /> attribute TextFormat ccStyle;<br /> readonly attribute PlaybackMetrics PlaybackMetrics;<br /> attribute MediaPlayerConfig mediaPlayerConfig;<br /> doppia tariffa attributo;<br /> attribuire la visualizzazione MediaPlayerView;<br /> timeline attributo readonly<br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface MediaPlayerStatus<br /> {<br /> // PlayerStatus<br /> const short PLAYER_STATUS_IDLE non firmato;<br /> const unsigned short PLAYER_STATUS_INITIALIZING;<br /> const unsigned short PLAYER_STATUS_INITIALIZED;<br /> const unsigned short PLAYER_STATUS_PREPARING;<br /> const unsigned short PLAYER_STATUS_PREPARED;<br /> const short PLAYER_STATUS_PLAYING non firmato;<br /> const short PLAYER_STATUS_PAUSED;<br /> const unsigned short PLAYER_STATUS_SEEKING;<br /> const short PLAYER_STATUS_COMPLETE;<br /> const unsigned short PLAYER_STATUS_ERROR;<br /> const short PLAYER_STATUS_RELEASED;<br /> const short PLAYER_STATUS_SUSPENDED;<br /> };</p> </td> 
   <td>(Novità per 2.0)</td> 
  </tr> 
 </tbody> 
</table>

#### Eventi supportati da MediaPlayer {#events-supported-by-mediaplayer}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 Nome evento</th> 
   <th>Interfaccia 2.0</th> 
   <th> </th> 
   <th>1.3 Nome evento</th> 
   <th>1.3 Interfaccia</th> 
  </tr> 
  <tr> 
   <td><p>(soppresso per 2.0)</p> </td> 
   <td> </td> 
   <td> </td> 
   <td>preparato</td> 
   <td>Evento</td> 
  </tr> 
  <tr> 
   <td><p>itemUpdated</p> <p>Quando un elemento del lettore multimediale viene aggiornato.</p> </td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>aggiornato</p> <p>Quando il lettore multimediale ha aggiornato correttamente il supporto.</p> </td> 
   <td>Evento</td> 
  </tr> 
  <tr> 
   <td>timedMetadataAvailable</td> 
   <td>TimedMetadataEvent</td> 
   <td> </td> 
   <td>TtmedMetadata</td> 
   <td>TimedMetadataEvent</td> 
  </tr> 
  <tr> 
   <td>timelineUpdated</td> 
   <td>Evento</td> 
   <td> </td> 
   <td>TmelineUpdated</td> 
   <td>Evento</td> 
  </tr> 
  <tr> 
   <td>Eliminato in 2.0</td> 
   <td> </td> 
   <td> </td> 
   <td>playStart</td> 
   <td>Evento</td> 
  </tr> 
  <tr> 
   <td>Eliminato per 2.0</td> 
   <td> </td> 
   <td> </td> 
   <td>playComplete</td> 
   <td>Evento</td> 
  </tr> 
  <tr> 
   <td>statusChanged</td> 
   <td>StatusEvent</td> 
   <td> </td> 
   <td>stateChanged</td> 
   <td>StateEvent</td> 
  </tr> 
  <tr> 
   <td>sizeAvailable</td> 
   <td>SizeEvent</td> 
   <td> </td> 
   <td>size</td> 
   <td>SizeEvent</td> 
  </tr> 
  <tr> 
   <td>adBreakStarted</td> 
   <td>AdBreakEvent</td> 
   <td> </td> 
   <td>adBreakStart</td> 
   <td>AdBreakEvent</td> 
  </tr> 
  <tr> 
   <td>adStarted</td> 
   <td>AdEvent</td> 
   <td> </td> 
   <td>adStart</td> 
   <td>AdEvent</td> 
  </tr> 
  <tr> 
   <td>adProgress</td> 
   <td>AdProgressEvent</td> 
   <td> </td> 
   <td>adProgress</td> 
   <td>AdProgressEvent</td> 
  </tr> 
  <tr> 
   <td>adCompleted</td> 
   <td>AdEvent</td> 
   <td> </td> 
   <td>adComplete</td> 
   <td>AdEvent</td> 
  </tr> 
  <tr> 
   <td>adBreakCompleted</td> 
   <td>AdBreakEvent</td> 
   <td> </td> 
   <td>adBreakComplete</td> 
   <td>AdBreakEvent</td> 
  </tr> 
  <tr> 
   <td>timeChanged</td> 
   <td>TimeEvent</td> 
   <td> </td> 
   <td>progress</td> 
   <td>ProgressEvent</td> 
  </tr> 
  <tr> 
   <td>bufferingBegin</td> 
   <td>Evento</td> 
   <td> </td> 
   <td>buffer</td> 
   <td>Evento</td> 
  </tr> 
  <tr> 
   <td>bufferingEnd</td> 
   <td>Evento</td> 
   <td> </td> 
   <td>bufferComplete</td> 
   <td>Evento</td> 
  </tr> 
  <tr> 
   <td>searchBegin</td> 
   <td>SeekEvent</td> 
   <td> </td> 
   <td>searchStart</td> 
   <td>Evento</td> 
  </tr> 
  <tr> 
   <td>searchEnd</td> 
   <td>SeekEvent</td> 
   <td> </td> 
   <td>searchComplete</td> 
   <td>TimeEvent</td> 
  </tr> 
  <tr> 
   <td>loadInformationAvailable</td> 
   <td>LoadInformationEvent</td> 
   <td> </td> 
   <td>loadInfo</td> 
   <td>LoadInfoEvent</td> 
  </tr> 
  <tr> 
   <td>operationFailed</td> 
   <td>NotificationEvent</td> 
   <td> </td> 
   <td>operationFailed</td> 
   <td>ErrorEvent</td> 
  </tr> 
  <tr> 
   <td>drmMetadataInfoAvailable</td> 
   <td>DRMMetadataEvent</td> 
   <td> </td> 
   <td>drmMetadata</td> 
   <td>DRMMetadataEvent</td> 
  </tr> 
  <tr> 
   <td>reserveReached</td> 
   <td>ReservationEvent</td> 
   <td> </td> 
   <td>timelineHolderReached</td> 
   <td>TimelineHolderEvent</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td>bitrateChanged</td> 
   <td>BitrateChangedEvent</td> 
  </tr> 
  <tr> 
   <td>rateSelected</td> 
   <td>PlaybackRateEvent</td> 
   <td> </td> 
   <td>rateSelected</td> 
   <td>PlaybackRateEvent</td> 
  </tr> 
  <tr> 
   <td>ratePlaying</td> 
   <td>PlaybackRateEvent</td> 
   <td> </td> 
   <td>ratePlaying</td> 
   <td>PlaybackRateEvent</td> 
  </tr> 
  <tr> 
   <td>adBreakSkipped</td> 
   <td>AdBreakEvent</td> 
   <td> </td> 
   <td>adBreakSkipped</td> 
   <td>AdBreakEvent</td> 
  </tr> 
  <tr> 
   <td>adClic<br /> Quando l'utente fa clic su un annuncio.</td> 
   <td>AdClicEvent</td> 
   <td> </td> 
   <td><p>Novità in 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>profileChanged<br /> Quando il profilo di riproduzione cambia.</td> 
   <td>ProfileEvent</td> 
   <td> </td> 
   <td><p>Novità in 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>searchPositionAdjusted<br /> Quando la posizione di ricerca viene regolata a causa di regole interne o esterne.</td> 
   <td>SeekEvent</td> 
   <td> </td> 
   <td><p>Novità in 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>audioAggiornato<br /> Quando un elemento del lettore multimediale viene aggiornato. Per alcuni flussi che contengono tracce audio rilevabili solo in fase di riproduzione, questo evento viene attivato quando sono disponibili nuove tracce audio.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>Novità in 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>captionsAggiornato <br /> Quando un elemento del lettore multimediale viene aggiornato. Per i flussi live/lineari, il client deve aggiornare periodicamente la risorsa multimediale per rilevare il nuovo contenuto disponibile. In questo caso, alcune caratteristiche del supporto potrebbero cambiare.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>Novità in 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>masterAggiornato <br /> Quando un elemento del lettore multimediale viene aggiornato. Per i flussi live/lineari, il client deve aggiornare periodicamente la risorsa multimediale per rilevare il nuovo contenuto disponibile. In questo caso, alcune caratteristiche del supporto potrebbero cambiare.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>Novità in 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>riproduzioneRangeAggiornato<br /> Quando un elemento del lettore multimediale viene aggiornato. Per i flussi live/lineari, il client deve aggiornare periodicamente la risorsa multimediale per rilevare il nuovo contenuto disponibile. In questo caso, alcune caratteristiche del supporto potrebbero cambiare.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>Novità in 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>timedEvent<br /> Inviato quando vengono generati eventi temporizzati.</td> 
   <td>TimedEvent</td> 
   <td> </td> 
   <td><p>Novità in 2.0</p> </td> 
  </tr> 
 </tbody> 
</table>

### ABRControlParameters {#abrcontrolparameters}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interfaccia ABRControlParameters<br /> {<br /> const unsigned short ABR_POLICY_CONSERVATIVE = 0 ;<br /> const unsigned short ABR_POLICY_MODERATE = 1 ;<br /> const unsigned short ABR_POLICY_AGGRESIVE = 2 ;<br /> <br /> attribute short abrPolicy;<br /> attribute unsigned int initialBitRate;<br /> attribute int minBitRate non firmato;<br /> attribute unsigned int maxBitRate;<br /> const unsigned short DEFAULT_ABR_INITIAL_BITRATE;<br /> const unsigned short DEFAULT_ABR_MIN_BITRATE;<br /> const unsigned short DEFAULT_ABR_MAX_BITRATE;<br /> const ABRPolicy DEFAULT_ABR_POLICY;<br /> };</p> </td> 
   <td><p>interfaccia ABRControlParameters<br /> {<br /> const unsigned short ABR_POLICY_CONSERVATIVE = 0 ;<br /> const unsigned short ABR_POLICY_MODERATE = 1 ;<br /> const unsigned short ABR_POLICY_AGGRESIVE = 2 ;<br /> <br /> attribute short abrPolicy;<br /> attribute unsigned int initialBitRate;<br /> attribute int minBitRate non firmato;<br /> attribute unsigned int maxBitRate;<br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### BufferControlParameters {#buffercontrolparameters}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface BufferControlParameters<br /> {<br /> attribute double initialBufferTime;<br /> attribute double playBufferTime;<br /> const double DEFAULT_INITIAL_BUFFER_TIME;<br /> const double DEFAULT_PLAY_BUFFER_TIME;<br /> };</p> </td> 
   <td><p>interface BufferControlParameters<br /> {<br /> attribute double initialBufferTime;<br /> attribute double playBufferTime;<br /> <br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### TextFormat {#textformat}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>Nessuna modifica per 2.0</td> 
   <td><p>interface TextFormat<br /> {<br /> // Colore<br /> const unsigned short COLOR_DEFAULT = 0 ;<br /> const unsigned short COLOR_BLACK = 1 ;<br /> const unsigned short COLOR_GRAY = 2 ;<br /> const unsigned short COLOR_WHITE = 3 ;<br /> const unsigned short COLOR_BRIGHT_WHITE = 4 ;<br /> const unsigned short COLOR_DARK_RED = 5 ;<br /> const unsigned short COLOR_RED = 6 ;<br /> const unsigned short COLOR_BRIGHT_RED = 7 ;<br /> const unsigned short COLOR_DARK_GREEN = 8 ;<br /> const unsigned short COLOR_GREEN = 9 ;<br /> const unsigned short COLOR_BRIGHT_GREEN = 10 ;<br /> const unsigned short COLOR_DARK_BLUE = 11 ;<br /> const unsigned short COLOR_BLUE = 12 ;<br /> const unsigned short COLOR_BRIGHT_BLUE = 13 ;<br /> const unsigned short COLOR_DARK_YELLOW = 14 ;<br /> const unsigned short COLOR_YELLOW = 15 ;<br /> const unsigned short COLOR_BRIGHT_YELLOW = 16 ;<br /> const unsigned short COLOR_DARK_MAGENTA = 17 ;<br /> const unsigned short COLOR_MAGENTA = 18 ;<br /> const unsigned short COLOR_BRIGHT_MAGENTA = 19 ;<br /> const unsigned short COLOR_DARK_CYAN = 20 ;<br /> const unsigned short COLOR_CYAN = 21 ;<br /> const unsigned short COLOR_BRIGHT_CYAN = 22 ;<br /> <br /> readonly attributo short fontColor non firmato;<br /> readonly attributo short backgroundColor non firmato;<br /> readonly attributo short fillColor non firmato;<br /> readonly attributo short edgeColor non firmato;<br /> <br /> // Dimensione<br /> contenuto non firmata SIZE_DEFAULT = 0 ;<br /> const unsigned short SIZE_SMALL = 1 ;<br /> const unsigned short SIZE_MEDIUM = 2 ;<br /> const unsigned short SIZE_LARGE = 3 ;<br /> <br /> readonly attributo unsigned short size;<br /> <br /> // Const FontEdge<br /> const short FONT_EDGE_DEFAULT = 0 non firmato;<br /> const unsigned short FONT_EDGE_NONE = 1 ;<br /> const unsigned short FONT_EDGE_RAISED = 2 ;<br /> const unsigned short FONT_EDGE_DEPRESSED = 3 ;<br /> const unsigned short FONT_EDGE_UNIFORM = 4 ;<br /> const unsigned short FONT_EDGE_DROP_SHADOW_LEFT = 5 ;<br /> const unsigned short FONT_EDGE_DROP_SHADOW_RIGHT = 6 ;<br /> readonly attributo short fontEdge non firmato;<br /> <br /> // Contenuti del font<br /> abbreviati FONT_DEFAULT = 0 ;<br /> const unsigned short FONT_MONOSPACED_WITH_SERIFS = 1 ;<br /> const unsigned short FONT_PROPORTIONAL_WITH_SERIFS = 2 ;<br /> const unsigned short FONT_MONSPACED_WITHOUT_SERIFS = 3 ;<br /> const unsigned short FONT_CASUAL = 4 ;<br /> const unsigned short FONT_CURSIVE = 5 ;<br /> const unsigned short FONT_SMALL_CAPITALS = 6 ;<br /> readonly attributo unsigned short font;<br /> readonly attribute short fontOpacity non firmato;<br /> readonly attribute short backgroundOpacity non firmato;<br /> readonly attribute short fillOpacity non firmato;<br /> readonly attributo unsigned short DEFAULT_OPACITY;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### MediaPlayerItemLoader {#mediaplayeritemloader}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface MediaPlayerItemLoader:<br /> {<br /> void load(MediaResource, long resourceId,<br /> listener ItemLoaderListener, configurazione <br /> MediaPlayerItemConfig);<br /> void cancel();<br /> readonly attribute MediaPlayerItem currentItem;<br /> };</p> </td> 
   <td>Nuovo per 2.0</td> 
  </tr> 
  <tr> 
   <td><p>interface ItemLoaderListener<br /> {<br /> //onLoadCompleteCallbackFunc(MediaPlayerItem)<br /> var onLoadCompleteCallbackFunc;<br /> //onErrorCallbackFunc(PSDKErrorCode)<br /> var onErrorCallbackFunc;<br /> }</p> </td> 
   <td>Nuovo per 2.0</td> 
  </tr> 
 </tbody> 
</table>

## Modifiche degli elementi API delle caratteristiche multimediali per 2.0 {#media-characteristics-api-element-changes-for}

Queste tabelle confrontano gli elementi dell&#39;API delle caratteristiche dei supporti per l&#39;SDK C++ TVSDK tra le versioni 1.3 e 2.0.

Tabelle in questo argomento:

* MediaPlayerItem
* Track, AudioTrack, ClosedCaptionsTrack
* Profilo
* DRMMetadataInfo

### MediaPlayerItem {#mediaplayeritem}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface MediaPlayerItem {<br /> readonly attributo MediaResource;<br /> readonly attribute long resourceId;<br /> readonly attributo boolean live;<br /> <br /> readonly attribute boolean hasAlternateAudio;<br /> readonly attribute AudioTrackList audioTracks;<br /> attributo readonly AudioTrack selectedAudioTrack;<br /> void selectAudioTrack(AudioTrack track); <br /> <br /> readonly attribute boolean hasClosedCaptions;<br /> readonly attribute ClosedCaptionsTrackList closedCaptionsTracks;<br /> readonly attribute ClosedCaptionsTrack selectedClosedCaptionsTrack;<br /> void selectClosedCaptionsTrack(traccia<br /> ClosedCaptionsTrack); <br /> <br /> readonly attribute boolean hasTimedMetadata;<br /> attributo Legonly TimedMetadataList timedMetadata;<br /> readonly attribute boolean dynamic;<br /> <br /> readonly attribute boolean isProtected;<br /> readonly attribute DRMMetadataInfoList drmMetadataInfos;<br /> profili ProfileList di attributi readonly;<br /> Attributo readonly Profilo selectedProfile;<br /> <br /> readonly attributo booleano truccoPlaySupported;<br /> readonly attribute FloatArray availablePlaybackRates;<br /> readonly attribute float selectedPlaybackRate;<br /> <br /> <br /> readonly attribute MediaPlayer mediaPlayer;<br /> config dell’attributo di sola lettura MediaPlayerItemConfig;<br /> };</p> </td> 
   <td><p>interface MediaPlayerItem {<br /> readonly attributo MediaResource;<br /> readonly attribute long resourceId;<br /> readonly attributo boolean live;<br /> <br /> readonly attribute boolean hasAlternateAudio;<br /> readonly attribute AudioTrackList audioTracks;<br /> attribute AudioTrack selectedAudioTrack;<br /> <br /> <br /> readonly attribute boolean hasClosedCaptions;<br /> readonly attribute ClosedCaptionsTrackList ccTracks;<br /> attribute ClosedCaptionsTrack selectedCCTrack;<br /> <br /> <br /> <br /> readonly attribute boolean hasTimedMetadata;<br /> attributo Legonly TimedMetadataList timedMetadata;<br /> readonly attribute boolean dynamic;<br /> <br /> readonly attribute boolean isProtected;<br /> readonly attribute DRMMetadataInfoList drmMetadataInfos;<br /> profili ProfileList di attributi readonly;<br /> <br /> <br /> readonly attributo booleano truccoPlaySupported;<br /> readonly attribute Int32Array availablePlaybackRates;<br /> <br /> readonly attribute StringList adTags;<br /> <br /> readonly attribute MediaPlayer mediaPlayer;<br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### Track / AudioTrack / ClosedCaptionsTrack {#track-audiotrack-closedcaptionstrack}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface Track<br /> {<br /> readonly attribute DomString name;<br /> readonly attributo DomString language;<br /> readonly attribute boolean default;<br /> readonly attribute boolean autoSelect;<br /> }; </p> </td> 
   <td>Nuovo per 2.0</td> 
  </tr> 
  <tr> 
   <td><p>interface AudioTrack : Track<br /> {<br /> readonly attribute DomString name; //FromTrack<br /> readonly attributo DomString language;//FromTrack<br /> readonly attributo booleano predefinito; // Da Track<br /> readonly attributo boolean autoSelect;//FromTrack<br /> <br /> attributo readonly non firmato int pid;<br /> };</p> </td> 
   <td><p>interface AudioTrack<br /> {<br /> nome DomString attributo readonly;<br /> readonly attributo DomString language; <br /> readonly attribute boolean default;<br /> readonly attribute boolean autoSelect;<br /> attributo readonly boolean forzato;<br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td>Nessuna modifica per 2.0</td> 
   <td><p>interface AudioTrackList<br /> {<br /> attributo readonly lunghezza non firmata;<br /> getter AudioTrack (indice lungo senza segno);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface ClosedCaptionsTrack : Track<br /> {<br /> readonly attribute DomString name; //FromTrack<br /> readonly attributo DomString language;//FromTrack<br /> readonly attributo booleano predefinito; // Attributo di sola lettura FromTrack<br /> booleano autoSelect;//FromTrack<br /> const <br /> <br /> unsigned short SERVICE_608_CAPTIONS = 0;<br /> const unsigned short SERVICE_708_CAPTIONS = 1;<br /> const unsigned short SERVICE_WEB_VTT_CAPTIONS = 2;<br /> readonly attribute short serviceType non firmato;<br /> attributo readonly boolean forzato;<br /> };</p> </td> 
   <td><p>interface ClosedCaptionsTrack<br /> {<br /> nome DomString dell'attributo readonly;<br /> readonly attributo DomString language;<br /> readonly attribute boolean default;<br /> <br /> <br /> readonly attribute boolean active;<br /> <br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td>Nessuna modifica per 2.0</td> 
   <td><p>interface ClosedCaptionsTrackList<br /> {<br /> attributo readonly lunghezza non firmata;<br /> getter ClosedCaptionsTrack(indice esteso non firmato);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### Profilo {#profile}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>Profilo: Nessuna modifica per 2.0</td> 
   <td><p>profilo<br /> interfaccia {<br /> attributo readonly non firmato in larghezza;<br /> readonly attributo unsigned int height;<br /> readonly attributo int bitRate non firmato;<br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td>ProfileList: Nessuna modifica per 2.0</td> 
   <td><p>interface ProfileList<br /> {<br /> attributo readonly lunghezza non firmata;<br /> getter Profile(indice lungo non firmato);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMMetadataInfo {#drmmetadatainfo}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><strong>DRMMetadataInfo</strong>: Nessuna modifica per 2.0</td> 
   <td><p>interfacce DRMMetadataInfo<br /> { <br /> metadati DRMMetadata di sola lettura;<br /> readonly attributo long prefetchTimestamp;<br /> readonly attribute TimeRange;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>DRMMetadataInfoList</strong>: Nessuna modifica per 2.0</td> 
   <td><p>interfaccia DRMMetadataInfoList<br /><br /> {attributo readonly lunghezza non firmata;<br /> getter DRMMetadataInfo(indice esteso non firmato);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

## Mapping di errori C++ alle eccezioni in diverse lingue {#mapping-c-errors-to-exceptions-in-different-languages}

È possibile mappare i codici di errore C++ alle eccezioni in lingue diverse.

Il PSDK C++ dispone di un criterio di &quot;nessun lancio&quot; per le proprie API. La maggior parte dei metodi API restituisce un valore PSDKErrorCode per indicare se il metodo è stato eseguito correttamente. Gli errori asincroni vengono notificati tramite gli eventi di errore.

Il ActionScript  e il PSDK JAVA hanno un criterio diverso. La maggior parte degli errori genererà un ArgumentError o IllegalStateException per indicare che la parte sincrona del metodo non può essere eseguita. Queste eccezioni non vengono rilevate e il codice dell&#39;applicazione è responsabile della gestione delle eccezioni. In genere contengono informazioni utili sul motivo per cui la chiamata del metodo ha avuto esito negativo. Ad esempio, se il comando readyToPlay viene chiamato in uno stato non valido, viene generata l&#39;eccezione seguente:

```shell
throw new IllegalStateException("Invalid player state. prepareToPlay method 
must be called only once after replaceCurrentItem or replaceCurrentResource method.");
```

Il  ActionScript/JAVA genera inoltre eccezioni dai costruttori per indicare che alcuni oggetti interni sono stati creati in modo errato. Queste eccezioni vengono gestite internamente e non vengono propagate all’applicazione. Le eccezioni verranno incluse in una notifica di avviso inviata all&#39;applicazione

Ad esempio, se non è stato trovato alcun file multimediale valido per la risposta all&#39;annuncio ricevuta, non è possibile creare alcun oggetto o annuncio pubblicitario valido. Di conseguenza, non viene inserito alcun annuncio nella timeline e viene inviata una notifica NotificationEvent.OperationFailed.

I codici di errore o di avviso ricevuti in modo asincrono dal motore video del Adobe  (AVE) vengono inviati all&#39;applicazione come eventi normali. L&#39;evento di notifica contiene tutti i codici di errore ricevuti ed eventuali metadati aggiuntivi, ad esempio l&#39;URL, l&#39;identificatore della risorsa, l&#39;handle e così via. Se l’errore è grave e la riproduzione del supporto corrente non può continuare, MediaPlayer passa allo stato ERROR e all’evento onStatusChanged o MediaPlayerStatusChanged.STATUS_CHANGED viene inviato. Se la riproduzione può continuare, viene inviato un normale evento di notifica.

<table> 
 <tbody> 
  <tr> 
   <th>Errore C++ (codice PSDKError)</th> 
   <th> </th> 
   <th>Java</th> 
   <th>ActionScript </th> 
   <th>JavaScript</th> 
  </tr> 
  <tr> 
   <td>kECInvalidArgument</td> 
   <td> </td> 
   <td>IllegalArgumentException</td> 
   <td>ArgumentError</td> 
   <td>Eccezione con il codice = 1, descrizione = "INVALID_ARGUMENT" e AdditionalInfo= &lt;come passato dal metodo che ha generato questa eccezione&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNullPointer</td> 
   <td> </td> 
   <td>IllegalArgumentException</td> 
   <td>ArgumentError</td> 
   <td>Eccezione con il codice = 2, descrizione = "GENERIC_ERROR" e AdditionalInfo= &lt;as passato dal metodo che ha generato questa eccezione&gt;</td> 
  </tr> 
  <tr> 
   <td>kECIllegalState</td> 
   <td> </td> 
   <td>IllegalStateException</td> 
   <td>IllegalStateException</td> 
   <td>Eccezione con il codice = 3, descrizione = "ILLEGAL_STATE" e AdditionalInfo= &lt;come passato dal metodo che ha generato questa eccezione&gt;</td> 
  </tr> 
  <tr> 
   <td>kECInterfaceNotFound</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con il codice = 4, descrizione = "GENERIC_ERROR" e AdditionalInfo= &lt;as passato dal metodo che ha generato questa eccezione&gt;</td> 
  </tr> 
  <tr> 
   <td>kECCreationFailed</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con il codice = 5, descrizione = "CREATION_FAILED" e AdditionalInfo= &lt;come passato dal metodo che ha generato questa eccezione&gt;</td> 
  </tr> 
  <tr> 
   <td>kECUnsupportedOperation</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con il codice = 5, descrizione = "CREATION_FAILED" e AdditionalInfo= &lt;come passato dal metodo che ha generato questa eccezione&gt;</td> 
  </tr> 
  <tr> 
   <td>kELataNotAvailable</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con il codice = 7, descrizione = "DATA_NOT_AVAILABLE" e AdditionalInfo= &lt;come passato dal metodo che ha generato questa eccezione&gt;</td> 
  </tr> 
  <tr> 
   <td>kECSeekError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con il codice = 8, descrizione = "SEEK_ERROR" e AdditionalInfo= &lt;come passato dal metodo che ha generato questa eccezione&gt;</td> 
  </tr> 
  <tr> 
   <td>kECUnsupportedFeature</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con il codice = 9, descrizione = "UNSUPPORTED_FEATURE" e AdditionalInfo= &lt;come passato dal metodo che ha generato questa eccezione&gt;</td> 
  </tr> 
  <tr> 
   <td>kECRangeError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 10, descrizione = "RANGE_ERROR" e AdditionalInfo= &lt;come passato dal metodo che ha generato questa eccezione</td> 
  </tr> 
  <tr> 
   <td>kECCodecNotSupported</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 11, descrizione = "CODEC_NOT_SUPPORTED" e AdditionalInfo= &lt;come passato dal metodo che ha generato questa eccezione&gt;</td> 
  </tr> 
  <tr> 
   <td>kECMediaError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 12, descrizione = "MEDIA_ERROR" e AdditionalInfo= &lt;come passato dal metodo che ha generato questa eccezione&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNetworkError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 13, descrizione = "NETWORK_ERROR" e AdditionalInfo= &lt;come passato dal metodo che ha generato questa eccezione&gt;</td> 
  </tr> 
  <tr> 
   <td>kECGenericError</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Error o MediaPlayerNotification.Warning</td> 
   <td>MediaError o NotificationEvent</td> 
   <td>Eccezione con codice = 14, descrizione = "GENERIC_ERROR" e AdditionalInfo= &lt;come passato dal metodo che ha generato questa eccezione&gt;</td> 
  </tr> 
  <tr> 
   <td>kECInvalidSeekTime</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 15, descrizione = "INVALID_SEEK_TIME" e AdditionalInfo= &lt;come passato dal metodo che ha generato questa eccezione&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAudioTrackError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 16, descrizione = "AUDIO_TRACK_ERROR" e AdditionalInfo= &lt;come passato dal metodo che ha generato questa eccezione&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAccessFromdifferent<p>ThreadError</p> </td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 17, descrizione = "GENERIC_ERROR" e AdditionalInfo= &lt;come passato dal metodo che ha generato questa eccezione&gt;</td> 
  </tr> 
  <tr> 
   <td>kECElementNotFound</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con il codice = 18, descrizione = "GENERIC_ERROR" e AdditionalInfo= &lt;come passato dal metodo che ha generato questa eccezione</td> 
  </tr> 
  <tr> 
   <td>kECNotImplemented</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 19, descrizione = "GENERIC_ERROR" e AdditionalInfo= &lt;come passato dal metodo che ha generato questa eccezione&gt;</td> 
  </tr> 
  <tr> 
   <td>kECPlaybackOperationFailed</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 200, descrizione = "PLAYBACK_OPERATION_FAILED" e AdditionalInfo= &lt;come passato dal metodo che ha generato questa eccezione&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNativeWarning</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Warning</td> 
   <td>NotificationEvent</td> 
   <td>Eccezione con codice = 201, descrizione = "NATIVE_WARNING" e AdditionalInfo= &lt;come passato dal metodo che ha generato questa eccezione</td> 
  </tr> 
  <tr> 
   <td>kECAdResolverFailed</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Warning</td> 
   <td>-</td> 
   <td>Eccezione con codice = 202, descrizione = "AD_RESOLVER_FAILED" e AdditionalInfo= &lt;come passato dal metodo che ha generato questa eccezione&gt;</td> 
  </tr> 
 </tbody> 
</table>

## Modifiche degli elementi API Utility e Helper per per 2.0 {#utility-and-helper-api-element-changes-for}

Queste tabelle confrontano gli elementi Utility e Helper API per JavaScript TVSDK tra le versioni 1.3 e 2.0.

Tabelle in questo argomento:

* Versione
* TimeRange
* QOSProvider
* DeviceInformation
* LoadInfo
* Visualizza
* PlaybackInformation

### Versione {#version}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>versione<br /> dell'interfaccia {<br /> readonly attribute DomString version;<br /> readonly attribute DomString description;<br /> readonly attribute long major;<br /> attributo readonly long minor;<br /> Legonly attributo long revision;<br /> readonly attributo long apiVersion;<br /> };</p> </td> 
   <td><p>versione<br /> dell'interfaccia {<br /> readonly attribute DomString version;<br /> readonly attribute DomString description;<br /> readonly attribute DomString major;<br /> readonly attribute DomString minor;<br /> readonly attribute DomString revision;<br /> readonly attribute DomString apiVersion;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### TimeRange {#timerange}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>Nessuna modifica per 2.0</td> 
   <td><p>interface TimeRange<br /> {<br /> attributo readonly non signed long begin;<br /> readonly attribute unsigned long end;<br /> readonly attributo unsigned long length;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### QOSProvider {#qosprovider}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>Nessuna modifica per 2.0</td> 
   <td><p>interfaccia QOSProvider<br /> {<br /> void attachmentMediaPlayer(MediaPlayer player);<br /> void detachMediaPlayer();<br /> <br /> readonly attribute DeviceInformation deviceInformation;<br /> readonly attribute PlaybackInformation PlaybackInformation;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DeviceInformation {#deviceinformation}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface DeviceInformation<br /> {<br /> readonly attribute DomString os;<br /> <br /> <br /> <br /> readonly attribute DomString id;<br /> readonly attribute int densityDPI;<br /> readonly attribute int heightPixels;<br /> readonly attribute int widthPixels;<br /> readonly attributo booleano searchToKeyFrame;<br /> };</p> </td> 
   <td><p>interface DeviceInformation<br /> {<br /> readonly attribute DomString os;<br /> readonly attribute int sdk;<br /> readonly attribute DomString model;<br /> readonly attribute DomString Manufacturer;<br /> readonly attribute DomString id;<br /> readonly attribute int densityDPI;<br /> readonly attribute int heightPixels;<br /> readonly attribute int widthPixels;<br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### LoadInfo {#loadinfo}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>Nessuna modifica per 2.0</td> 
   <td><p>interface LoadInfo<br /> {<br /> readonly attribute DomString url;<br /> readonly attribute int size;<br /> readonly attribute double downloadDuration;<br /> readonly attribute int pointIndex;<br /> readonly attribute double mediaDuration;<br /> readonly attributo short TRACK_TYPE_FRAGMENT;<br /> readonly attributo short TRACK_TYPE_TRACK;<br /> readonly attributo short TRACK_TYPE_MANIFEST;<br /> readonly attribute short type;<br /> readonly attribute DomString trackName;<br /> readonly attribute DomString trackType;<br /> readonly attribute int trackIndex;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### Visualizza {#view}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>Nessuna modifica per 2.0</td> 
   <td><p>visualizzazione<br /> interfaccia {<br /> attributo readonly non firmato short x;<br /> readonly attribute unsigned short y;<br /> readonly attributo unsigned short width;<br /> readonly attributo unsigned short height;<br /> <br /> void setSize(short width non firmato, unsigned short height);<br /> void setPos(unsigned short x, unsigned short y);<br /> }</p> </td> 
  </tr> 
 </tbody> 
</table>

### PlaybackInformation {#playbackinformation}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface PlaybackInformation<br /> {<br /> readonly attributo doubleToFirstByte;<br /> readonly attribute double timeToLoad;<br /> readonly attributo doubleToStart;<br /> readonly attribute double timeToFail;<br /> readonly attribute int totalSecondsPlayed;<br /> readonly attribute int totalSecondsSpent;<br /> readonly attribute double frameRate;<br /> readonly attribute int dropFrameCount;<br /> readonly attribute int perceedBandwidth;<br /> readonly attribute int bitrate;<br /> readonly attribute double bufferTime;<br /> readonly attribute int bufferLength;<br /> readonly attribute int emptyBufferCount;<br /> readonly attributo double bufferingTime;<br /> };</p> </td> 
   <td><p>interface PlaybackInformation<br /> {<br /> readonly attributo doubleToFirstByte;<br /> readonly attribute double timeToLoad;<br /> readonly attributo doubleToStart;<br /> readonly attribute double timeToFail;<br /> readonly attribute int totalSecondsPlayed;<br /> readonly attribute int totalSecondsSpent;<br /> readonly attribute double frameRate;<br /> readonly attribute int dropFrameCount;<br /> <br /> readonly attribute int bitrate;<br /> readonly attribute double bufferTime;<br /> readonly attribute int bufferLength;<br /> readonly attribute int emptyBufferCount;<br /> readonly attributo double bufferingTime;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

## Risorse utili {#helpful-resources}

* Consulta la documentazione completa della guida [pagina Informazioni e supporto](https://helpx.adobe.com/support/primetime.html) di Adobe Primetime.
