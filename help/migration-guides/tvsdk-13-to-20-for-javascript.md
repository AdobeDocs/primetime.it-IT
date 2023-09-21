---
title: Conversione TVSDK - Da 1.3 a 2.0 Per JavaScript
description: Molte firme di metodi e nomi di elementi API sono stati modificati per la versione 2.0. Esamina queste tabelle per visualizzare tutti i dettagli di modifica dell’API.
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: migration
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '5034'
ht-degree: 0%

---

# Conversione TVSDK - Da 1.3 a 2.0 Per JavaScript {#tvsdk-conversion-to-for-javascript}

Molte firme di metodi e nomi di elementi API sono stati modificati per la versione 2.0. Esamina queste tabelle per visualizzare tutti i dettagli di modifica dell’API.

## Implementare funzioni di callback in JavaScript {#implement-callback-functions-in-javascript}

I commenti nella documentazione del metodo suggeriscono la firma per i callback da implementare.

Per JavaScript, la sintassi API si basa sull’ID web. Per un&#39;interfaccia TVSDK, i nomi dei metodi sono denominati *methodName*(). Per i metodi da implementare tramite l&#39;applicazione, un attributo di lettura/scrittura denominato *methodName* CallbackFunc viene aggiunto all&#39;interfaccia e l&#39;applicazione deve impostarlo in modo che punti a una funzione che implementa il metodo. Ad esempio:

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

## Modifiche all’elemento API del flusso di lavoro Advertising per 2.0 {#advertising-workflow-api-element-changes-for}

Queste tabelle confrontano gli elementi API del flusso di lavoro pubblicitario per TVSDK JavaScript tra le versioni 1.3 e 2.0.

Tabelle in questo argomento:

