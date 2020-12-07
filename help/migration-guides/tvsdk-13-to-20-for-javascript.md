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

Per JavaScript, la sintassi API si basa sull&#39;ID Web. Per un&#39;interfaccia TVSDK, i nomi dei metodi sono denominati *methodName*(). Affinché i metodi possano essere implementati dall&#39;applicazione, all&#39;interfaccia viene aggiunto un attributo di lettura/scrittura denominato *methodName* CallbackFunc e l&#39;applicazione deve impostarlo in modo che punti a una funzione che implementa il metodo. Ad esempio:

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

## Modifiche dell&#39;elemento API del flusso di lavoro pubblicitario per 2.0 {#advertising-workflow-api-element-changes-for}

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
   <td><p> <strong>TimedMetadata</strong>: interfaccia TimedMetadata {<br /> const unsigned short METADATA_TYPE_TAG = 0 ;  <br /> const unsigned short METADATA_TYPE_ID3 = 1 ;  <br /> readonly attributo short type non firmato;  <br /> readonly attributo long time;<br /> readonly attribute DomString id;<br /> readonly attribute DomString name;<br /> readonly attribute DomString content;  <br /> readonly attribute Object metadata;<br /> }; </p> </td> 
   <td><p>interface TimedMetadata {<br /> const unsigned short METADATA_TYPE_TAG = 0 ;<br /> const unsigned short METADATA_TYPE_ID3 = 1 ;<br /> readonly attribute unsigned short metadataType;<br /> readonly attribute long time;<br /> readonly attribute long id;<br /> readonly attribute Dom name;<br /> <br /> metadati dell'attributo di sola lettura Object;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>TimedMetadataList</strong>: (Nessuna modifica per 2.0)</td> 
   <td><p>interface TimedMetadataList {<br /> attributo readonly lunghezza lunga senza segno;<br /> getter TimedMetadata(indice lungo senza segno);<br /> };</p> </td> 
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
   <td><p>Interface AdSignalingMode { <br /> const unsigned short MODE_DEFAULT, <br /> const unsigned short MODE_MANIFEST_CUES, <br /> const unsigned short MODE_SERVER_MAP, <br /> const unsigned short MODE_CUSTOM_RANGES <br /> };</p> </td> 
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
   <td><p>Interface AdvertisingMetadata { <br /> attributo AdSignalingMode mode; <br /> attributo AdBreakWatchedPolicy adBreakAsWatched; <br /> attributo boolean livePreroll; <br /> attributo boolean delayAdLoading ; <br /> };</p> </td> 
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
   <td><p>Interface CustomRangeMetadata { <br /> const unsigned short TYPE_MARK_RANGE; <br /> const unsigned short TYPE_DELETE_RANGE; <br /> const short TYPE_REPLACE_RANGE non firmato; <br /> attributo tipo breve non firmato; <br /> attributo booleano adjustSeekPosition; <br /> attributo TimeRangeList timeRangeList; <br /> };</p> </td> 
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
   <td><p>interface ReplaceTimeRange { <br /> attributo long begin non firmato; <br /> attributo readonly non firmato long end; <br /> attributo durata non firmata; <br /> attributo non firmato long replaceDuration; <br /> };</p> </td> 
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
   <td><p>Posizione interfaccia { <br /> const short TYPE_MID_ROLL non firmato; <br /> const unsigned short TYPE_PRE_ROLL; <br /> const unsigned short TYPE_POST_ROLL; <br /> const unsigned short TYPE_SERVER_MAP; <br /> const unsigned short TYPE_CUSTOM_RANGE;<br /> attributo readonly non firmato short type; <br /> attributo readonly long time; <br /> la durata dell'attributo readonly; <br /> const unsigned short MODE_DEFAULT; <br /> const unsigned short MODE_INSERT; <br /> const unsigned short MODE_REPLACE; <br /> const unsigned short MODE_DELETE; <br /> const unsigned short MODE_MARK; <br /> const unsigned short MODE_FREE_REPLACE; <br /> attributo readonly non signed short mode; <br /> intervallo TimeRange dell'attributo readonly; <br /> };</p> </td> 
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
   <td><p>interface Opportunity { <br /> readonly attribute DomString id; <br /> posizionamento dell'attributo di sola lettura; <br /> impostazioni dell'attributo di sola lettura Object; <br /> readonly attribute Object customParameters; <br /> }; </p> </td> 
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
   <td><p>interface Reservation { <br /> readonly attribute TimeRange range; <br /> blocco esteso attributo di sola lettura; <br /> }; </p> </td> 
   <td> (Novità per 2.0)</td> 
  </tr> 
 </tbody> 
</table>

### Timeline / TimelineItem / TimelineMarker {#timeline-timelineitem-timelinemarker}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p><strong>Timeline</strong>: interfaccia Timeline  <br /> { attributo readonly TimelineMarkerList timelineMarkers;  <br /> readonly attribute TimelineItemList timelineItems;  <br /> double convertToLocalTime( double time);  <br /> double convertToVirtualTime( double time);  <br /> };</p> </td> 
   <td><p>cronologia interfaccia {<br /> attributo readonly TimelineMarkerList timelineMarkers;<br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p> <strong>TimelineItem</strong>: interface TimelineItem:<br /> TimelineMarker {<br /> readonly attribute long id;  <br /> readonly attribute TimeRange virtualRange;  <br /> readonly attribute TimeRange localRange;  <br /> readonly attributo boolean guardato;  <br /> readonly attribute boolean temporary;  <br /> }; </p> </td> 
   <td>(Novità per 2.0)</td> 
  </tr> 
  <tr> 
   <td><strong>TimelineMarker</strong>: (Nessuna modifica per 2.0)</td> 
   <td><p>interface TimelineMarker {<br /> tempo doppio attributo di sola lettura;<br /> doppia durata attributo di sola lettura;<br /> };</p> </td> 
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
   <td><p>interface AdBreak {<br /> <br /> <br /> <br /> la doppia durata degli attributi di sola lettura;<br /> annunci AdList di attributi di sola lettura;<br /> <br /> <br /> attributo AdInsertionType di sola lettura;<br /> }; </p> </td> 
   <td><p>interface AdBreak {<br /> tempo doppio attributo readonly;<br /> attributo readonly double replaceDuration;<br /> <br /> doppia durata attributo readonly;<br /> attributo AdList adList;<br /> <br /> dati DomString di sola lettura;<br /> <br /> }; </p> </td> 
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
   <td><p> <strong>Annuncio</strong>: ad interfaccia {<br /> readonly attribute AdAsset PrimaryAsset;<br /> readonly attribute AdAssetCompanionAssets;<br /> <br /> readonly attribute double Duration;<br /> readonly attribute DomString id;<br /> const unsigned short ADTYPE_LINEAR = 0;<br /> const unsigned short ADTYPE_NONLINEAR = 1;<br /> <br /> readonly attribute unsigned short adType;<br /> readonly attribute AdInsertionType adInsertionType;  <br /> <br /> readonly attribute boolean click;  <br /> readonly attribute boolean isCustomAdMarker;<br /> }; </p> </td> 
   <td><p>ad interfaccia {<br /> Legonly attribute AdAsset PrimaryAsset;<br /> attributo AdassetList companionAssets;<br /> <br /> Legonly attribute double Duration;<br /> attributo readonly DomString id;<br /> const unsigned short ADTYPE_LINEAR = 0 ;<br /> const unsigned short ADTYPE_NONONLINEAR = 1 ;<br /> <br /> attributo di sola lettura tipo breve non firmato;<br /> attributo di sola lettura AdInsertionType inserimentoType; <br /> utilità di tracciamento oggetti attributo readonly;<br /> <br /> <br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAsset</strong>: (Nessuna modifica per 2.0)</td> 
   <td><p>interface AdAsset {<br /> Legonly attribute DomString id;<br /> readonly attribute double durata;<br /> readonly attribute MediaResource;<br /> readonly attribute AdClick adClick;<br /> readonly attribute Object metadata;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdClick</strong>: (Nessuna modifica per 2.0)</td> 
   <td><p>interface AdClick {<br /> Legonly attribute DomString id;<br /> readonly attribute DomString title;<br /> readonly attribute DomString url;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdList</strong>: (Nessuna modifica per 2.0)</td> 
   <td><p>interface AdList {<br /> Legonly attribute unsigned long length;<br /> getter Ad(unsigned long index);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAssetList</strong>: (Nessuna modifica per 2.0)</td> 
   <td><p>interface AdAssetList {<br /> attributo readonly lunghezza lunga senza segno;<br /> getter AdAsset(indice lungo senza segno);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBannerAsset</strong>: interface AdBannerAsset: AdAsset<br /> {attributo <br /> readonly int width;attributo <br /> readonly int height;<br /> readonly attributo DomString staticUrl;<br /> readonly attribute DomString height;<br /> readonly attribute DomString width;<br /> };</p> </td> 
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
   <td><p> <strong>AdBreakTimelineItem</strong>: interface AdBreakTimelineItem : TimelineItem { attributo  <br /> readonly AdBreak adBreak;  <br /> elementi AdTimelineItemList di attributi readonly;  <br /> }; </p> </td> 
   <td> (Novità per 2.0)</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdTimelineItem</strong>: interface AdTimelineItem : TimelineItem { attributo  <br /> readonly AdBreak adBreak;  <br /> readonly attribute Ad ad;  <br /> }; </p> </td> 
   <td> (Novità per 2.0)</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBreakTimelineItemList</strong>: interface AdBreakTimelineItemList { attributo  <br /> readonly lunghezza lunga senza segno;  <br /> getter AdBreakTimelineItem (indice ng non firmato);  <br /> };</p> </td> 
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
   <td><p>interface AdBreakPolicy {<br /> Legonly attribute short AD_BREAK_POLICY_SKIP;<br /> readonly attribute short AD_BREAK_POLICY_PLAY;<br /> readonly attribute short AD_BREAK_POLICY_REMOVE;<br /> readonly attribute short AD_BREAK_POLICY_REMOVE_AFTER_PLAY;<br /> };</p> </td> 
   <td><p> interface AdPolicyConstants {<br /> attributo readonly short AD_BREAK_POLICY_SKIP;<br /> attributo readonly short AD_BREAK_POLICY_PLAY;<br /> attributo readonly short AD_BREAK_POLICY_REMOVE;<br /> attributo readonly short AD_BREAK_POLICY_REMOVE VE_AFTER_PLAY;}<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p> interface AdBreakWatchedPolicy {<br /> attributo readonly short AD_BREAK_AS_WATCHED_ON_BEGIN;<br /> attributo readonly short AD_BREAK_AS_WATCHED_ON_END;<br /> attributo readonly short AD_BREAK_AS_WATCHED_NEVER;<br /> }; </p> </td> 
   <td><p> ...<br /> attributo readonly short AD_BREAK_AS_WATCHED_ON_BEGIN;<br /> attributo readonly short AD_BREAK_AS_WATCHED_ON_END;<br /> attributo readonly short AD_BREAK_AS_WATCHED_NEVER;<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicy {<br /> Legonly attribute short AD_POLICY_PLAY;<br /> readonly attribute short AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> readonly attribute short AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN; attributo readonly short AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK;<br /> <br /> attributo readonly short AD_POLICY_SKIP_AD_BREAK;<br /> };</p> </td> 
   <td><p> ... <br /> attributo readonly short AD_POLICY_PLAY;<br /> attributo readonly short AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> attributo readonly short AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN;<br /> attributo readonly short AD_POLICY_SKIP_TO_NEXT_AD IN_BREAK;<br /> attributo readonly short AD_POLICY_SKIP_AD_BREAK;<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicyMode {<br /> Legonly attribute short AD_POLICY_MODE_PLAY;<br /> readonly attribute short AD_POLICY_MODE_SEEK;<br /> readonly attribute short AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
   <td><p> ...<br /> {readonly attribute short AD_POLICY_MODE_PLAY;<br /> readonly attribute short AD_POLICY_MODE_SEEK;<br /> readonly attribute short AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicyInfo {<br /> attributo di sola lettura AdBreakTimelineItemList <br /> adBreakTimelineItems;<br /> attributo di sola lettura AdTimelineItem adTimelineItem;<br /> attributo di sola lettura double currentTime;<br /> attributo di sola lettura double searchToTime;<br /> attributo di sola lettura;<br /> readonly attribute short mode; //AdPolicyMode<br /> };</p> </td> 
   <td><p>interface AdPolicyInfo {<br /> attributo di sola lettura AdBreakPlacementList <br /> adBreakPlacements;<br /> attributo di sola lettura Ad;<br /> attributo di sola lettura double currentTime;<br /> attributo di sola lettura double searchToTime;<br /> bitrate di attributi di sola lettura;<br /> modalità di lettura; //AdPolicyMode<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> attributo Object selectPolicyForAdBreakCallbackFunc;<br /> /**<br /> * Ad BreakTimelineItemList selectAdBreaksToPlay(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> attributo Object selectAdBreaksToPlayCallbackFunc;<br /> /**<br /> * AdPolicy selectForSeekInk toAd(AdPolicyInfo adPolicyInfo);<br /> */<br /> attributo Object selectPolicyForSeekIntoAdCallbackFunc; <br /> /**<br /> * AdBreakWatchedPolicy selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> attributo selectWatchedPolicyForAdBreakCallbackFunc;<br /> };</p> </td> 
   <td><p>interface AdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> attributo Object selectPolicyForAdBreakFuncCallback;<br /> /**<br /> * Ad BreakPlacementList selectAdBreaksToPlay(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> attributo Object selectAdBreaksToPlayCallback;<br /> /**<br /> * AdPolicy selectForSeekIntoAd AdPolicyInfo adPolicyInfo);<br /> */<br /> attributo selectPolicyForSeekIntoAdCallback; <br /> /**<br /> * AdBreakAsWatched selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> attributo selectWatchedPolicyForAdBreakCallback;&lt;a 19/&gt; };<br /></p> </td> 
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
   <td><p>interface TimelineOperation { <br /> posizionamento dell'attributo di sola lettura ; <br /> };</p> </td> 
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
   <td><p>interface AdBreakPlacement : TimelineOperation {<br /> attributo di sola lettura AdBreak adBreak;<br /> posizionamento dell'attributo di sola lettura; // Da TimelineOperation<br /> doppio attributo di sola lettura;<br /> doppia durata attributo di sola lettura;<br /> };</p> </td> 
   <td><p>interface AdBreakPlacement {<br /> attributo di sola lettura AdBreak adBreak;<br /> posizionamento dell'attributo di sola lettura;<br /> doppio tempo dell'attributo di sola lettura;<br /> doppia durata dell'attributo di sola lettura;<br /> };</p> </td> 
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
   <td><p>interfaccia AuditudeSettings : AdvertisingMetadata { <br /> attributo DomString zoneId; <br /> attributo DomString mediaId; <br /> attributo DomString defaultMediaId ; <br /> attributo dominio DomString ; <br /> attributo Object targetingInfo ; <br /> attribute Object customParameters ; <br /> attributo booleano creativePackaingEnabled ;<br /> attributo Boolean showStaticBanners ;<br /> };</p> </td> 
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
   <td><p>interface MediaPlayerItemConfig {<br /> attributo ContentFactory adFactory;<br /> attributo StringList subscriptionTags;<br /> <br /> attributo StringList adTags;<br /> <br /> <br /> attributo AdSignalingMode adSignalingMode;<br /> attribute CustomRangeMetadata ;<br /> attributo NetworkConfiguration networkConfiguration;<br /> attributo AdvertisingMetadata advertisingMetadata;<br /> attributo Boolean useHardwareDecoder;<br /> };</p> </td> 
   <td><p>interface MediaPlayerConfig {<br /> <br /> <br /> <br /> attributo StringList adTags;<br /> attributo StringList subscribedTags;<br /> attributo MediaPlayerClientFactory;<br /> <br /> <br /> <br /> <br /> &lt;a1 1/&gt; };<br /></p> </td> 
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
   <td><p>interface ContentFactory {<br /> /*<br /> * AdPolicySelector retrieveAdPolicySelector(<br /> * MediaPlayerItem item);<br /> */<br /> attribute retrieveAdPolicySelectorCallbackFunc;<br /> };</p> </td> 
   <td><p>interface MediaPlayerClientFactory {<br /> /*<br /> * AdPolicySelector retrieveAdPolicySelector(<br /> * Elemento MediaPlayerItem);<br /> */<br /> attributo Object retrieveAdPolicySelectorFunc;<br /> };</p> </td> 
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
   <td><p>interface NetworkConfiguration<br /> {<br /> attributo booleano forceNativeNetworking;<br /> attributo booleano useRedirectUrl;<br /> attributo Object cookieHeader;<br /> attributo booleano readSetCookieHeader;<br /> attributo int masterUpdateInterval; <br /> attributo booleano useCookieHeaderForAllRequests;<br /> attributo in readLimit;<br /> };</p> </td> 
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
| Nessuna modifica per 2.0. | enum DRMAcquireLicenseSettings <br>{<br> const non firmato int FORCE_REFRESH = 0;<br> const unsigned int LOCAL_ONLY = 1;<br> const unsigned int ALLOW_SERVER = 2;<br> }; |
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
   <td><p>interface DRMMetadata<br /> {<br /> Legonly attribute DomString serverUrl;<br /> readonly attribute DomString licenseId;<br /> readonly attribute DRMPolicyArray policy; <br /> };</p> </td> 
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
   <td><p>interfaccia DRMPlaybackTimeWindow {<br /> attributo readonly in riproduzionePeriodInSeconds;<br /> attributo readonly long playStartDate;<br /> attributo readonly long playEndDate;<br /> };</p> </td> 
   <td><p>interface DRMPlaybackTimeWindow {<br /> attributo readonly int pointInSeconds;<br /> attributo readonly int startDate;<br /> attributo readonly int endDate;<br /> };</p> </td> 
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
   <td><p>interface DRMLicense {<br /> byte di Uint8Array di attributi di sola lettura;<br /> attributo di sola lettura DateStartDate;<br /> attributo di sola lettura DateLicenseEndDate;<br /> attributo di sola lettura Date offlineStorageStartDate;<br /> attributo di sola lettura DateOfflineStorageEndDate; <br /> adonly attribute DomString serverUrl;<br /> readonly attribute DomString licenseID;<br /> readonly attribute DomString policyID;<br /> readonly attribute DRMPlaybackTimeWindow PlaybackTimeWindow;<br /> readonly attribute Object customProperties;<br /> }; </p> </td> 
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
   <td><p>interface DRMLicenseDomain {<br /> attributo readonly DomString authenticationDomain;<br /> attributo readonly DRMAuthenticationMethod authenticationMethod; <br /> readonly attribute DomString serverUrl;<br /> };</p> </td> 
   <td><p>interface DRMLicenseDomain {<br /> attributo di sola lettura DomString authDomain;<br /> attributo di sola lettura DRMAuthenticationMethod authMethod; <br /> readonly attribute DomString serverURL;<br /> };</p> </td> 
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
   <td><p>interfaccia DRMPolicy<br /> {<br /> Attributo di sola lettura DomString authenticationDomain;<br /> attributo di sola lettura DRMAuthAuthenticationMethod;<br /> <br /> &lt;a4/&gt; attributo di sola lettura DomString displayName;<br /> attributo di sola lettura DRMLicenseDomain licenseDomain;<br /> };&lt;a6;&lt;a6/&gt;;</p> </td> 
   <td><p>interfaccia DRMPolicy<br /> {<br /> attributo di sola lettura DomString authDomain;<br /> attributo di sola lettura DRMAuthAuthenticationMethod authMethod;<br /> attributo di sola lettura DomString dispName;<br /> attributo di sola lettura DRMLicenseDomain licenseDomain;<br /> };</p> </td> 
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
   <td><p>interface DRMManager : EventTarget {<br /> void acquisitionLicense(metadati DRMMetadata, impostazione <br /> DRMAcquireLicenseSettings, <br /> listener DRMAquireLicenseListener);<br /> void acquisitionPreviewLicense(metadati DRMMetadata, <br /> listener DRMAquireLicenseListener); <br /> void authenticate(metadati DRMMetadata, <br /> URL DomString,<br /> DomString &amp;authenticationDomain, <br /> utente DomString, <br /> password DomString, <br /> listener DRMAuthenticateListener);<br /> &lt;a1 2/&gt; DRMMetadata createMetadataFromBytes(<br /> array Uint8Array, listener DRMErrorListener);<br /> void initialize(listener DRMOperationCompleteListener);<br /> attributo long maxOperationTime;<br /> <br /> void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> boolean forceRefresh, <br /> DRMOperationCompleteListener listener);<br /> void leftLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> listener DRMOperationCompleteListener);<br /> <br /> void resetDRM(DRMOperationCompleteListener listener);<br /> void returnLicense(DomString serverURL, <br /> DomStringlicenseID, &lt;a22 8/&gt; DomString policyID, <br /> booleano commitImmediatamente,<br /> DRMReturnLicenseListener listener);<br /> void setAuthenticationToken(<br /> Metadati DRMMetadata, <br /> DomString authenticationDomain, &lt;a3 token Uint8Array, <br /> listener DRMOperationCompleteListener);<br /> void storeLicenseBytes(Uint8Array licenseBytes, <br /> listener DRMOperationCompleteListener);<br /> };<br /><br /><br /></p> </td> 
   <td><p>interface DRMManager : EventTarget {<br /> void acquisitionLicense(DRMMetadata metadata, <br /> impostazione DRMAcquireLicenseSettings, <br /> EventContext eventContext);<br /> void acquisitionPreviewLicense(DRMMetadata metadata, <br /> EventContext eventContext);<br /> void authenticate(DRMM Metadati metadati, <br /> DomString url,<br /> DomString &amp;authenticationDomain, <br /> DomString user, <br /> DomString password, <br /> EventContext eventContext);<br /> <br /> DRMMetadata createMetadataFromBytes(<br /> Array Uint8Array, EventContext eventContext);<br /> void initialize(EventContext eventContext);<br /> attributo long maxOperationTime;<br /> <br /> void joinLicenseDomain(<br /> DRMLicenseDomain <br /> booleano forceRefresh, <br /> EventContext eventContext);<br /> void leftLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> EventContext eventContext);<br /> &lt;a25/ void DRM(EventContext eventContext);<br /> void returnLicense(DomString serverURL, <br /> DomString licenseID,<br /> DomString policyID, <br /> booleano commitImmediatamente,<br /> EventContext eventContext);&lt;a3 1/&gt; void setAuthenticationToken(<br /> metadati DRMMetadata, <br /> DomString authenticationDomain, <br /> token Uint8Array, <br /> EventContext eventContext);<br /> void storeLicenseBytes(Uint8Array licenseBytes, &lt;aBytes a37/&gt; EventContext eventContext);<br /> };<br /><br /><br /></p> </td> 
  </tr> 
  <tr> 
   <td><p>class DRMErrorListener : <br /> public psdkutils::PSDKInterfaceWithUserData {<br /> public:<br /> virtual void onDRMError(uint32_t major, <br /> uint32_t minor, <br /> const psdkutils: PSDKString&amp; errorString, <br /> const psdkutils::PSDKString&amp; errorServerUrl) = 0;<br /> <br /> protetto:<br /> virtuale ~DRMErrorListener() {}<br /> }</p> </td> 
   <td>Evento / Interfaccia / Descrizione 
    <ul> 
     <li>kEventDRMOperationError<p>/ DRMOperationErrorEvent</p> <p>Quando si verifica un errore durante uno dei metodi asincroni di DRMManger.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>class DRMOperationCompleteListener : <br /> public DRMErrorListener {<br /> public:<br /> virtual void onDRMOperationComplete() = 0;<br /> <br /> protected:<br /> ~DRMOperationCompleteListener() {}<br /> };</p> </td> 
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
   <td><p>class DRMAuthenticateListener : <br /> public DRMErrorListener {<br /> public:<br /> virtual void onAuthenticationComplete(<br /> psdkutils::PSDKImmutableByteArray* <br /> authenticationToken) = 0;<br /> <br /> virtuale:<br /> ~DRMAutheserver ateListener() {}<br /> }</p> </td> 
   <td>Evento / Interfaccia / Descrizione 
    <ul> 
     <li>kEventDRMAuthenticationComplete<p>/ DRMAuthenticationCompleteEvent</p> <p>Quando la chiamata del metodo DRMManager::authenticate ha esito positivo.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>classe DRMAquireLicenseListener: <br /> public DRMErrorListener {<br /> public:<br /> virtual void onLicenseAcquired(const DRMLicense*) = 0;<br /> <br /> protected:<br /> virtual ~DRMAquireLicenseListener() {}<br /> };</p> </td> 
   <td>Evento / Interfaccia / Descrizione 
    <ul> 
     <li>kEventDRMPreviewLicenseAcquisred<p>/ DRMLicenseAcquisredEvent</p> <p>Quando la chiamata del metodo DRMManager::acquisitionPreviewLicense ha esito positivo.</p> </li> 
     <li>kEventDRMLicenseAcquired<p>/ DRMLicenseAcquisredEvent</p> <p>Quando la chiamata del metodo DRMManager::acquisitionLicense ha esito positivo.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>class DRMReturnLicenseListener: <br /> public DRMErrorListener {<br /> public:<br /> virtual void onLicenseReturnComplete(uint32_t numReturn ) = 0;<br /> <br /> protected:<br /> virtuale ~DRMReturnLicenseListener() {}<br /> };</p> </td> 
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
   <td><p>interface MediaResource {<br /> attributo DomString url; <br /> attributo di tipo breve non firmato;<br /> metadati oggetto;<br /> const short TYPE_HLS;<br /> const unsigned short TYPE_HDS;<br /> const unsigned short TYPE_DASH;<br /> const unsigned short TYPE_CUSTOM;<br /> const unsigned short TYPE_UNKNOWN;&lt;a68/&gt; };<br /></p> </td> 
   <td><p>interface MediaResource {<br /> attributo DomString url;<br /> attributo DomString type;<br /> attributo metadata Object;<br /> <br /> <br /> <br /> <br /> <br /> };</p> </td> 
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
   <td><p>interface MediaPlayer : EventTarget<br /> {<br /> void PrepareToPlay( doppia posizione);<br /> void play();<br /> void pause();<br /> void search( doppia posizione);<br /> void searchToLocal( doppia posizione);<br /> void reset();<br /> void release();&lt;a8/ void release CurrentItem(elemento MediaPlayerItem);<br /> void replaceCurrentResource(origine MediaResource, <br /> configurazione MediaPlayerItemConfig); <br /> void suspension();<br /> void restore();<br /> void notificationClick();<br /> <br /> attributo di sola lettura TimeRange PlayRange;<br /> readonly attribute TimeRange searchRange;<br /> <br /> attributo readonly double currentTime;<br /> attributo readonly double localTime;<br /> attributo di sola lettura TimeRange bufferedRange;<br /> attributo di sola lettura DRMManager drmManager;<br /> attributo di sola lettura MediaPlayerItem currentItem;<br /> <br /> // PlayerStatus<br /> &lt;a7/ a8/&gt; const short PLAYER_STATUS_INITIALIZED;<br /> const unsigned short PLAYER_STATUS_PREPARING;<br /> const unsigned short PLAYER_STATUS_PREPARED;<br /> const unsigned short PLAYER_STATUS_PLAYING;&lt;a12/ const unsigned short PLAYER_STATUS_PAUSED;<br /> const unsigned short PLAYER_STATUS_SEEKING;<br /> const unsigned short PLAYER_STATUS_COMPLETE;<br /> const unsigned short PLAYER_STATUS_ERROR;<br /> const short PLAYE non firmato ER_STATUS_RELEASED;<br /> <br /> <br /><br /><br /> lo stato breve non firmato dell'attributo readonly;<br /> <br /> l'attributo volume breve non firmato;<br /> l'attributo ABRControlParameters abrControlParameters;<br /> l'attributo BufferControlParameters bufferControlParameters;<br /> <br /> const unsigned short VISIBLE; //Per visibilità CC<br /> const unsigned short INVISIBIBILE; //Per la visibilità CC<br /> attributo ccVisibility breve;<br /> attributo TextFormat ccStyle;<br /> readonly attribute PlaybackMetrics PlaybackMetricsMetrics;<br /> <br /> attributo double rate;<br /> attributo MediaPlayerView view;<br /> cronologia solo lettura;<br /> attributo double currentTimeUpdateInterval; <br /> // impostazione non supportata per 2.0<br /> };</p> </td> 
   <td><p>interface MediaPlayer : EventTarget<br /> {<br /> void PrepareToPlay( posizione int);<br /> void play();<br /> void pause();<br /> void search( posizione int);<br /> void searchToLocalTime( posizione int);<br /> void reset();<br /> void release();<br /> void replaceCurrentItem(MediaResource source);<br /> <br /> <br /> <br /> <br /> <br /> <br /> &lt;a15/&gt; attributo di sola lettura TimeRange PlayRange;<br /> attributo di sola lettura TimeRange;&lt;a1 7/&gt;<br /> attributo readonly double currentTime;<br /> attributo readonly double localTime;<br /> attributo readonly TimeRange bufferedRange;<br /> attributo readonly DRMManager drmManager;<br /> attributo di sola lettura MediaPlayerItem currentItem;<br /> <br /> // PlayerState<br /> const non firmato PLAT YER_STATE_IDLE;<br /> const short PLAYER_STATE_INITIALIZING;<br /> const unsigned short PLAYER_STATE_INITIALIZED;<br /> const unsigned short PLAYER_STATE_PREPARING;<br /> const unsigned short PLAYER_STATE_PREPARING ED;<br /> const short PLAYER_STATE_PLAYING;<br /> const unsigned short PLAYER_STATE_PAUSED;<br /> const unsigned short PLAYER_STATE_SEEKING;<br /> const unsigned short PLAYER_STATE_COMPLETE;&lt;a1 15/&gt; const short PLAYER_STATE_ERROR;<br /> const unsigned short PLAYER_STATE_RELEASED;<br /> <br /> imposta lo stato breve non firmato di PLAYER_STATUS_SUSPENDED;<br /> attributo di sola lettura;<br /> <br /> attributo volume breve non firmato;<br /> attributo ABRControlParameters abrControlParameters;<br /> attributo BufferControlParametersbufferControlParameters;<br /> <br /> solo lettura non firmata VISIBILE; //Per la visibilità CC<br /> leggete solo la breve invisibile non firmata; //Per visibilità CC<br /> attributo ccVisibility breve non firmato;<br /> attributo TextFormat ccStyle;<br /> attributo readonly PlaybackMetrics PlaybackMetrics;<br /> attributo MediaPlayerConfig mediaPlayerConfig;<br /> bitrate attributo;<br /> attribute MediaPlayerView;<br /> timeline dell'attributo readonly;<br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface MediaPlayerStatus<br /> {<br /> // PlayerStatus<br /> const short PLAYER_STATUS_IDLE non firmato;<br /> const unsigned short PLAYER_STATUS_INITIALIZING;<br /> const unsigned short PLAYER_STATUS_INITIALIZED;<br /> consigned short PLAYER_STATUS_PREPARING;<br /> const short PLAYER_STATUS_PREPARED;<br /> const unsigned short PLAYER_STATUS_PLAYING;<br /> const unsigned short PLAYER_STATUS_PAUSED;<br /> const unsigned short PLAYER_STATUS_SEEKING;&lt;a 11 0/&gt; const short PLAYER_STATUS_COMPLETE;<br /> const unsigned short PLAYER_STATUS_ERROR;<br /> const unsigned short PLAYER_STATUS_RELEASED;<br /> const unsigned short PLAYER_STATUS_SUSPENDED;<br /> };<br /></p> </td> 
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
   <td>adClick<br /> Quando l'utente fa clic su un annuncio.</td> 
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
   <td>audioUpdated<br /> Quando un elemento del lettore multimediale viene aggiornato. Per alcuni flussi che contengono tracce audio rilevabili solo in fase di riproduzione, questo evento viene attivato quando sono disponibili nuove tracce audio.</td> 
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
   <td>PlayRangeUpdated<br /> Quando un elemento del lettore multimediale viene aggiornato. Per i flussi live/lineari, il client deve aggiornare periodicamente la risorsa multimediale per rilevare il nuovo contenuto disponibile. In questo caso, alcune caratteristiche del supporto potrebbero cambiare.</td> 
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
   <td><p>interfaccia ABRControlParameters<br /> {<br /> const unsigned short ABR_POLICY_CONSERVATIVE = 0 ;<br /> const unsigned short ABR_POLICY_MODERATE = 1 ;<br /> const unsigned short ABR_POLICY_AGGRESIVE = 2 ;<br /> <br /> attributo non firmato short abrPolicy;<br /> attributo unsigned int initialBitRate;<br /> attributo int minBitRate;<br /> attributo unsigned int maxBitRate;<br /> const unsigned short DEFAULT_ABR_INITIAL_BITRATE;<br /> const unsigned short DEFAULT_ABR_MIN_MIN_ABR_MIN_TA ITRATE;<br /> const unsigned short DEFAULT_ABR_MAX_BITRATE;<br /> const ABRPolicy DEFAULT_ABR_POLICY;<br /> };</p> </td> 
   <td><p>interfaccia ABRControlParameters<br /> {<br /> const unsigned short ABR_POLICY_CONSERVATIVE = 0 ;<br /> const unsigned short ABR_POLICY_MODERATE = 1 ;<br /> const unsigned short ABR_POLICY_AGGRESIVE = 2 ;<br /> <br /> attributo non firmato short abrPolicy;<br /> attributo unsigned int initialBitRate;<br /> attributo int minBitRate;<br /> attributo unsigned int maxBitRate;<br /> <br /> <br /> <br /> <br /> };</p> </td> 
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
   <td><p>interface BufferControlParameters<br /> {<br /> attributo double initialBufferTime;<br /> attributo double playBufferTime;<br /> const double DEFAULT_INITIAL_BUFFER_TIME;<br /> const double DEFAULT_PLAY_BUFFER_TIME;<br /> };</p> </td> 
   <td><p>interface BufferControlParameters<br /> {<br /> attributo double initialBufferTime;<br /> attributo double playBufferTime;<br /> <br /> <br /> };</p> </td> 
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
   <td><p>interface TextFormat<br /> {<br /> // Color<br /> const unsigned short COLOR_DEFAULT = 0 ;<br /> const unsigned short COLOR_BLACK = 1 ;<br /> const unsigned short COLOR_GRAY = 2 ;<br /> const unsigned short COLOR_WHITE = 3 ;<br /> const COLOR_BRIGHT_WHITE = 4 ;<br /> const short COLOR_DARK_RED = 5 ;<br /> const unsigned short COLOR_RED = 6 ;<br /> const unsigned short COLOR_BRIGHT_RED = 7 ;<br /> const unsigned short COLOR_DARK_GREEN = 8 ;&lt;a CONST unsigned short COLOR_GREEN = 9 ;<br /> const unsigned short COLOR_BRIGHT_GREEN = 10 ;<br /> const unsigned short COLOR_DARK_BLUE = 11 ;<br /> const unsigned short COLOR_BLUE = 12 ;&lt;a a15/&gt; const short COLOR_BRIGHT_BLUE = 13 ;<br /> const short COLOR_DARK_YELLOW = 14 ;<br /> const unsigned short COLOR_DARK_YELLOW = 14 <br /><br /> const unsigned short COLOR_YELLOW = 15 ;<br /> const unsigned short COLOR_BRIGHT_YELLOW = 16 ;<br /> const unsigned short COLOR_DARK_MAGENTA = 17 ;<br /> const unsigned short COLOR_MAGENTA = 18 ;<br /> const unsigned short COLOR_BRIGHT_MAGENTA = 19 ;<br /> const unsigned short COLOR_DARK_CYAN = 20 ;<br /> const unsigned short COLOR_CYAN = 21 ;<br /> const unsigned short COLOR_BRIGHT_CYAN = 22 ;<br /> <br /> Attributo di sola lettura short fontColor;<br /> readonly attribute unsigned short backgroundColor;<br /> readonly attribute unsigned short fillColor;<br /> readonly attribute unsigned short edgeColor;<br /> <br /> // Size<br /> const unsigned short SIZE_DEFAULT = 0 ;&lt;a1 15/&gt; const short SIZE_SMALL = 1 ;<br /> const unsigned short SIZE_MEDIUM = 2 ;<br /> <br /> const unsigned short SIZE_LARGE = 3 ;<br /> <br /> Attributo di sola lettura non firmato di dimensione breve;<br /> <br /> // FontEdge<br /> const unsigned short FONT_EDGE_DEFAULT = 0 ;<br /> const unsigned short FONT_EDGE_NONE = 1 ;<br /> consigned short_FONT EDGE_RAISED = 2 ;<br /> const unsigned short FONT_EDGE_DEPRESSED = 3 ;<br /> const unsigned short FONT_EDGE_UNIFORM = 4 ;<br /> const unsigned short FONT_EDGE_DROP_SHADOW_LEFT = 5 ;<br /> const unsigned short FONT_EDGE_DGE_EDGE_DEPRESSELEFT ROP_SHADOW_RIGHT = 6 ;<br /> attributo di sola lettura non firmato fontEdge;<br /> <br /> // Font<br /> const unsigned short FONT_DEFAULT = 0 ;<br /> const unsigned short FONT_MONOSPACED_WITH_SERIFS = 1 ;&lt;a CONST unsigned short FONT_PROPORTIONAL_WITH_SERIFS = 2 ;<br /> <br /> const unsigned short FONT_MONSPACED_WITHOUT_SERIFS = 3 ;<br /> const unsigned short FONT_CASUAL = 4 ;<br /> const unsigned short FONT_CURSIVE = 5 ;<br /> const unsigned short FONT_SMALL_CAPITALS = 6 ;<br /> attributo readonly unsigned short font;<br /> attributo readonly fontOpacity breve con segno;<br /> attributo readonly short backgroundOpacity senza segno;<br /> attributo readonly unsigned short fillOpacity;<br /> attributo readonly non firmato short DEFAULT_OPACITY;<br /> };</p> </td> 
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
   <td><p>interface MediaPlayerItemLoader:<br /> {<br /> vuoto load(MediaResource, long resourceId,<br /> listener ItemLoaderListener, <br /> MediaPlayerItemConfig config);<br /> void cancel();<br /> attributo di sola lettura MediaPlayerItem currentItem;<br /> };</p> </td> 
   <td>Nuovo per 2.0</td> 
  </tr> 
  <tr> 
   <td><p>interface ItemLoaderListener<br /> {<br /> //onLoadCompleteCallbackFunc(MediaPlayerItem)<br /> var onLoadCompleteCallbackFunc;<br /> //onErrorCallbackFunc(PSDKErrorCode)<br /> var onErrorCallbackFunc; a5/&gt; }<br /></p> </td> 
   <td>Nuovo per 2.0</td> 
  </tr> 
 </tbody> 
</table>

## Modifiche dell&#39;elemento API per le caratteristiche multimediali per 2.0 {#media-characteristics-api-element-changes-for}

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
   <td><p>interface MediaPlayerItem {<br /> risorsa MediaResource con attributi di sola lettura;<br /> attributo readonly long resourceId;<br /> attributo booleano di sola lettura dal vivo;<br /> <br /> attributo di sola lettura booleano hasAlternateAudio;<br /> attributo di sola lettura AudioTrackTracks;<br /> attributo di sola lettura AudioTrack Track;<br /> void selectAudioTrack(AudioTrack track); <br /> <br /> l'attributo di sola lettura booleano haClosedCaptions;<br /> attributo di sola lettura ClosedCaptionsTrackList closedCaptionsTracks;<br /> attributo di sola lettura ClosedCaptionsTrack selectedClosedCaptionsTrack;<br /> void selectClosedCaptionsTrack(&lt;a (13/&gt; brano ClosedCaptionsTrack); <br /> <br /> l'attributo di sola lettura booleano haTimedMetadata;<br /> l'attributo di sola lettura TimedMetadataList timedMetadata;<br /> l'attributo di sola lettura booleano;<br /> <br /> l'attributo di sola lettura è booleano protetto;&lt;a220/&gt; attributo DRMMetadataInfoList drmMetadataInfos;<br /> profili ProfileList per attributi di sola lettura;<br /> attributo di sola lettura Profile selectedProfile;<br /> <br /> attributo booleano di sola letturaPlaySupported;<br /> attributo di sola lettura FloatArrayPlayback disponibile Tassi;<br /> attributo readonly mobile selectedPlaybackRate;<br /> <br /> <br /> attributo di sola lettura MediaPlayer mediaPlayer;<br /> configurazione di MediaPlayerItemConfig;<br /> };<br /><br /></p> </td> 
   <td><p>interface MediaPlayerItem {<br /> risorsa MediaResource con attributi di sola lettura;<br /> attributo readonly long resourceId;<br /> attributo booleano di sola lettura live;<br /> <br /> attributo di sola lettura booleano hasAlternateAudio;<br /> attributo di sola lettura AudioTrack audioTracks;<br /> attributo AudioTrack selectedAudioAudioTrack;<br /> <br /> <br /> l'attributo di sola lettura booleano haClosedCaptions;<br /> attributo di sola lettura ClosedCaptionsTrackList ccTracks;<br /> attributo ClosedCaptionsTrack selectedCCTrack;<br /> <br /> &lt;a14/ <br /> attributo di sola lettura booleano hasTimedMetadata;<br /> attributo di sola lettura TimedMetadataList timedMetadata;<br /> attributo di sola lettura booleano dinamico;<br /> <br /> attributo di sola lettura booleano isProtected;<br /> attributo di sola lettura DRMMetadata drmMetadataInfos;<br /> profili ProfileList per attributi di sola lettura;<br /> <br /> <br /> attributo di sola lettura "booleanPlaySupported";<br /> attributo di sola lettura Int32Array availablePlaybackRates;<br /> a 27/&gt; attributo di sola lettura StringList adTags;<br /> <br /> &lt;a29/&gt; l'attributo di sola lettura MediaPlayer mediaPlayer;<br /> <br /> };<br /><br /></p> </td> 
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
   <td><p>interface Track<br /> {<br /> Legonly attribute DomString name;<br /> readonly attribute DomString language;<br /> readonly attribute boolean default;<br /> readonly attribute boolean autoSelect;<br /> }; </p> </td> 
   <td>Nuovo per 2.0</td> 
  </tr> 
  <tr> 
   <td><p>interface AudioTrack : Track<br /> {<br /> nome DomString dell'attributo readonly; //FromTrack<br /> lingua DomString dell'attributo readonly;//FromTrack<br /> attributo booleano predefinito; // Da Track<br /> l'attributo di sola lettura booleano autoSelect;//FromTrack<br /> <br /> l'attributo di sola lettura non firmato int pid;<br /> };</p> </td> 
   <td><p>interface AudioTrack<br /> {<br /> nome DomString dell'attributo readonly;<br /> lingua DomString dell'attributo readonly; <br /> attributo booleano predefinito;<br /> attributo booleano autoSelect;<br /> attributo booleano di sola lettura forzato;<br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td>Nessuna modifica per 2.0</td> 
   <td><p>interface AudioTrackList<br /> {<br /> attributo readonly lunghezza lunga senza segno;<br /> getter AudioTrack (indice lungo senza segno);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface ClosedCaptionsTrack : Track<br /> {<br /> nome DomString dell'attributo readonly; //FromTrack<br /> lingua DomString dell'attributo readonly;//FromTrack<br /> attributo booleano predefinito; // FromTrack<br /> attributo di sola lettura booleano autoSelect;//FromTrack<br /> <br /> <br /> const unsigned short SERVICE_608_CAPTIONS = 0;<br /> const unsigned short SERVICE_708_CAPTIONS = 1;<br /> const unsigned short SERVICE_WEB_VTT_CAPTIONS = 2;<br /> attributo readonly unsigned short serviceType;<br /> attributo booleano di sola lettura forzato;<br /> };</p> </td> 
   <td><p>interface ClosedCaptionsTrack<br /> {<br /> nome DomString dell'attributo di sola lettura;<br /> lingua DomString dell'attributo di sola lettura;<br /> attributo booleano predefinito di sola lettura;<br /> <br /> <br /> attributo booleano attivo di sola lettura;<br /> <br /> <br /> &lt;a4/&gt; a11/&gt; <br /> };<br /><br /></p> </td> 
  </tr> 
  <tr> 
   <td>Nessuna modifica per 2.0</td> 
   <td><p>interface ClosedCaptionsTrackList<br /> {<br /> Attributo di sola lettura lunghezza non firmata;<br /> getter ClosedCaptionsTrack(indice esteso non firmato);<br /> };</p> </td> 
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
   <td><p>profilo di interfaccia<br /> {<br /> attributo di sola lettura non firmato int width;<br /> attributo di sola lettura non firmato int height;<br /> Legonly attribute unsigned int bitRate;<br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td>ProfileList: Nessuna modifica per 2.0</td> 
   <td><p>interface ProfileList<br /> {<br /> Legonly attribute unsigned long length;<br /> getter Profile(unsigned long index);<br /> };</p> </td> 
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
   <td><p>interface DRMMetadataInfo<br /> { <br /> metadati DRMMetadata dell'attributo readonly;<br /> attributo readonly long prefetchTimestamp;<br /> timeRange dell'attributo readonly;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>DRMMetadataInfoList</strong>: Nessuna modifica per 2.0</td> 
   <td><p>interfaccia DRMMetadataInfoList<br /> {<br /> attributo readonly lunghezza lunga senza segno;<br /> getter DRMMetadataInfo(indice lungo senza segno);<br /> };</p> </td> 
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

## Modifiche dell&#39;elemento API Utility e Helper per per 2.0 {#utility-and-helper-api-element-changes-for}

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
   <td><p>versione dell'interfaccia <br /> {<br /> versione DomString dell'attributo di sola lettura;<br /> descrizione DomString dell'attributo di sola lettura;<br /> attributo di sola lettura esteso;<br /> attributo di sola lettura secondario lungo;<br /> revisione dell'attributo di sola lettura;<br /> versione estesa dell'attributo di sola lettura;<br /> };</p> </td> 
   <td><p>versione dell'interfaccia<br /> {<br /> versione DomString dell'attributo di sola lettura;<br /> descrizione DomString dell'attributo di sola lettura;<br /> attributo di sola lettura DomString major;<br /> attributo di sola lettura DomString minor;<br /> revisione DomString di sola lettura;<br /> attributo di sola lettura DomStringVersion;<br /> ;</p> </td> 
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
   <td><p>interface TimeRange<br /> {<br /> l'attributo readonly unsigned long begin;<br /> l'attributo readonly non signed long end;<br /> l'attributo readonly non signed long length;<br /> };</p> </td> 
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
   <td><p>l'interfaccia QOSProvider<br /> {<br /> void attachmentMediaPlayer(MediaPlayer player);<br /> void detachMediaPlayer();<br /> <br /> attributo di sola lettura DeviceInformation deviceInformation;<br /> readonly attribute PlaybackInformation PlaybackInformation;<br /> };</p> </td> 
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
   <td><p>deviceInformation<br /> {<br /> Legonly attribute DomString os;<br /> <br /> <br /> <br /> Legonly attribute DomString id;<br /> readonly attribute int densityDPI;<br /> readonly attribute int heightPixels;<br /> readonly attribute int widthPixels;<br /> attributo readonly booleano searchToKeyFrame;<br /> };</p> </td> 
   <td><p>interface DeviceInformation<br /> {<br /> Legonly attribute DomString os;<br /> readonly attribute int sdk;<br /> readonly attribute DomString model;<br /> readonly attribute DomString Manufacturers;<br /> readonly attribute DomString id;<br /> readonly attribute int densityDPI;<br /> readonly attributo int heightPixels;<br /> attributo readonly int widthPixels;<br /> <br /> };</p> </td> 
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
   <td><p>interface LoadInfo<br /> {<br /> Legonly attribute DomString url;<br /> readonly attribute int size;<br /> readonly attribute double downloadDuration;<br /> readonly attribute int periodIndex;<br /> readonly attribute double mediaDuration;<br /> readonly attribute short TRACK_TYPE_FRAGMENT;<br /> readonly attribute short attributo short TRACK_TYPE_TRACK;<br /> readonly attributo short TRACK_TYPE_MANIFEST;<br /> tipo di attributo di sola lettura;<br /> attributo di sola lettura DomString trackName;<br /> attributo di sola lettura DomString trackType;<br /> attributo di sola lettura trackIndex;&lt;a1 3/&gt; };<br /></p> </td> 
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
   <td><p>interface View<br /> {<br /> Legonly attribute unsigned short x;<br /> readonly attribute unsigned short y;<br /> readonly attribute unsigned short width;<br /> readonly attribute unsigned short height;<br /> void setSize(unsigned short width, unsigned short height);<br /> void setPos(unsigned short, unsigned short width) x, unsigned short y);<br /> }<br /></p> </td> 
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
   <td><p>interface PlaybackInformation<br /> {<br /> Legonly attribute double timeToFirstByte;<br /> readonly attribute double timeToLoad;<br /> readonly attribute double timeToStart;<br /> readonly attribute double timeToFail;<br /> readonly attribute int totalSecondsPlayed;<br /> readonly attribute only totalSecondsSpent;<br /> attributo readonly double frameRate;<br /> attributo readonly int dropFrameCount;<br /> attributo readonly int perceedBandwidth;<br /> attributo readonly int bitrate;<br /> readonly attribute double bufferTime;<br /> readonly attribute bufferLength; a13/&gt; attributo readonly in emptyBufferCount;<br /> readonly attributo double bufferingTime;<br /> };<br /></p> </td> 
   <td><p>interface PlaybackInformation<br /> {<br /> Legonly attribute double timeToFirstByte;<br /> readonly attribute double timeToLoad;<br /> readonly attribute double timeToStart;<br /> readonly attribute double timeToFail;<br /> readonly attribute int totalSecondsPlayed;<br /> readonly attribute only totalSecondsSpent;<br /> attributo readonly double frameRate;<br /> attributo readonly int dropFrameCount;<br /> <br /> attributo readonly int bitrate;<br /> attributo readonly double bufferTime;<br /> attributo readonly int bufferLength;<br /> attributo readonly emptyBufferCount;<br /> readonly attribute double bufferingTime;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

## Risorse utili {#helpful-resources}

* Consulta la documentazione completa della guida in linea alla pagina [ Informazioni e supporto per Adobe Primetime](https://helpx.adobe.com/support/primetime.html).