* TimedMetadata
* AdSignalingMode
* AdvertisingMetadata
* CustomRangeMetadata
* ReplaceTimeRange
* Posizione
* opportunità
* Prenotazione
* Timeline/TimelineItem/TimelineMarker
* AdBreak
* Ad/AdAsset/AdClick/AdList/AdAssetList/AdBannerAsset
* AdBreakTimelineItem / AdTimelineItem
* AdBreakPolicy/AdBreakWatchedPolicy/AdPolicy/AdPolicyMode/AdPolicyInfo/AdPolicySelector
* OperazioneTimeline
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
   <td><p> <strong>TimedMetadata</strong>: Interfaccia TimedMetadata {<br /> const short METADATA_TYPE_TAG senza segno = 0 ; <br /> const short METADATA_TYPE_ID3 senza segno = 1 ; <br /> attributo readonly senza segno di tipo breve; <br /> attributo di sola lettura long time;<br /> attributo di sola lettura ID DomString;<br /> attributo di sola lettura DomString name;<br /> contenuto DomString dell’attributo readonly; <br /> attributo di sola lettura Metadati oggetto;<br /> }; </p> </td> 
   <td><p>Interfaccia TimedMetadata {<br /> const short METADATA_TYPE_TAG senza segno = 0 ;<br /> const short METADATA_TYPE_ID3 senza segno = 1 ;<br /> attributo readonly short metadataType senza segno;<br /> attributo di sola lettura long time;<br /> id lungo attributo readonly;<br /> attributo di sola lettura DomString name;<br /> <br /> attributo di sola lettura Metadati oggetto;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>ElencoMetadatiTemporizzati</strong>: (nessuna modifica per 2.0)</td> 
   <td><p>Interfaccia TimedMetadataList {<br /> attributo di sola lettura long length senza segno;<br /> getter TimedMetadata(unsigned long index);<br /> };</p> </td> 
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
   <td><p>Interfaccia AdSignalingMode { <br /> const short MODE_DEFAULT senza segno, <br /> const short MODE_MANIFEST_CUES senza segno, <br /> const short MODE_SERVER_MAP senza segno, <br /> const short MODE_CUSTOM_RANGES senza segno <br /> };</p> </td> 
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
   <td><p>Interfaccia AdvertisingMetadata { <br /> attributo ModalitàAdSignaling; <br /> attributo AdBreakWatchedPolicy adBreakAsWatched; <br /> attributo booleano livePreroll; <br /> attribute booleano delayAdLoading ; <br /> };</p> </td> 
   <td>Questa funzionalità è stata fornita da<p>Chiavi metadati::ADVERTISING_METADATA</p> chiave.</td> 
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
   <td><p>Interfaccia CustomRangeMetadata { <br /> const short TYPE_MARK_RANGE senza segno; <br /> const short TYPE_DELETE_RANGE senza segno; <br /> const short TYPE_REPLACE_RANGE senza segno; <br /> attributo di tipo short senza segno; <br /> attributo booleano adjustSeekPosition; <br /> attributo TimeRangeList timeRangeList; <br /> };</p> </td> 
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
   <td><p>Interfaccia ReplaceTimeRange { <br /> attributo long begin senza segno; <br /> attributo di sola lettura long end senza segno; <br /> attributo di lunga durata senza segno; <br /> attributo long replaceDuration senza segno; <br /> };</p> </td> 
   <td>(Novità per 2.0)</td> 
  </tr> 
 </tbody> 
</table>

### Posizione {#placement}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>Posizionamento interfaccia { <br /> const short TYPE_MID_ROLL senza segno; <br /> const short TYPE_PRE_ROLL senza segno; <br /> const short TYPE_POST_ROLL senza segno; <br /> const short TYPE_SERVER_MAP senza segno; <br /> const short TYPE_CUSTOM_RANGE senza segno;<br /> attributo readonly senza segno di tipo breve; <br /> attributo di sola lettura long time; <br /> attributo di sola lettura di lunga durata; <br /> const short MODE_DEFAULT senza segno; <br /> const short MODE_INSERT senza segno; <br /> const short MODE_REPLACE senza segno; <br /> const short MODE_DELETE senza segno; <br /> const short MODE_MARK senza segno; <br /> const short MODE_FREE_REPLACE senza segno; <br /> attributo readonly in modalità breve senza segno; <br /> attributo di sola lettura Intervallo di tempo; <br /> };</p> </td> 
   <td>(Novità per 2.0)</td> 
  </tr> 
 </tbody> 
</table>

### opportunità {#opportunity}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>Opportunità di interfaccia { <br /> attributo di sola lettura ID DomString; <br /> posizione posizionamento di posizionamento attributo di sola lettura; <br /> attributo di sola lettura Impostazioni oggetto; <br /> attributo di sola lettura Object customParameters; <br /> }; </p> </td> 
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
   <td><p>Prenotazione interfaccia { <br /> attributo di sola lettura Intervallo di tempo; <br /> proprietà long hold dell'attributo di sola lettura; <br /> }; </p> </td> 
   <td> (Novità per 2.0)</td> 
  </tr> 
 </tbody> 
</table>

### Timeline/TimelineItem/TimelineMarker {#timeline-timelineitem-timelinemarker}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p><strong>Timeline</strong>: sequenza temporale dell’interfaccia <br /> { attributo di sola lettura TimelineMarkerList timelineMarkers; <br /> attributo di sola lettura TimelineItemList timelineItems; <br /> double convertToLocalTime( ora doppia); <br /> double convertToVirtualTime( tempo doppio); <br /> };</p> </td> 
   <td><p>Interfaccia Timeline {<br /> attributo di sola lettura TimelineMarkerList timelineMarkers;<br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p> <strong>TimelineItem</strong>: elemento sequenza temporale interfaccia :<br /> TimelineMarker {<br /> id lungo attributo readonly; <br /> attributo di sola lettura TimeRange virtualRange; <br /> attributo di sola lettura TimeRange localRange; <br /> attributo di sola lettura booleano guardato; <br /> attributo di sola lettura booleano temporaneo; <br /> }; </p> </td> 
   <td>(Novità per 2.0)</td> 
  </tr> 
  <tr> 
   <td><strong>IndicatoreTimeline</strong>: (nessuna modifica per 2.0)</td> 
   <td><p>Interfaccia TimelineMarker {<br /> attributo di sola lettura double time;<br /> attributo di sola lettura a doppia durata;<br /> };</p> </td> 
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
   <td><p>Interfaccia AdBreak {<br /> <br /> <br /> <br /> attributo di sola lettura a doppia durata;<br /> annunci AdList di attributi di sola lettura;<br /> <br /> <br /> attributo di sola lettura AdInsertionType insertionType;<br /> }; </p> </td> 
   <td><p>Interfaccia AdBreak {<br /> attributo di sola lettura double time;<br /> attributo di sola lettura double replaceDuration;<br /> <br /> attributo di sola lettura a doppia durata;<br /> attributo readonly AdList adList;<br /> <br /> dati DomString dell’attributo readonly;<br /> <br /> }; </p> </td> 
  </tr> 
 </tbody> 
</table>

### Ad/AdAsset/AdClick/AdList/AdAssetList/AdBannerAsset {#ad-adasset-adclick-adlist-adassetlist-adbannerasset}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p> <strong>Annuncio</strong>: annuncio interfaccia {<br /> attributo di sola lettura AdAsset primaryAsset;<br /> attributo di sola lettura AdAssetList companionAssets;<br /> <br /> attributo di sola lettura a doppia durata;<br /> attributo di sola lettura ID DomString;<br /> const short senza segno ADTYPE_LINEAR = 0 ;<br /> const short senza segno ADTYPE_NONLINEAR = 1 ;<br /> <br /> attributo readonly short adType senza segno;<br /> attributo di sola lettura AdInsertionType adInsertionType; <br /> <br /> attributo di sola lettura booleano cliccabile; <br /> attributo booleano di sola lettura isCustomAdMarker;<br /> }; </p> </td> 
   <td><p>Annuncio interfaccia {<br /> attributo di sola lettura AdAsset primaryAsset;<br /> attributo di sola lettura AdAssetList companionAssets;<br /> <br /> attributo di sola lettura a doppia durata;<br /> attributo di sola lettura ID DomString;<br /> const short senza segno ADTYPE_LINEAR = 0 ;<br /> const short senza segno ADTYPE_NONLINEAR = 1 ;<br /> <br /> attributo readonly senza segno di tipo breve;<br /> attributo di sola lettura AdInsertionType insertionType; <br /> attributo di sola lettura Tracker di oggetti;<br /> <br /> <br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAsset</strong>: (nessuna modifica per 2.0)</td> 
   <td><p>Interfaccia di AdAsset {<br /> attributo di sola lettura ID DomString;<br /> attributo di sola lettura a doppia durata;<br /> attributo di sola lettura MediaResource;<br /> attributo di sola lettura AdClick adClick;<br /> attributo di sola lettura Metadati oggetto;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdClick</strong>: (nessuna modifica per 2.0)</td> 
   <td><p>Interfaccia AdClick {<br /> attributo di sola lettura ID DomString;<br /> attributo di sola lettura DomString title;<br /> URL DomString di attributo readonly;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdList</strong>: (nessuna modifica per 2.0)</td> 
   <td><p>Interfaccia AdList {<br /> attributo di sola lettura long length senza segno;<br /> getter Ad(unsigned long index);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAssetList</strong>: (nessuna modifica per 2.0)</td> 
   <td><p>Interfaccia AdAssetList {<br /> attributo di sola lettura long length senza segno;<br /> getter AdAsset(indice lungo senza segno);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBannerAsset</strong>: interfaccia AdBannerAsset : AdAsset<br /> {<br /> attributo readonly int width;<br /> attributo readonly int height;<br /> attributo di sola lettura DomString staticUrl;<br /> attributo di sola lettura DomString height;<br /> attributo readonly larghezza DomString;<br /> };</p> </td> 
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
   <td><p> <strong>AdBreakTimelineItem</strong>: interface AdBreakTimelineItem : TimelineItem { <br /> attributo di sola lettura AdBreak adBreak; <br /> attributi di sola lettura Elementi AdTimelineItemList; <br /> }; </p> </td> 
   <td> (Novità per 2.0)</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdTimelineItem</strong>: interface AdTimelineItem : TimelineItem { <br /> attributo di sola lettura AdBreak adBreak; <br /> attributo readonly Ad ad; <br /> }; </p> </td> 
   <td> (Novità per 2.0)</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBreakTimelineItemList</strong>: interfaccia AdBreakTimelineItemList { <br /> attributo di sola lettura long length senza segno; <br /> getter AdBreakTimelineItem (indice di log non firmato); <br /> };</p> </td> 
   <td> (Novità per 2.0)</td> 
  </tr> 
 </tbody> 
</table>

### AdBreakPolicy/AdBreakWatchedPolicy/AdPolicy/AdPolicyMode/AdPolicyInfo/AdPolicySelector {#adbreakpolicy-adbreakwatchedpolicy-adpolicy-adpolicymode-adpolicyinfo-adpolicyselector}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>Interfaccia AdBreakPolicy {<br /> attributo di sola lettura short AD_BREAK_POLICY_SKIP;<br /> attributo di sola lettura short AD_BREAK_POLICY_PLAY;<br /> attributo di sola lettura short AD_BREAK_POLICY_REMOVE;<br /> attributo di sola lettura short AD_BREAK_POLICY_REMOVE_AFTER_PLAY;<br /> };</p> </td> 
   <td><p> Interfaccia AdPolicyConstants {<br /> attributo di sola lettura short AD_BREAK_POLICY_SKIP;<br /> attributo di sola lettura short AD_BREAK_POLICY_PLAY;<br /> attributo di sola lettura short AD_BREAK_POLICY_REMOVE;<br /> attributo di sola lettura short AD_BREAK_POLICY_REMOVE_AFTER_PLAY;}<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p> Interfaccia AdBreakWatchedPolicy {<br /> attributo di sola lettura short AD_BREAK_AS_WATCHED_ON_BEGIN;<br /> attributo di sola lettura short AD_BREAK_AS_WATCHED_ON_END;<br /> attributo di sola lettura short AD_BREAK_AS_WATCHED_NEVER;<br /> }; </p> </td> 
   <td><p> ...<br /> attributo di sola lettura short AD_BREAK_AS_WATCHED_ON_BEGIN;<br /> attributo di sola lettura short AD_BREAK_AS_WATCHED_ON_END;<br /> attributo di sola lettura short AD_BREAK_AS_WATCHED_NEVER;<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>Interfaccia AdPolicy {<br /> attributo di sola lettura short AD_POLICY_PLAY;<br /> attributo di sola lettura short AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> attributo readonly short AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN; attributo readonly short AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK;<br /> <br /> attributo di sola lettura short AD_POLICY_SKIP_AD_BREAK;<br /> };</p> </td> 
   <td><p> ... <br /> attributo di sola lettura short AD_POLICY_PLAY;<br /> attributo di sola lettura short AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> attributo di sola lettura short AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN;<br /> attributo di sola lettura short AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK;<br /> attributo di sola lettura short AD_POLICY_SKIP_AD_BREAK;<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>Interfaccia AdPolicyMode {<br /> attributo di sola lettura short AD_POLICY_MODE_PLAY;<br /> attributo di sola lettura short AD_POLICY_MODE_SEEK;<br /> attributo di sola lettura short AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
   <td><p> ...<br /> {readonly attribute short AD_POLICY_MODE_PLAY;<br /> attributo di sola lettura short AD_POLICY_MODE_SEEK;<br /> attributo di sola lettura short AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>Interfaccia AdPolicyInfo {<br /> attributo readonly AdBreakTimelineItemList <br /> adBreakTimelineItems;<br /> attributo di sola lettura AdTimelineItem adTimelineItem;<br /> attributo di sola lettura double currentTime;<br /> attributo di sola lettura double seekToTime;<br /> attributo di sola lettura double rate;<br /> attributo di sola lettura modalità breve; //AdPolicyMode<br /> };</p> </td> 
   <td><p>Interfaccia AdPolicyInfo {<br /> attributo readonly AdBreakPlacementList <br /> adBreakPlacements;<br /> attributo readonly Ad ad;<br /> attributo di sola lettura double currentTime;<br /> attributo di sola lettura double seekToTime;<br /> attributo di sola lettura double rate;<br /> attributo di sola lettura modalità breve; //AdPolicyMode<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>Interfaccia di AdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectPolicyForAdBreak(<br /> * AdPolicyInfo (adPolicyInfo);<br /> */<br /> attribute Object selectPolicyForAdBreakCallbackFunc;<br /> /**<br /> * SelectAdBreakTimelineItemList di AdBreaksToPlay(<br /> * AdPolicyInfo (adPolicyInfo);<br /> */<br /> attribute Object selectAdBreaksToPlayCallbackFunc;<br /> /**<br /> * AdPolicy selectPolicyForSeekIntoAd(AdPolicyInfo adPolicyInfo);<br /> */<br /> attribute Object selectPolicyForSeekIntoAdCallbackFunc; <br /> /**<br /> * SelectWatchedPolicyForAdBreak() di AdBreakPolicy di AdBreak<br /> * AdPolicyInfo (adPolicyInfo);<br /> */<br /> attribute Object selectWatchedPolicyForAdBreakCallbackFunc;<br /> };</p> </td> 
   <td><p>Interfaccia di AdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectPolicyForAdBreak(<br /> * AdPolicyInfo (adPolicyInfo);<br /> */<br /> attribute Oggetto selectPolicyForAdBreakFuncCallback;<br /> /**<br /> * SelectAdBreakPlacementListAdBreaksToPlay(<br /> * AdPolicyInfo (adPolicyInfo);<br /> */<br /> attribute Object selectAdBreaksToPlayCallback;<br /> /**<br /> * AdPolicy selectPolicyForSeekIntoAd(AdPolicyInfo adPolicyInfo);<br /> */<br /> attribute Object selectPolicyForSeekIntoAdCallback; <br /> /**<br /> * SelectWatchedPolicyForAdBreak( di AdBreakAsWatched<br /> * AdPolicyInfo (adPolicyInfo);<br /> */<br /> attribute Object selectWatchedPolicyForAdBreakCallback;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### OperazioneTimeline {#timelineoperation}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>Interfaccia TimelineOperation { <br /> posizione posizionamento attributo di sola lettura ; <br /> };</p> </td> 
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
   <td><p>interface AdBreakPlacement : TimelineOperation {<br /> attributo di sola lettura AdBreak adBreak;<br /> posizione posizionamento attributo di sola lettura; // From TimelineOperation<br /> attributo di sola lettura double time;<br /> attributo di sola lettura a doppia durata;<br /> };</p> </td> 
   <td><p>Interfaccia AdBreakPlacement {<br /> attributo di sola lettura AdBreak adBreak;<br /> posizione posizionamento di posizionamento attributo di sola lettura;<br /> attributo di sola lettura double time;<br /> attributo di sola lettura a doppia durata;<br /> };</p> </td> 
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
   <td><p>Interfaccia AuditudeSettings : AdvertisingMetadata { <br /> attributo DomString zoneId; <br /> attributo mediaId DomString; <br /> attributo DomString defaultMediaId ; <br /> attributo dominio DomString ; <br /> attribute Oggetto targettingInfo ; <br /> attribute Object customParameters ; <br /> attributo Boolean creativePackagingEnabled ;<br /> attributo Boolean showStaticBanners ;<br /> };</p> </td> 
   <td>La funzionalità è stata fornita dalla chiave MetadataKeys::AUDITUDE_METADATA_KEY.</td> 
  </tr> 
 </tbody> 
</table>

## Modifiche all’elemento API di personalizzazione per 2.0 {#customization-api-element-changes-for}

Queste tabelle confrontano gli elementi API di personalizzazione per JavaScript TVSDK tra le versioni 1.3 e 2.0.

Tabelle in questo argomento:

* MediaPlayerItemConfig
* ContentFactory
* NetworkConfiguration

### MediaPlayerItemConfig {#mediaplayeritemconfig}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface MediaPlayerItemConfig {<br /> attributo ContentFactory adFactory;<br /> attributo StringList subscribeTags;<br /> <br /> attributo StringList adTags;<br /> <br /> <br /> attributo AdSignalingMode adSignalingMode;<br /> attributo CustomRangeMetadata customRangeMetadata;<br /> attributo NetworkConfiguration networkConfiguration;<br /> attribuire AdvertisingMetadata advertisingMetadata;<br /> attributo Boolean useHardwareDecoder;<br /> };</p> </td> 
   <td><p>interface MediaPlayerConfig {<br /> <br /> <br /> <br /> attributo StringList adTags;<br /> attributo StringList subscscriptionsTags;<br /> attributo MediaPlayerClientFactory clientFactory;<br /> <br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### ContentFactory {#contentfactory}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>Interfaccia ContentFactory {<br /> /*<br /> * AdPolicySelector retrieveAdPolicySelector(<br /> * elemento MediaPlayerItem);<br /> */<br /> attributo Object retrieveAdPolicySelectorCallbackFunc;<br /> };</p> </td> 
   <td><p>Interfaccia MediaPlayerClientFactory {<br /> /*<br /> * AdPolicySelector retrieveAdPolicySelector(<br /> * elemento MediaPlayerItem);<br /> */<br /> attributo Object retrieveAdPolicySelectorFunc;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### NetworkConfiguration {#networkconfiguration}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interfaccia NetworkConfiguration<br /> {<br /> attributo booleano forceNativeNetworking;<br /> attributo booleano useRedirectedUrl;<br /> attributo Object cookieHeader;<br /> attributo booleano readSetCookieHeader;<br /> attributo int masterUpdateInterval; <br /> attributo booleano useCookieHeaderForAllRequests;<br /> attributo int readLimit;<br /> };</p> </td> 
   <td>Nella versione 1.3, alcune di queste funzionalità erano fornite da MetadataKeys</td> 
  </tr> 
 </tbody> 
</table>

## Modifiche all’elemento dell’API DRM per 2.0 {#drm-api-element-changes-for}

Queste tabelle confrontano gli elementi API DRM per JavaScript TVSDK tra le versioni 1.3 e 2.0.

Tabelle in questo argomento:

* Inizializzazione flusso di lavoro DRM
* DRMAcquireLicenseSettings/DRMAuthenticationMethod
* Metadati DRM
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
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td>L’applicazione deve chiamare AdobePSDK.beginDRMWorkflow per avviare il flusso di lavoro DRM. Senza questa chiamata, i video DRM non verranno riprodotti.<p>Interfaccia di AdobePSDK<br /> {<br /> void beginDRMWorkFlow(<br /> DomString appStoratePath <br /> DomString publisherId, <br /> AppId DomString, <br /> AppVersion DomString, <br /> booleano privacyModeOn);<br /> };</p> </td> 
   <td>L'inizializzazione è stata eseguita internamente e non è stata richiesta alcuna chiamata esplicita.</td> 
  </tr> 
 </tbody> 
</table>

### DRMAcquireLicenseSettings/DRMAuthenticationMethod {#drmacquirelicensesettings-drmauthenticationmethod}

| API 2.0 | API 1.3 |
|--- |--- |
| **DRMAcquireLicenseSettings** |  |
| Nessuna modifica per 2.0. | enum DRMAcquireLicenseSettings <br>{<br> const unsigned int FORCE_REFRESH = 0;<br> const unsigned int LOCAL_ONLY = 1;<br> const unsigned int ALLOW_SERVER = 2;<br> }; |
| **DRMAuthenticationMethod** |  |
| Nessuna modifica per 2.0. | enum DRMAuthenticationMethod <br>{<br> const unsigned int UNKNOWN = 0;<br> const unsigned int ANONYMOUS = 1;<br> const unsigned int USERNAME_AND_PASSWORD = 2;<br> } |

### Metadati DRM {#drmmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td>Nessuna modifica per 2.0.</td> 
   <td><p>interfaccia DRMMetadata<br /> {<br /> attributo di sola lettura serverUrl DomString;<br /> attributo di sola lettura licenseId DomString;<br /> criteri DRMPolicyArray di sola lettura; <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMPlaybackTimeWindow {#drmplaybacktimewindow}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interfaccia DRMPlaybackTimeWindow {<br /> attributo readonly in playbackPeriodInSeconds;<br /> attributo di sola lettura long playbackStartDate;<br /> attributo di sola lettura long playbackEndDate;<br /> };</p> </td> 
   <td><p>interfaccia DRMPlaybackTimeWindow {<br /> attributo readonly int periodInSeconds;<br /> attributo readonly int startDate;<br /> attributo readonly int endDate;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMLicense {#drmlicense}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td>Nessuna modifica per 2.0.</td> 
   <td><p>interfaccia DRMLicense {<br /> attributo di sola lettura Uint8Array byte;<br /> attributo di sola lettura Date licenseStartDate;<br /> attributo di sola lettura Date licenseEndDate;<br /> attributo di sola lettura Date offlineStorageStartDate;<br /> attributo di sola lettura Date offlineStorageEndDate; <br /> attributo di sola lettura serverUrl DomString;<br /> attributo di sola lettura licenseID DomString;<br /> attributo readonly DomString policyID;<br /> attributo di sola lettura DRMPlaybackTimeWindow playbackTimeWindow;<br /> attributo di sola lettura Object customProperties;<br /> }; </p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMLicenseDomain {#drmlicensedomain}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interfaccia DRMLicenseDomain {<br /> attributo di sola lettura DomString authenticationDomain;<br /> attributo readonly DRMAuthenticationMethod authenticationMethod; <br /> attributo di sola lettura serverUrl DomString;<br /> };</p> </td> 
   <td><p>interfaccia DRMLicenseDomain {<br /> attributo di sola lettura DomString authDomain;<br /> attributo readonly DRMAuthenticationMethod authMethod; <br /> attributo di sola lettura DomString serverURL;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMPolicy {#drmpolicy}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interfaccia DRMPolicy<br /> {<br /> attributo di sola lettura DomString authenticationDomain;<br /> attributo readonly DRMAuthenticationMethod authenticationMethod;<br /> <br /> attributo di sola lettura DomString displayName;<br /> attributo di sola lettura DRMLicenseDomain licenseDomain;<br /> };</p> </td> 
   <td><p>interfaccia DRMPolicy<br /> {<br /> attributo di sola lettura DomString authDomain;<br /> attributo readonly DRMAuthenticationMethod authMethod;<br /> attributo di sola lettura DomString dispName;<br /> attributo di sola lettura DRMLicenseDomain licenseDomain;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMManager {#drmmanager}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface DRMManager : EventTarget {<br /> void acquisitionLicense(DRMMetadata metadata, <br /> impostazione DRMAcquireLicenseSettings, <br /> DRMAquireLicenseListener listener);<br /> void acquisitionPreviewLicense(DRMMetadata metadata, <br /> DRMAquireLicenseListener listener);<br /> void authenticate (metadati DRMetadata), <br /> URL DomString,<br /> DomString &amp;authenticationDomain <br /> Utente DomString, <br /> Password DomString, <br /> DRMAuthenticateListener listener);<br /> <br /> DRMMetadata createMetadataFromBytes(<br /> Array di unità, listener DRMErrorListener);<br /> void initialize(DRMOperationCompleteListener);<br /> attributo long maxOperationTime;<br /> <br /> void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain <br /> forceRefresh booleano, <br /> DRMOperationCompleteListener);<br /> void leaveLicenseDomain(<br /> DRMLicenseDomain licenseDomain <br /> DRMOperationCompleteListener);<br /> <br /> void resetDRM(DRMOperationCompleteListener listener);<br /> void returnLicense(DomString serverURL, <br /> ID licenza DomString, <br /> ID criterio DomString, <br /> commitImmediately booleano,<br /> DRMRreturnLicenseListener listener);<br /> void setAuthenticationToken(<br /> metadati DRMM, <br /> DomString authenticationDomain <br /> Token Uint8Array, <br /> DRMOperationCompleteListener);<br /> void storeLicenseBytes(Uint8Array licenseBytes, <br /> DRMOperationCompleteListener);<br /> };</p> </td> 
   <td><p>interface DRMManager : EventTarget {<br /> void acquisitionLicense(DRMMetadata metadata, <br /> impostazione DRMAcquireLicenseSettings, <br /> EventContext (eventContext);<br /> void acquisitionPreviewLicense(DRMMetadata metadata, <br /> EventContext (eventContext);<br /> void authenticate (metadati DRMetadata), <br /> URL DomString,<br /> DomString &amp;authenticationDomain <br /> Utente DomString, <br /> Password DomString, <br /> EventContext (eventContext);<br /> <br /> DRMMetadata createMetadataFromBytes(<br /> Matrice Uint8Array, EventContext (eventContext);<br /> void initialize(EventContext eventContext);<br /> attributo long maxOperationTime;<br /> <br /> void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain <br /> forceRefresh booleano, <br /> EventContext (eventContext);<br /> void leaveLicenseDomain(<br /> DRMLicenseDomain licenseDomain <br /> EventContext (eventContext);<br /> <br /> void resetDRM(EventContext eventContext);<br /> void returnLicense(DomString serverURL, <br /> ID licenza DomString,<br /> ID criterio DomString, <br /> commitImmediately booleano,<br /> EventContext (eventContext);<br /> void setAuthenticationToken(<br /> metadati DRMM, <br /> DomString authenticationDomain <br /> Token Uint8Array, <br /> EventContext (eventContext);<br /> void storeLicenseBytes(Uint8Array licenseBytes, <br /> EventContext (eventContext);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>classe DRMErrorListener : <br /> psdkutils pubblico::PSDKInterfaceWithUserData {<br /> pubblico:<br /> void virtuale onDRMError(uint32_t principale, <br /> uint32_t minore, <br /> const psdkutils:: PSDKString&amp; errorString, <br /> const psdkutils::PSDKString&amp; errorServerUrl) = 0;<br /> <br /> protetto:<br /> virtual ~DRMErrorListener() {}<br /> }</p> </td> 
   <td>Evento/Interfaccia/Descrizione 
    <ul> 
     <li>kEventDRMOperationError<p>/ DRMOperationErrorEvent</p> <p>Quando si verifica un errore durante uno dei metodi asincroni di DRMManger.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>classe DRMOperationCompleteListener : <br /> pubblico DRMErrorListener {<br /> pubblico:<br /> void virtuale onDRMOperationComplete() = 0;<br /> <br /> protetto:<br /> virtual ~DRMOperationCompleteListener() {}<br /> };</p> </td> 
   <td>Evento/Interfaccia/Descrizione 
    <ul> 
     <li>kEventDRMInitializationComplete<p>/ PSDKEvent</p> <p>Al termine dell'inizializzazione della DRM.</p> </li> 
     <li>kEventDRMJoinLicenseDomainComplete<p>/ PSDKEvent</p> <p>Al completamento dell’azione joinLicenseDomain().</p> </li> 
     <li>kEventDRMLeaveLicenseDomainComplete<p>/ PSDKEvent</p> <p>Al completamento dell’azione leaveLicenseDomain().</p> </li> 
     <li>kEventDRMResetCompletePSDKEvent<p>/ PSDKEvent</p> <p>Quando l'azione resetDRM() viene completata correttamente.</p> </li> 
     <li>kEventDRMAuthenticationTokenSet<p>/ PSDKEvent</p> <p>Quando l’azione setAuthenticationTokenSet() viene completata correttamente.</p> </li> 
     <li>kEventDRMLicenseStored<p>/ PSDKEvent</p> <p>Al completamento dell’azione storeLicenseBytes().</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>classe DRMAuthenticateListener : <br /> pubblico DRMErrorListener {<br /> pubblico:<br /> void virtuale onAuthenticationComplete(<br /> psdkutils::PSDKImmutableByteArray* <br /> authenticationToken) = 0;<br /> <br /> protetto:<br /> virtual ~DRMAuthenticateListener() {}<br /> }</p> </td> 
   <td>Evento/Interfaccia/Descrizione 
    <ul> 
     <li>kEventDRMAuthenticationComplete<p>/ DRMAuthenticationCompleteEvent</p> <p>Quando la chiamata al metodo DRMManager::authenticate ha esito positivo.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>class DRMAquireLicenseListener: <br /> pubblico DRMErrorListener {<br /> pubblico:<br /> void virtuale onLicenseAcquired(const DRMLicense*) = 0;<br /> <br /> protetto:<br /> virtual ~DRMAquireLicenseListener() {}<br /> };</p> </td> 
   <td>Evento/Interfaccia/Descrizione 
    <ul> 
     <li>kEventDRMPreviewLicenseAcquired<p>/ DRMLicenseAcquiredEvent</p> <p>Quando DRMManager::acquisitionPreviewLicense viene chiamato correttamente.</p> </li> 
     <li>kEventDRMLicenseAcquired<p>/ DRMLicenseAcquiredEvent</p> <p>Quando DRMManager::acquisitionLicense viene chiamato correttamente.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>class DRMReturnLicenseListener: <br /> pubblico DRMErrorListener {<br /> pubblico:<br /> void virtuale onLicenseReturnComplete(uint32_t numReturned ) = 0;<br /> <br /> protetto:<br /> virtual ~DRMReturnLicenseListener() {}<br /> };</p> </td> 
   <td>Evento/Interfaccia/Descrizione 
    <ul> 
     <li>kEventDRMLicenseReturnComplete<p>/ DRMLicenseReturnCompleteEvent</p> <p>Quando DRMManager::returnLicense viene chiamato correttamente.</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## Modifiche all’elemento API di riproduzione generica per 2.0 {#generic-playback-api-element-changes-for}

Queste tabelle confrontano gli elementi API di riproduzione generici tra JavaScript TVSDK 1.3 e 2.0.

Tabelle in questo argomento:

* MediaResource
* MediaPlayer
* ABRControlParameters
* ParametriControlloBuffer
* FormatoTesto
* MediaPlayerItemLoader

### MediaResource {#mediaresource}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface MediaResource {<br /> attributo URL DomString; <br /> attributo di tipo short senza segno;<br /> attributo Metadati oggetto;<br /> const short TYPE_HLS senza segno;<br /> const short TYPE_HDS senza segno;<br /> const short TYPE_DASH senza segno;<br /> const short TYPE_CUSTOM senza segno;<br /> const short TYPE_UNKNOWN senza segno;<br /> };</p> </td> 
   <td><p>interface MediaResource {<br /> attributo URL DomString;<br /> tipo DomString dell'attributo;<br /> attributo Metadati oggetto;<br /> <br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### MediaPlayer {#mediaplayer}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface MediaPlayer : EventTarget<br /> {<br /> void prepareToPlay( posizione doppia);<br /> void play();<br /> void pause()<br /> void seek( doppia posizione);<br /> void seekToLocal( posizione doppia);<br /> void reset();<br /> void release();<br /> void replaceCurrentItem(MediaPlayerItem item);<br /> void replaceCurrentResource(MediaResource, <br /> MediaPlayerItemConfig config); <br /> void SUSPENCE();<br /> void restore();<br /> void notificationClick();<br /> <br /> attributo di sola lettura TimeRange playbackRange;<br /> attributo di sola lettura TimeRange seekableRange;<br /> attributo di sola lettura double currentTime;<br /> attributo readonly double localTime;<br /> attributo di sola lettura TimeRange bufferedRange;<br /> attributo di sola lettura DRManager drmManager;<br /> attributo di sola lettura MediaPlayerItem currentItem;<br /> <br /> // StatoLettore<br /> <br /> <br /> const short PLAYER_STATUS_INITIALIZED senza segno;<br /> const short PLAYER_STATUS_PREPARING senza segno;<br /> contiene il breve PLAYER_STATUS_READY senza segno;<br /> const short PLAYER_STATUS_PLAYED senza segno;<br /> const short PLAYER_STATUS_PAUSED senza segno;<br /> contiene il breve PLAYER_STATUS_SEEKING senza segno;<br /> contiene il breve PLAYER_STATUS_COMPLETE senza segno;<br /> const short PLAYER_STATUS_ERROR senza segno;<br /> contiene il breve PLAYER_STATUS_RELEASE senza segno;<br /> <br /> attributo readonly: stato short senza segno;<br /> <br /> attribuire un volume corto senza segno;<br /> attributo ABRControlParameters abrControlParameters;<br /> attributo BufferControlParameters bufferControlParameters;<br /> <br /> const unsigned short VISIBLE; //Per visibilità CC<br /> const unsigned short INVISIBLE; //Per visibilità CC<br /> attributo short non firmato ccVisibility;<br /> attributo TextFormat ccStyle;<br /> attributo di sola lettura PlaybackMetrics playbackMetrics;<br /> <br /> attributo double rate;<br /> attributo MediaPlayerView view;<br /> timeline della timeline dell’attributo di sola lettura;<br /> attributo double currentTimeUpdateInterval; <br /> // impostazione non supportata per la versione 2.0<br /> };</p> </td> 
   <td><p>interface MediaPlayer : EventTarget<br /> {<br /> void prepareToPlay( int position);<br /> void play();<br /> void pause()<br /> void seek( posizione int);<br /> void seekToLocalTime( int position);<br /> void reset();<br /> void release();<br /> void replaceCurrentItem(MediaResource source);<br /> <br /> <br /> <br /> <br /> <br /> <br /> attributo di sola lettura TimeRange playbackRange;<br /> attributo di sola lettura TimeRange seekableRange;<br /> attributo di sola lettura double currentTime;<br /> attributo readonly double localTime;<br /> attributo di sola lettura TimeRange bufferedRange;<br /> attributo di sola lettura DRManager drmManager;<br /> attributo di sola lettura MediaPlayerItem currentItem;<br /> <br /> // StatoLettore<br /> contiene il breve PLAYER_STATE_IDLE senza segno;<br /> const short PLAYER_STATE_INITIALIZING senza segno;<br /> const short PLAYER_STATE_INITIALIZED senza segno;<br /> const short PLAYER_STATE_PREPARING senza segno;<br /> contiene il breve PLAYER_STATE_READY senza segno;<br /> const short PLAYER_STATE_PLAYED senza segno;<br /> contiene il breve PLAYER_STATE_PAUSED senza segno;<br /> contiene il breve PLAYER_STATE_SEEKING senza segno;<br /> contiene il breve PLAYER_STATE_COMPLETE senza segno;<br /> const short PLAYER_STATE_ERROR senza segno;<br /> contiene il breve PLAYER_STATE_RELEASE senza segno;<br /> contiene il breve PLAYER_STATUS_SUSPENDED senza segno;<br /> attributo readonly: stato breve senza segno;<br /> <br /> attribuire un volume corto senza segno;<br /> attributo ABRControlParameters abrControlParameters;<br /> attributo BufferControlParameters bufferControlParameters;<br /> <br /> readonly unsigned short VISIBLE; //Per visibilità CC<br /> invisibile corto senza segno in sola lettura; //Per visibilità CC<br /> attributo short non firmato ccVisibility;<br /> attributo TextFormat ccStyle;<br /> attributo di sola lettura PlaybackMetrics playbackMetrics;<br /> attributo MediaPlayerConfig mediaPlayerConfig;<br /> attributo double rate;<br /> attributo MediaPlayerView view;<br /> timeline della timeline dell’attributo di sola lettura;<br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interfaccia MediaPlayerStatus<br /> {<br /> // StatoLettore<br /> contiene il breve PLAYER_STATUS_IDLE senza segno;<br /> const short PLAYER_STATUS_INITIALIZING senza segno;<br /> const short PLAYER_STATUS_INITIALIZED senza segno;<br /> const short PLAYER_STATUS_PREPARING senza segno;<br /> contiene il breve PLAYER_STATUS_READY senza segno;<br /> const short PLAYER_STATUS_PLAYED senza segno;<br /> const short PLAYER_STATUS_PAUSED senza segno;<br /> contiene il breve PLAYER_STATUS_SEEKING senza segno;<br /> contiene il breve PLAYER_STATUS_COMPLETE senza segno;<br /> const short PLAYER_STATUS_ERROR senza segno;<br /> contiene il breve PLAYER_STATUS_RELEASE senza segno;<br /> contiene il breve PLAYER_STATUS_SUSPENDED senza segno;<br /> };</p> </td> 
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
   <th>1.3 Nome dell’evento</th> 
   <th>1.3 Interfaccia</th> 
  </tr> 
  <tr> 
   <td><p>(eliminato per 2.0)</p> </td> 
   <td> </td> 
   <td> </td> 
   <td>preparato</td> 
   <td>Evento</td> 
  </tr> 
  <tr> 
   <td><p>itemUpdated</p> <p>Quando viene aggiornato un elemento del lettore multimediale.</p> </td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>aggiornato</p> <p>Quando il lettore multimediale è stato aggiornato correttamente.</p> </td> 
   <td>Evento</td> 
  </tr> 
  <tr> 
   <td>timedMetadataAvailable</td> 
   <td>TimedMetadataEvent</td> 
   <td> </td> 
   <td>TmedMetadata</td> 
   <td>TimedMetadataEvent</td> 
  </tr> 
  <tr> 
   <td>timelineUpdated</td> 
   <td>Evento</td> 
   <td> </td> 
   <td>TimelineUpdated</td> 
   <td>Evento</td> 
  </tr> 
  <tr> 
   <td>Eliminato nella versione 2.0</td> 
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
   <td>dimensione</td> 
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
   <td>avanzamento</td> 
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
   <td>seekBegin</td> 
   <td>SeekEvent</td> 
   <td> </td> 
   <td>seekStart</td> 
   <td>Evento</td> 
  </tr> 
  <tr> 
   <td>seekEnd</td> 
   <td>SeekEvent</td> 
   <td> </td> 
   <td>seekComplete</td> 
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
   <td>bookingReached</td> 
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
   <td>adClicked<br /> Quando l’utente fa clic su un annuncio.</td> 
   <td>AdClickedEvent</td> 
   <td> </td> 
   <td><p>Novità in 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>profileChanged<br /> Quando cambia il profilo di riproduzione.</td> 
   <td>ProfileEvent</td> 
   <td> </td> 
   <td><p>Novità in 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>seekPositionAdjusted<br /> Quando la posizione di ricerca si regola a causa di regole interne o esterne.</td> 
   <td>SeekEvent</td> 
   <td> </td> 
   <td><p>Novità in 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>audioUpdated<br /> Quando viene aggiornato un elemento del lettore multimediale. Per alcuni flussi che contengono tracce audio rilevabili solo al momento della riproduzione, questo evento viene attivato quando sono disponibili nuove tracce audio.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>Novità in 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>sottotitoli aggiornati <br /> Quando viene aggiornato un elemento del lettore multimediale. Per i flussi live/lineari, il client deve aggiornare periodicamente la risorsa multimediale per rilevare i nuovi contenuti disponibili. In questo caso, alcune caratteristiche dei supporti potrebbero cambiare.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>Novità in 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>masterUpdated <br /> Quando viene aggiornato un elemento del lettore multimediale. Per i flussi live/lineari, il client deve aggiornare periodicamente la risorsa multimediale per rilevare i nuovi contenuti disponibili. In questo caso, alcune caratteristiche dei supporti potrebbero cambiare.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>Novità in 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>playbackRangeUpdated<br /> Quando viene aggiornato un elemento del lettore multimediale. Per i flussi live/lineari, il client deve aggiornare periodicamente la risorsa multimediale per rilevare i nuovi contenuti disponibili. In questo caso, alcune caratteristiche dei supporti potrebbero cambiare.</td> 
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
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface ABRControlParameters<br /> {<br /> const short non firmato ABR_POLICY_CONSERVATIVE = 0 ;<br /> const short non firmato ABR_POLICY_MODERATE = 1 ;<br /> const short non firmato ABR_POLICY_AGGRESIVE = 2 ;<br /> <br /> attributo short abrPolicy senza segno;<br /> attributo unsigned int initialBitRate;<br /> attributo senza segno int minBitRate;<br /> attributo unsigned int maxBitRate;<br /> const short DEFAULT_ABR_INITIAL_BITRATE senza segno;<br /> const short DEFAULT_ABR_MIN_BITRATE senza segno;<br /> const short DEFAULT_ABR_MAX_BITRATE senza segno;<br /> const ABRPolicy DEFAULT_ABR_POLICY;<br /> };</p> </td> 
   <td><p>interface ABRControlParameters<br /> {<br /> const short non firmato ABR_POLICY_CONSERVATIVE = 0 ;<br /> const short non firmato ABR_POLICY_MODERATE = 1 ;<br /> const short non firmato ABR_POLICY_AGGRESIVE = 2 ;<br /> <br /> attributo short abrPolicy senza segno;<br /> attributo unsigned int initialBitRate;<br /> attributo senza segno int minBitRate;<br /> attributo unsigned int maxBitRate;<br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### ParametriControlloBuffer {#buffercontrolparameters}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interfaccia BufferControlParameters<br /> {<br /> attributo initialBufferTime doppio;<br /> attributo double playBufferTime;<br /> const double DEFAULT_INITIAL_BUFFER_TIME;<br /> const double DEFAULT_PLAY_BUFFER_TIME;<br /> };</p> </td> 
   <td><p>interfaccia BufferControlParameters<br /> {<br /> attributo initialBufferTime doppio;<br /> attributo double playBufferTime;<br /> <br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### FormatoTesto {#textformat}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td>Nessuna modifica per 2.0</td> 
   <td><p>Interfaccia TextFormat<br /> {<br /> // Colore<br /> const short COLOR_DEFAULT senza segno = 0 ;<br /> const short COLOR_BLACK senza segno = 1 ;<br /> const short COLOR_GREY senza segno = 2 ;<br /> const short COLOR_WHITE senza segno = 3 ;<br /> const short COLOR_BRIGHT_WHITE senza segno = 4 ;<br /> const short non firmato COLOR_DARK_RED = 5 ;<br /> const short COLOR_RED senza segno = 6 ;<br /> const short COLOR_BRIGHT_RED senza segno = 7 ;<br /> const short non firmato COLOR_DARK_GREEN = 8 ;<br /> const short COLOR_GREEN senza segno = 9 ;<br /> const short non firmato COLOR_BRIGHT_GREEN = 10 ;<br /> const short non firmato COLOR_DARK_BLUE = 11 ;<br /> const short COLOR_BLUE senza segno = 12 ;<br /> const short COLOR_BRIGHT_BLUE senza segno = 13 ;<br /> const short non firmato COLOR_DARK_YELLOW = 14 ;<br /> const short COLOR_YELLOW senza segno = 15 ;<br /> const short COLOR_BRIGHT_YELLOW senza segno = 16 ;<br /> const short non firmato COLOR_DARK_MAGENTA = 17 ;<br /> const short COLOR_MAGENTA senza segno = 18 ;<br /> const short non firmato COLOR_BRIGHT_MAGENTA = 19 ;<br /> const short COLOR_DARK_CYAN senza segno = 20 ;<br /> const short COLOR_CYAN senza segno = 21 ;<br /> const short COLOR_BRIGHT_CYAN senza segno = 22 ;<br /> <br /> attributo di sola lettura fontColor corto senza segno;<br /> attributo readonly short backgroundColor senza segno;<br /> attributo readonly short fillColor senza segno;<br /> attributo readonly short edgeColor senza segno;<br /> <br /> // Dimensioni<br /> const short SIZE_DEFAULT senza segno = 0 ;<br /> const short SIZE_SMALL senza segno = 1 ;<br /> const short SIZE_MEDIUM senza segno = 2 ;<br /> const short SIZE_LARGE senza segno = 3 ;<br /> <br /> attributo readonly senza segno di dimensione corta;<br /> <br /> // CarattereBordo<br /> const short FONT_EDGE_DEFAULT senza segno = 0 ;<br /> const short FONT_EDGE_NONE senza segno = 1 ;<br /> const short FONT_EDGE_RAISED senza segno = 2 ;<br /> const short FONT_EDGE_DEPRESSED senza segno = 3 ;<br /> const short FONT_EDGE_UNIFORM senza segno = 4 ;<br /> const short FONT_EDGE_DROP_SHADOW_LEFT senza segno = 5 ;<br /> const short FONT_EDGE_DROP_SHADOW_RIGHT senza segno = 6 ;<br /> attributo readonly short fontEdge senza segno;<br /> <br /> // Carattere<br /> const short FONT_DEFAULT senza segno = 0 ;<br /> const short FONT_MONOSPACED_WITH_SERIFS senza segno = 1 ;<br /> const short FONT_proportIONAL_WITH_SERIFS senza segno = 2 ;<br /> const short FONT_MONSPACED_WITHOUT_SERIFS senza segno = 3 ;<br /> const short FONT_CASUAL senza segno = 4 ;<br /> const short FONT_CURSIVE senza segno = 5 ;<br /> const short FONT_SMALL_CAPITALS senza segno = 6 ;<br /> attributo readonly: carattere breve senza segno;<br /> attributo readonly fontOpacity breve senza segno;<br /> attributo readonly short backgroundOpacity senza segno;<br /> attributo readonly short fillOpacity senza segno;<br /> attributo di sola lettura short DEFAULT_OPACITY senza segno;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### MediaPlayerItemLoader {#mediaplayeritemloader}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interfaccia MediaPlayerItemLoader:<br /> {<br /> void load(MediaResource resource, long resourceId,<br /> Listener ItemLoaderListener, <br /> MediaPlayerItemConfig config) ;<br /> void cancel();<br /> attributo di sola lettura MediaPlayerItem currentItem;<br /> };</p> </td> 
   <td>Nuovo per 2.0</td> 
  </tr> 
  <tr> 
   <td><p>interfaccia ItemLoaderListener<br /> {<br /> //onLoadCompleteCallbackFunc(MediaPlayerItem)<br /> var onLoadCompleteCallbackFunc;<br /> //onErrorCallbackFunc(PSDKErrorCode)<br /> var onErrorCallbackFunc;<br /> }</p> </td> 
   <td>Nuovo per 2.0</td> 
  </tr> 
 </tbody> 
</table>

## Modifiche all’elemento API delle caratteristiche multimediali per 2.0 {#media-characteristics-api-element-changes-for}

Queste tabelle confrontano gli elementi API delle caratteristiche multimediali per C++ TVSDK tra le versioni 1.3 e 2.0.

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
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface MediaPlayerItem {<br /> attributo di sola lettura MediaResource;<br /> attributo di sola lettura long resourceId;<br /> attributo di sola lettura boolean live;<br /> <br /> attributo di sola lettura booleano hasAlternateAudio;<br /> attributo di sola lettura AudioTrackList audioTracks;<br /> attributo di sola lettura AudioTrack selectedAudioTrack;<br /> void selectAudioTrack(traccia AudioTrack); <br /> <br /> attributo boolean di sola lettura hasClosedCaptions;<br /> attributo di sola lettura ClosedCaptionsTrackList closedCaptionsTracks;<br /> attributo di sola lettura ClosedCaptionsTrack selectedClosedCaptionsTrack;<br /> void selectClosedCaptionsTrack(<br /> ClosedCaptionsTrack); <br /> <br /> attributo booleano di sola lettura hasTimedMetadata;<br /> attributo di sola lettura TimedMetadataList timedMetadata;<br /> attributo di sola lettura boolean dynamic;<br /> <br /> attributo di sola lettura boolean isProtected;<br /> attributo di sola lettura DRMMetadataInfoList drmMetadataInfos;<br /> attributo di sola lettura ProfileList profiles;<br /> attributo di sola lettura Profile selectedProfile;<br /> <br /> attributo di sola lettura trickPlaySupported booleano;<br /> attributo di sola lettura FloatArray availablePlaybackRates;<br /> valore float selectedPlaybackRate dell'attributo di sola lettura;<br /> <br /> <br /> attributo di sola lettura MediaPlayer mediaPlayer;<br /> attributo readonly: configurazione MediaPlayerItemConfig;<br /> };</p> </td> 
   <td><p>interface MediaPlayerItem {<br /> attributo di sola lettura MediaResource;<br /> attributo di sola lettura long resourceId;<br /> attributo di sola lettura boolean live;<br /> <br /> attributo di sola lettura booleano hasAlternateAudio;<br /> attributo di sola lettura AudioTrackList audioTracks;<br /> attributo AudioTrack selectedAudioTrack;<br /> <br /> <br /> attributo boolean di sola lettura hasClosedCaptions;<br /> attributo di sola lettura ClosedCaptionsTrackList ccTracks;<br /> attributo ClosedCaptionsTrack selectedCCTrack;<br /> <br /> <br /> <br /> attributo booleano di sola lettura hasTimedMetadata;<br /> attributo di sola lettura TimedMetadataList timedMetadata;<br /> attributo di sola lettura boolean dynamic;<br /> <br /> attributo di sola lettura boolean isProtected;<br /> attributo di sola lettura DRMMetadataInfoList drmMetadataInfos;<br /> attributo di sola lettura ProfileList profiles;<br /> <br /> <br /> attributo di sola lettura trickPlaySupported booleano;<br /> attributo di sola lettura Int32Array availablePlaybackRates;<br /> <br /> attributo di sola lettura StringList adTags;<br /> <br /> attributo di sola lettura MediaPlayer mediaPlayer;<br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### Track/AudioTrack/ClosedCaptionsTrack {#track-audiotrack-closedcaptionstrack}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>Interfaccia Track<br /> {<br /> attributo di sola lettura DomString name;<br /> attributo di sola lettura linguaggio DomString;<br /> valore predefinito boolean dell'attributo readonly;<br /> attributo di sola lettura boolean autoSelect;<br /> }; </p> </td> 
   <td>Nuovo per 2.0</td> 
  </tr> 
  <tr> 
   <td><p>interface AudioTrack : Track<br /> {<br /> attributo di sola lettura DomString name; //FromTrack<br /> attributo di sola lettura DomString language;//FromTrack<br /> attributo di sola lettura predefinito booleano; // From Track<br /> attributo di sola lettura boolean autoSelect;//FromTrack<br /> <br /> attributo readonly senza segno int pid;<br /> };</p> </td> 
   <td><p>Interfaccia AudioTrack<br /> {<br /> attributo di sola lettura DomString name;<br /> attributo di sola lettura linguaggio DomString; <br /> valore predefinito boolean dell'attributo readonly;<br /> attributo di sola lettura boolean autoSelect;<br /> attributo di sola lettura booleano forzato;<br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td>Nessuna modifica per 2.0</td> 
   <td><p>interfaccia AudioTrackList<br /> {<br /> attributo di sola lettura long length senza segno;<br /> getter AudioTrack (indice lungo senza segno);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>Interfaccia ClosedCaptionsTrack : Track<br /> {<br /> attributo di sola lettura DomString name; //FromTrack<br /> attributo di sola lettura DomString language;//FromTrack<br /> attributo di sola lettura predefinito boolean; // FromTrack<br /> attributo di sola lettura boolean autoSelect;//FromTrack<br /> <br /> <br /> const short SERVICE_608_CAPTIONS non firmato = 0;<br /> const short SERVICE_708_CAPTIONS senza segno = 1;<br /> const short SERVICE_WEB_VTT_CAPTIONS senza segno = 2;<br /> attributo readonly short serviceType senza segno;<br /> attributo di sola lettura booleano forzato;<br /> };</p> </td> 
   <td><p>Interfaccia ClosedCaptionsTrack<br /> {<br /> attributo di sola lettura DomString name;<br /> attributo di sola lettura linguaggio DomString;<br /> valore predefinito boolean dell'attributo readonly;<br /> <br /> <br /> attributo di sola lettura booleano attivo;<br /> <br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td>Nessuna modifica per 2.0</td> 
   <td><p>interfaccia ClosedCaptionsTrackList<br /> {<br /> attributo di sola lettura long length senza segno;<br /> getter ClosedCaptionsTrack(indice lungo senza segno);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### Profilo {#profile}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td>Profilo: nessuna modifica per 2.0</td> 
   <td><p>Profilo interfaccia<br /> {<br /> attributo readonly senza segno int width;<br /> attributo readonly senza segno int height;<br /> attributo readonly senza segno int bitRate;<br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td>ProfileList: nessuna modifica per 2.0</td> 
   <td><p>ProfileList dell'interfaccia<br /> {<br /> attributo di sola lettura long length senza segno;<br /> getter Profile(unsigned long index);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMMetadataInfo {#drmmetadatainfo}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><strong>DRMMetadataInfo</strong>: nessuna modifica per 2.0</td> 
   <td><p>interfaccia DRMMetadataInfo<br /> { <br /> metadati DRMMetadata di attributo di sola lettura;<br /> attributo di sola lettura long prefetchTimestamp;<br /> attributo di sola lettura TimeRange timeRange;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>DRMMetadataInfoList</strong>: nessuna modifica per 2.0</td> 
   <td><p>interfaccia DRMMetadataInfoList<br /> {<br /> attributo di sola lettura long length senza segno;<br /> getter DRMMetadataInfo(unsigned long index);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

## Mappatura degli errori C++ alle eccezioni in diverse lingue {#mapping-c-errors-to-exceptions-in-different-languages}

È possibile mappare i codici di errore C++ alle eccezioni in lingue diverse.

Il PSDK C++ dispone di un criterio &quot;no throw&quot; per le sue API. La maggior parte dei metodi API restituisce un valore PSDKErrorCode per indicare se il metodo è stato eseguito correttamente. Gli errori asincroni vengono notificati tramite gli eventi di errore.

Il PSDK ActionScript e JAVA hanno un criterio diverso. La maggior parte degli errori genererà ArgumentError o IllegalStateException per indicare che non è stato possibile eseguire la parte sincrona del metodo. Queste eccezioni non vengono rilevate e il codice dell’applicazione è responsabile della loro gestione. In genere contengono informazioni utili sul motivo per cui la chiamata al metodo non è riuscita. Ad esempio, se il comando prepareToPlay viene chiamato in uno stato non valido, viene generata la seguente eccezione:

```shell
throw new IllegalStateException("Invalid player state. prepareToPlay method 
must be called only once after replaceCurrentItem or replaceCurrentResource method.");
```

L’ActionScript/JAVA genera anche eccezioni dai costruttori per indicare che un oggetto interno è stato creato in modo errato. Queste eccezioni vengono gestite internamente e non vengono propagate all&#39;applicazione. Le eccezioni verranno incluse in una notifica di avviso inviata all&#39;applicazione

Ad esempio, se non è stato trovato alcun file multimediale valido per la risposta dell’annuncio ricevuto, non è possibile creare alcun oggetto o annuncio di risorsa dell’annuncio valido. Di conseguenza, non viene inserito alcun annuncio nella timeline e viene inviata una notifica NotificationEvent.OperationFailed.

I codici di errore o di avviso ricevuti in modo asincrono dal motore video di Adobe (AVE) vengono inviati all&#39;applicazione come eventi normali. L’evento di notifica contiene tutti i codici di errore ricevuti ed eventuali metadati aggiuntivi, ad esempio l’URL, l’identificatore della risorsa, l’handle e così via. Se l&#39;errore è grave e la riproduzione del supporto corrente non può continuare, MediaPlayer passa allo stato ERROR e viene inviato il callback onStatusChanged o l&#39;evento MediaPlayerStatusChanged.STATUS_CHANGED. Se la riproduzione può continuare, viene inviato un evento di notifica normale.

<table> 
 <tbody> 
  <tr> 
   <th>Errore C++ (codice PSDKError)</th> 
   <th> </th> 
   <th>Java</th> 
   <th>ActionScript</th> 
   <th>JavaScript</th> 
  </tr> 
  <tr> 
   <td>ArgomentoECInvalid</td> 
   <td> </td> 
   <td>IllegalArgumentException</td> 
   <td>ErroreArgomento</td> 
   <td>Eccezione con codice = 1, descrizione = "INVALID_ARGUMENT" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNullPointer</td> 
   <td> </td> 
   <td>IllegalArgumentException</td> 
   <td>ErroreArgomento</td> 
   <td>Eccezione con codice = 2, descrizione = "GENERIC_ERROR" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECIllegalState</td> 
   <td> </td> 
   <td>IllegalStateException</td> 
   <td>IllegalStateException</td> 
   <td>Eccezione con codice = 3, descrizione = "ILLEGAL_STATE" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECInterfaceNotFound</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 4, descrizione = "GENERIC_ERROR" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECCreationFailed</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 5, descrizione = "CREATION_FAILED" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECUnsupportedOperation</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 5, descrizione = "CREATION_FAILED" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECDataNotAvailable</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 7, descrizione = "DATA_NOT_AVAILABLE" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECSekError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 8, descrizione = "SEEK_ERROR" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECUnsupportedFeature</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 9, descrizione = "UNSUPPORTED_FEATURE" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECRangeError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 10, descrizione = "RANGE_ERROR" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECCodecNotSupported</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 11, descrizione = "CODEC_NOT_SUPPORTED" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECMediaError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 12, descrizione = "MEDIA_ERROR" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNetworkError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 13, descrizione = "NETWORK_ERROR" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>Errore genericoECG</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Error o MediaPlayerNotification.Warning</td> 
   <td>MediaError o NotificationEvent</td> 
   <td>Eccezione con codice = 14, descrizione = "GENERIC_ERROR" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECInvalidSeekTime</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 15, descrizione = "INVALID_SEEK_TIME" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAudioTrackError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 16, descrizione = "AUDIO_TRACK_ERROR" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAccessFromDifferent<p>ThreadError</p> </td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 17, descrizione = "GENERIC_ERROR" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>ElementoNonTrovato</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 18, descrizione = "GENERIC_ERROR" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNotImplementato</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 19, descrizione = "GENERIC_ERROR" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECPlaybackOperationFailed</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 200, descrizione = "PLAYBACK_OPERATION_FAILED" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNativeWarning</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Warning</td> 
   <td>NotificationEvent</td> 
   <td>Eccezione con codice = 201, descrizione = "NATIVE_WARNING" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAdResolverFailed</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Warning</td> 
   <td>-</td> 
   <td>Eccezione con codice = 202, descrizione = "AD_RESOLVER_FAILED" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
 </tbody> 
</table>

## Modifiche all’elemento Utility e Helper API per 2.0 {#utility-and-helper-api-element-changes-for}

Queste tabelle confrontano gli elementi API Utility e Helper per TVSDK JavaScript tra le versioni 1.3 e 2.0.

Tabelle in questo argomento:

* Versione
* Intervallo di tempo
* QOSProvider
* InformazioniDispositivo
* LoadInfo
* Visualizza
* PlaybackInformation

### Versione {#version}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>Versione interfaccia<br /> {<br /> attributo readonly versione DomString;<br /> attributo di sola lettura DomString description;<br /> attributo di sola lettura long major;<br /> attributo di sola lettura long minor;<br /> revisione estesa attributo di sola lettura;<br /> attributo di sola lettura long apiVersion;<br /> };</p> </td> 
   <td><p>Versione interfaccia<br /> {<br /> attributo readonly versione DomString;<br /> attributo di sola lettura DomString description;<br /> attributo di sola lettura DomString major;<br /> attributo di sola lettura DomString secondario;<br /> revisione DomString dell’attributo di sola lettura;<br /> attributo di sola lettura DomString apiVersion;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### Intervallo di tempo {#timerange}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td>Nessuna modifica per 2.0</td> 
   <td><p>Interfaccia TimeRange<br /> {<br /> attributo di sola lettura long begin senza segno;<br /> attributo di sola lettura long end senza segno;<br /> attributo di sola lettura di lunga durata senza segno;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### QOSProvider {#qosprovider}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td>Nessuna modifica per 2.0</td> 
   <td><p>Interfaccia QOSProvider<br /> {<br /> void attachMediaPlayer(MediaPlayer player);<br /> void detachMediaPlayer();<br /> <br /> attributo di sola lettura DeviceInformation deviceInformation;<br /> attributo di sola lettura PlaybackInformation playbackInformation playbackInformation;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### InformazioniDispositivo {#deviceinformation}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interfaccia DeviceInformation<br /> {<br /> attributo di sola lettura DomString os;<br /> <br /> <br /> <br /> attributo di sola lettura ID DomString;<br /> attributo readonly int densityDPI;<br /> attributo readonly int heightPixels;<br /> attributo readonly int widthPixels;<br /> attributo booleano di sola lettura seekToKeyFrame;<br /> };</p> </td> 
   <td><p>interfaccia DeviceInformation<br /> {<br /> attributo di sola lettura DomString os;<br /> attributo readonly int sdk;<br /> modello DomString di attributo readonly;<br /> attributo di sola lettura DomString produttore;<br /> attributo di sola lettura ID DomString;<br /> attributo readonly int densityDPI;<br /> attributo readonly int heightPixels;<br /> attributo readonly int widthPixels;<br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### LoadInfo {#loadinfo}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td>Nessuna modifica per 2.0</td> 
   <td><p>interfaccia LoadInfo<br /> {<br /> URL DomString di attributo readonly;<br /> dimensione int attributo di sola lettura;<br /> attributo di sola lettura double downloadDuration;<br /> attributo readonly int periodIndex;<br /> attributo di sola lettura double mediaDuration;<br /> attributo di sola lettura short TRACK_TYPE_FRAGMENT;<br /> attributo di sola lettura short TRACK_TYPE_TRACK;<br /> attributo di sola lettura short TRACK_TYPE_MANIFEST;<br /> tipo short dell'attributo readonly;<br /> attributo di sola lettura DomString trackName;<br /> attributo di sola lettura DomString trackType;<br /> attributo readonly int trackIndex;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### Visualizza {#view}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td>Nessuna modifica per 2.0</td> 
   <td><p>Vista interfaccia<br /> {<br /> attributo readonly: x corta senza segno;<br /> attributo readonly senza segno y breve;<br /> attributo readonly senza segno larghezza breve;<br /> attributo readonly: altezza corta senza segno;<br /> <br /> void setSize(larghezza breve senza segno, altezza breve senza segno);<br /> void setPos(unsigned short x, unsigned short y);<br /> }</p> </td> 
  </tr> 
 </tbody> 
</table>

### PlaybackInformation {#playbackinformation}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interfaccia PlaybackInformation<br /> {<br /> attributo di sola lettura double timeToFirstByte;<br /> attributo di sola lettura double timeToLoad;<br /> attributo di sola lettura double timeToStart;<br /> attributo di sola lettura double timeToFail;<br /> attributo readonly int totalSecondsPlayed;<br /> attributo readonly int totalSecondsSpent;<br /> attributo di sola lettura double frameRate;<br /> attributo readonly int droppedFrameCount;<br /> attributo readonly int percepivedBandwidth;<br /> attributo readonly int bitrate;<br /> attributo di sola lettura double bufferTime;<br /> attributo readonly in bufferLength;<br /> attributo readonly in emptyBufferCount;<br /> attributo di sola lettura double bufferingTime;<br /> };</p> </td> 
   <td><p>interfaccia PlaybackInformation<br /> {<br /> attributo di sola lettura double timeToFirstByte;<br /> attributo di sola lettura double timeToLoad;<br /> attributo di sola lettura double timeToStart;<br /> attributo di sola lettura double timeToFail;<br /> attributo readonly int totalSecondsPlayed;<br /> attributo readonly int totalSecondsSpent;<br /> attributo di sola lettura double frameRate;<br /> attributo readonly int droppedFrameCount;<br /> <br /> attributo readonly int bitrate;<br /> attributo di sola lettura double bufferTime;<br /> attributo readonly in bufferLength;<br /> attributo readonly in emptyBufferCount;<br /> attributo di sola lettura double bufferingTime;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

## Risorse utili {#helpful-resources}

* Consulta la documentazione completa dell’Aiuto all’indirizzo [Informazioni e supporto per Adobe Primetime](https://helpx.adobe.com/support/primetime.html) pagina.
