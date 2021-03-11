---
title: Conversione TVSDK - da 1.3 a 2.0 per JavaScript
description: Molte firme dei metodi e i nomi degli elementi API sono cambiati per la versione 2.0. Rivedi queste tabelle per visualizzare tutti i dettagli delle modifiche API.
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: migration
translation-type: tm+mt
source-git-commit: b33240bf1b42b80389cd95a7ae4d3f85185a2d32
workflow-type: tm+mt
source-wordcount: '5034'
ht-degree: 0%

---


# Conversione TVSDK - da 1.3 a 2.0 per JavaScript {#tvsdk-conversion-to-for-javascript}

Molte firme dei metodi e i nomi degli elementi API sono cambiati per la versione 2.0. Rivedi queste tabelle per visualizzare tutti i dettagli delle modifiche API.

## Implementazione delle funzioni di callback in JavaScript {#implement-callback-functions-in-javascript}

I commenti nella documentazione del metodo suggeriscono la firma per i callback che è necessario implementare.

Per JavaScript, la sintassi API è basata su Web ID. Per un&#39;interfaccia TVSDK, i nomi dei metodi sono chiamati *methodName*(). Per implementare i metodi dall&#39;applicazione, all&#39;interfaccia viene aggiunto un attributo di lettura/scrittura denominato *methodName* CallbackFunc e l&#39;applicazione deve impostarlo per puntare a una funzione che implementa il metodo . Ad esempio:

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

Queste tabelle confrontano gli elementi dell’API del flusso di lavoro pubblicitario per l’SDK JavaScript TVSDK tra le versioni 1.3 e 2.0.

Tabelle in questo argomento:

* TimedMetadata
* AdSignalingMode
* AdvertisingMetadata
* MetadatiIntervalloPersonalizzato
* ReplaceTimeRange
* Posizionamento
* Opportunità
* Prenotazione
* Timeline/TimelineItem/TimelineMarker
* AdBreak
* Annuncio / AdAsset / AdClick / AdList / AdAssetList / AdBannerAsset
* AdBreakTimelineItem / AdTimelineItem
* AdBreakPolicy / AdBreakWatchedPolicy / AdPolicy / AdPolicyMode / AdPolicyInfo / AdPolicySelector
* TimelineOperation
* AdBreakPlacement
* AuditudeSettings

### Metadati temporizzati {#timedmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p> <strong>Metadati</strong> temporizzati: Interfaccia TimedMetadata {<br /> const unsigned short METADATA_TYPE_TAG = 0 ;  <br /> const short METADATA_TYPE_ID3 = 1 ;  <br /> attributo di sola lettura tipo breve non firmato;  <br /> attributo di sola lettura a lungo termine;<br /> attributo di sola lettura ID DomString;nome attributo di <br /> sola lettura DomString;contenuto <br /> attributo di sola lettura DomString;  <br /> metadati dell'oggetto attributo di sola lettura;<br /> }; </p> </td> 
   <td><p>Interfaccia TimedMetadata {<br /> const unsigned short METADATA_TYPE_TAG = 0 ;<br /> const unsigned short METADATA_TYPE_ID3 = 1 ;<br /> readonly attribute unsigned short metadataType;<br /> readonly attribute long time;<br /> readonly attribute long id;<br /> readonly attribute DomString name;<br /> <br /> metadati dell'attributo di sola lettura Object;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>TimedMetadataList</strong>: (Nessuna modifica per la versione 2.0)</td> 
   <td><p>interfaccia TimedMetadataList {<br /> attributo readonly a lunga lunghezza senza segno;<br /> getter TimedMetadata(unsigned long index);<br /> };</p> </td> 
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
   <td><p>Interfaccia AdSignalingMode { <br /> const unsigned short MODE_DEFAULT, <br /> const unsigned short MODE_MANIFEST_CUES , <br /> const unsigned short MODE_SERVER_MAP , <br /> const unsigned short MODE_CUSTOM_RANGES <br /> };</p> </td> 
   <td>Questo sostituisce la chiave MetadataKeys::MANIFEST_CUES .</td> 
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
   <td><p>Interfaccia AdvertisingMetadata { <br /> attributo Modalità AdSignaling; <br /> attributo AdBreakWatchedPolicy adBreakAsWatched; <br /> attributo boolean livePreroll; <br /> attributo boolean delayAdLoading ; <br /> };</p> </td> 
   <td>Questa funzionalità è stata fornita da<p>Tasti metadati::ADVERTISING_METADATA</p> key.</td> 
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
   <td><p>Interfaccia CustomRangeMetadata { <br /> const unsigned short TYPE_MARK_RANGE; <br /> const short TYPE_DELETE_RANGE non firmato; <br /> const short TYPE_REPLACE_RANGE non firmato; <br /> attributo tipo breve non firmato; <br /> attributo booleano adjustSeekPosition; <br /> attributo TimeRangeList timeRangeList; <br /> };</p> </td> 
   <td>(Novità per la versione 2.0)</td> 
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
   <td><p>interfaccia ReplaceTimeRange { <br /> attributo long started senza segno; <br /> attributo di sola lettura a lungo termine senza firma; <br /> attributo a lunga durata senza segno; <br /> attributo unsigned long replaceDuration; <br /> };</p> </td> 
   <td>(Novità per la versione 2.0)</td> 
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
   <td><p>Posizione interfaccia { <br /> const short TYPE_MID_ROLL non firmato; <br /> const unsigned short TYPE_PRE_ROLL; <br /> const unsigned short TYPE_POST_ROLL; <br /> const unsigned short TYPE_SERVER_MAP; <br /> const unsigned short TYPE_CUSTOM_RANGE;<br /> attributi di sola lettura tipo breve non firmato; <br /> attributi di sola lettura a lungo termine; <br /> attributi di sola lettura di lunga durata; <br /> const unsigned short MODE_DEFAULT; <br /> const unsigned short MODE_INSERT; <br /> const unsigned short MODE_REPLACE; <br /> const unsigned short MODE_DELETE; <br /> const unsigned short MODE_MARK; <br /> const unsigned short MODE_FREE_REPLACE; <br /> attributi di sola lettura modalità breve non firmata; <br /> attributo readonly intervallo TimeRange; <br /> };</p> </td> 
   <td>(Novità per la versione 2.0)</td> 
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
   <td><p>interface Opportunity { <br /> readonly attribute DomString id; <br /> posizionamento dell'attributo di sola lettura; <br /> impostazioni dell'attributo di sola lettura Object; <br /> readonly attribute customParameters; <br /> }; </p> </td> 
   <td>(Novità per la versione 2.0)</td> 
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
   <td><p>Interfaccia Reservation { <br /> attributo readonly intervallo TimeRange; <br /> sospensione attributi di sola lettura; <br /> }; </p> </td> 
   <td> (Novità per la versione 2.0)</td> 
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
   <td><p><strong>Timeline</strong>: interfaccia Timeline  <br /> { attributo readonly TimelineMarkerList timelineMarkers;  <br /> attributo readonly TimelineItemList timelineItems;  <br /> double convertToLocalTime( double time);  <br /> double convertToVirtualTime( double time);  <br /> };</p> </td> 
   <td><p>interfaccia Timeline {<br /> attributo readonly TimelineMarkerList timelineMarkers;<br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p> <strong>Elemento</strong>Timeline: interfaccia TimelineItem:<br /> TimelineMarker {<br /> readonly attribute long id;  <br /> attributo di sola lettura TimeRange virtualRange;  <br /> attributo di sola lettura TimeRange localRange;  <br /> attributo booleano di sola lettura controllato;  <br /> attributo booleano temporaneo di sola lettura;  <br /> }; </p> </td> 
   <td>(Novità per la versione 2.0)</td> 
  </tr> 
  <tr> 
   <td><strong>TimelineMarker</strong>: (Nessuna modifica per la versione 2.0)</td> 
   <td><p>interfaccia TimelineMarker {<br /> attributo di sola lettura doppio tempo;<br /> attributo di sola lettura doppia durata;<br /> };</p> </td> 
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
   <td><p>interfaccia AdBreak {<br /> <br /> <br /> <br /> attributi di sola lettura di doppia durata;<br /> attributi di sola lettura AdList;<br /> <br /> <br /> attributi di sola lettura AdInsertionType InsertType;<br /> }; </p> </td> 
   <td><p>interfaccia AdBreak {<br /> attributo di sola lettura doppio tempo;<br /> attributo di sola lettura sostituzione doppia durata;<br /> <br /> attributi di sola lettura doppia durata;<br /> attributo di sola lettura AdList adList;<br /> <br /> attributi di sola lettura DomString dati;<br /> <br /> }; </p> </td> 
  </tr> 
 </tbody> 
</table>

### Annuncio / AdAsset / AdClick / AdList / AdAssetList / AdBannerAsset {#ad-adasset-adclick-adlist-adassetlist-adbannerasset}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p> <strong>Annuncio</strong>: interfaccia Ad {<br /> readonly attribute AdAsset primaryAsset;<br /> readonly attribute AdAssetList companionAssets;<br /> <br /> readonly attribute double duration;<br /> readonly attribute DomString id;<br /> const unsigned short ADTYPE_LINEAR = 0 ;<br /> const unsigned short ADTYPE_NONLINEAR = 1 ;attributo <br /> <br /> readonly unsigned short adType;<br /> readattribute AdInsertionType adInsertionType;  <br /> <br /> attributo di sola lettura cliccabile booleano;  <br /> attributo di sola lettura boolean isCustomAdMarker;<br /> }; </p> </td> 
   <td><p>Ad interfaccia Ad {<br /> attributo di sola lettura AdAsset primaryAsset;<br /> attributo di sola lettura AdAssetList companionAssets;<br /> <br /> attributi di sola lettura di doppia durata;<br /> attributo di sola lettura DomString id;<br /> attributo di sola lettura di ADTYPE_LINEAR = 0 ;<br /> const short ADTYPE_ONONONONONONON LINEAR = 1 ;<br /> <br /> attributo di sola lettura tipo breve non firmato;<br /> attributo di sola lettura AdInsertionType insertType; <br /> rilevatore di oggetti di sola lettura;<br /> <br /> <br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAsset</strong>: (Nessuna modifica per la versione 2.0)</td> 
   <td><p>interfaccia AdAsset {<br /> attributi di sola lettura DomString id;<br /> attributi di sola lettura a doppia durata;<br /> attributi di sola lettura MediaResource resource;<br /> attributi di sola lettura AdClick adClick;<br /> metadati di attributi di sola lettura Object;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdClick</strong>: (Nessuna modifica per la versione 2.0)</td> 
   <td><p>interfaccia AdClick {<br /> attributo di sola lettura DomString id;<br /> attributo di sola lettura DomString title;<br /> attributo di sola lettura DomString url;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdList</strong>: (Nessuna modifica per la versione 2.0)</td> 
   <td><p>interface AdList {<br /> attributo readonly a lunga lunghezza senza segno;<br /> getter Ad(indice lungo senza segno);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAssetList</strong>: (Nessuna modifica per la versione 2.0)</td> 
   <td><p>interface AdAssetList {<br /> attributo readonly a lunga lunghezza senza segno;<br /> getter AdAsset(unsigned long index);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBannerAsset</strong>: interfaccia AdBannerAsset : AdAsset<br /> {<br /> readonly attributo int width;<br /> readonly attributo int height;<br /> readonly attributo DomString staticUrl;<br /> readonly attributo DomString height;<br /> readonly attribute DomString width;<br /> };</p> </td> 
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
   <td><p> <strong>AdBreakTimelineItem</strong>: interfaccia AdBreakTimelineItem : TimelineItem { attributo  <br /> readonly AdBreak;  <br /> elementi AdTimelineItemList dell'attributo di sola lettura;  <br /> }; </p> </td> 
   <td> (Novità per la versione 2.0)</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdTimelineItem</strong>: interfaccia AdTimelineItem : TimelineItem { attributo  <br /> readonly AdBreak;  <br /> annuncio dell'attributo di sola lettura;  <br /> }; </p> </td> 
   <td> (Novità per la versione 2.0)</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBreakTimelineItemList</strong>: interfaccia AdBreakTimelineItemList {  <br /> attributi di sola lettura a lunga lunghezza senza firma;  <br /> getter AdBreakTimelineItem (indice ng non firmato);  <br /> };</p> </td> 
   <td> (Novità per la versione 2.0)</td> 
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
   <td><p>interface AdBreakPolicy {<br /> attributo di sola lettura short AD_BREAK_POLICY_SKIP;<br /> attributo di sola lettura breve AD_BREAK_POLICY_PLAY;<br /> attributo di sola lettura breve AD_BREAK_POLICY_REMOVE;<br /> attributo di sola lettura breve AD_BREAK_POLICY_REMOVE_AFTER_PLAY;<br /> };</p> </td> 
   <td><p> interface AdPolicyConstants {<br /> attributo di sola lettura short AD_BREAK_POLICY_SKIP;<br /> attributo di sola lettura breve AD_BREAK_POLICY_PLAY;<br /> attributo di sola lettura breve AD_BREAK_POLICY_REMOVE;<br /> attributo di sola lettura breve AD_BREAK_POLICY_REMOVE VE_AFTER_PLAY;}<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p> interfaccia AdBreakWatchedPolicy {<br /> attributi di sola lettura brevi AD_BREAK_AS_WATCHED_ON_BEGIN;<br /> attributi di sola lettura brevi AD_BREAK_AS_WATCHED_ON_END;<br /> attributi di sola lettura brevi AD_BREAK_AS_WATCHED_NEVER;<br /> }; </p> </td> 
   <td><p> ...<br /> attributi di sola lettura brevi AD_BREAK_AS_WATCHED_ON_BEGIN;<br /> attributi di sola lettura brevi AD_BREAK_AS_WATCHED_ON_END;<br /> attributi di sola lettura brevi AD_BREAK_AS_WATCHED_NEVER;<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>interfaccia AdPolicy {<br /> attributi di sola lettura brevi AD_POLICY_PLAY;<br /> attributi di sola lettura brevi AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> attributi di sola lettura brevi AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN; attributo readonly short AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK;<br /> <br /> attributo di sola lettura short AD_POLICY_SKIP_AD_BREAK;<br /> };</p> </td> 
   <td><p> .. <br /> attributo di sola lettura short AD_POLICY_PLAY;<br /> attributo di sola lettura short AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> attributo di sola lettura breve AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> attributo di sola lettura breve AD_POLICY_SKIP_TO_NEGIN_AD_IN_BREAK;<br /> attributo di sola lettura short AD_POLICY_SKIP_AD_BREAK;<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>interfaccia AdPolicyMode {<br /> attributi di sola lettura brevi AD_POLICY_MODE_PLAY;<br /> attributi di sola lettura brevi AD_POLICY_MODE_SEEK;<br /> attributi di sola lettura brevi AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
   <td><p> ...<br /> {attributo readonly short AD_POLICY_MODE_PLAY;<br /> attributo readonly short AD_POLICY_MODE_SEEK;<br /> attributo readonly short AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>Interfaccia AdPolicyInfo {<br /> attributo di sola lettura AdBreakTimelineItemList <br /> adBreakTimelineItems;<br /> attributo di sola lettura AdTimelineItem adTimelineItem;<br /> attributo di sola lettura double currentTime;<br /> attributo di sola lettura doppio searchToTime;<br /> attributo di sola lettura a doppia velocità;<br /> modalità breve attributo di sola lettura; //AdPolicyMode<br /> };</p> </td> 
   <td><p>interface AdPolicyInfo {<br /> attributo di sola lettura AdBreakPlacementList <br /> adBreakPlacements;<br /> attributo di sola lettura Ad;<br /> attributo di sola lettura double currentTime;<br /> attributo di sola lettura doppio lookToTime;<br /> attributo di sola lettura a doppia velocità;<br /> attributo di sola lettura; //AdPolicyMode<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interfaccia AdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> attributo Object selectPolicyForAdBreakCallbackFunc;<br /> /*<br /> * Ad BreakTimelineItemList selectAdBreaksToPlay(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> attributo Object selectAdBreaksToPlayCallbackFunc;<br /> /*<br /> * AdPolicy selectPolicyForSeekInc toAd(AdPolicyInfo adPolicyInfo);<br /> */<br /> attributo Object selectPolicyForSeekIntoAdCallbackFunc; <br /> /**<br /> * AdBreakWatchedPolicy selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> attributo Object selectWatchedPolicyForAdBreakCallbackFunc;<br /> };</p> </td> 
   <td><p>interfaccia AdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> attributo Object selectPolicyForAdBreakFuncCallback;<br /> /*<br /> * Ad BreakPlacementList selectAdBreaksToPlay(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> attributo Object selectAdBreaksToPlayCallback;<br /> /*<br /> * AdPolicy selectPolicyForSeekIntoAd(Ad) AdPolicyInfo adPolicyInfo);<br /> */<br /> attributo Object selectPolicyForSeekIntoAdCallback; <br /> /**<br /> * AdBreakAsWatched selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> attributo Object selectWatchedPolicyForAdBreakCallback;&lt;a 19/&gt; };<br /></p> </td> 
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
   <td><p>interfaccia TimelineOperation { <br /> posizionamento dell'attributo di sola lettura ; <br /> };</p> </td> 
   <td> (Novità per la versione 2.0)</td> 
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
   <td><p>AdBreakPlacement dell'interfaccia : TimelineOperation {<br /> attributo di sola lettura AdBreak adBreak;<br /> posizionamento dell'attributo di sola lettura; // Da TimelineOperation<br /> attributi di sola lettura a doppio tempo;<br /> attributi di sola lettura a doppia durata;<br /> };</p> </td> 
   <td><p>interfaccia AdBreakPlacement {<br /> attributo di sola lettura AdBreak adBreak;<br /> posizionamento dell'attributo di sola lettura;<br /> doppio tempo dell'attributo di sola lettura;<br /> doppia durata dell'attributo di sola lettura;<br /> };</p> </td> 
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
   <td><p>interfaccia AuditudeSettings : AdvertisingMetadata { <br /> attributo DomString zoneId; <br /> attributo DomString mediaId; <br /> attributo DomString defaultMediaId ; <br /> attributo Dominio DomString ; Attributo <br /> Object targettingInfo ; <br /> attributo Object customParameters ; <br /> attributo Boolean creativePackaingEnabled ;<br /> attributo Boolean showStaticBanner ;<br /> };</p> </td> 
   <td>Funzionalità fornita dalla chiave MetadataKeys::AUDITUDE_METADATA_KEY.</td> 
  </tr> 
 </tbody> 
</table>

## Modifiche all&#39;elemento API di personalizzazione per 2.0 {#customization-api-element-changes-for}

Queste tabelle confrontano gli elementi dell’API di personalizzazione per l’SDK JavaScript TVSDK tra le versioni 1.3 e 2.0.

Tabelle in questo argomento:

* MediaPlayerItemConfig
* ContentFactory
* Configurazione di rete

### MediaPlayerItemConfig {#mediaplayeritemconfig}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interfaccia MediaPlayerItemConfig {<br /> attributo ContentFactory adFactory;<br /> attributo StringList subscriTags;<br /> <br /> attributo StringList adTags;<br /> <br /> <br /> attributo AdSignalingMode adSignalingMode;<br /> attributo CustomRangeMetadataRange;<br /> attributo NetworkConfiguration networkConfiguration;<br /> attributo AdvertisingMetadata advertisingMetadataMetadata;<br /> attributo Boolean useHardwareDecoder;<br /> };</p> </td> 
   <td><p>interfaccia MediaPlayerConfig {<br /> <br /> <br /> <br /> attributo StringList adTags;<br /> attributo StringList subscribedTags;<br /> attributo MediaPlayerClientFactory clientFactory;<br /> <br /> <br /> <br /> <br /> &lt;a11 1/&gt; };<br /></p> </td> 
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
   <td><p>interface ContentFactory {<br /> /*<br /> * AdPolicySelector retrieveAdPolicySelector(<br /> * Elemento MediaPlayerItem);<br /> */<br /> attributo retrieveAdPolicySelectorCallbackFunc;<br /> };</p> </td> 
   <td><p>interfaccia MediaPlayerClientFactory {<br /> /*<br /> * AdPolicySelector retrieveAdPolicySelector(<br /> * Elemento MediaPlayerItem);<br /> */<br /> attributo Object retrieveAdPolicySelectorFunc;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### Configurazione di rete {#networkconfiguration}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interfaccia NetworkConfiguration<br /> {<br /> attributo booleano forceNativeNetworking;<br /> attributo booleano useReindirizzaUrl;<br /> attributo Object cookieHeader;<br /> attributo booleano readSetCookieHeader;<br /> attributo int masterUpdateInterval; <br /> attributo booleano useCookieHeaderForAllRequests;<br /> attributo in readLimit;<br /> };</p> </td> 
   <td>Nella versione 1.3, alcune di queste funzionalità sono state fornite da MetadataKeys</td> 
  </tr> 
 </tbody> 
</table>

## Modifiche dell&#39;elemento API DRM per 2.0 {#drm-api-element-changes-for}

Queste tabelle confrontano gli elementi dell’API DRM per l’SDK JavaScript TVSDK tra le versioni 1.3 e 2.0.

Tabelle in questo argomento:

* Inizializzazione del flusso di lavoro DRM
* DRMAcquireLicenseSettings / DRMAuthAuthenticationMethod
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
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td>L'applicazione deve chiamare AdobePSDK.startDRMWorkflow per avviare il flusso di lavoro DRM. Senza questa chiamata, i video DRM non verranno riprodotti.<p>interfaccia AdobePSDK<br /> {<br /> void startDRMWorkFlow(<br /> DomString appStoratePath, <br /> DomString publisherId, <br /> DomString appId, <br /> DomString appVersion, <br /> boolean privacyModeOn);<br /> };</p> </td> 
   <td>L'inizializzazione è stata eseguita internamente e non è stata richiesta alcuna chiamata esplicita.</td> 
  </tr> 
 </tbody> 
</table>

### DRMAcquireLicenseSettings/DRMAuthAuthenticationMethod {#drmacquirelicensesettings-drmauthenticationmethod}

| API 2.0 | API 1.3 |
|--- |--- |
| **DRMAcquireLicenseSettings** |  |
| Nessuna modifica per la versione 2.0. | enum DRMAcquireLicenseSettings <br>{<br> const unsigned int FORCE_REFRESH = 0;<br> const unsigned int LOCAL_ONLY = 1;<br> const unsigned int ALLOW_SERVER = 2;<br> }; |
| **DRMAuthAuthenticationMethod** |  |
| Nessuna modifica per la versione 2.0. | enum DRMAuthAuthenticationMethod <br>{<br> const unsigned int UNKNOWN = 0;<br> const unsigned int ANONYMOUS = 1;<br> const unsigned int USERNAME_AND_PASSWORD = 2;<br> } |

### DRMMetadata {#drmmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td>Nessuna modifica per la versione 2.0.</td> 
   <td><p>interfaccia DRMMetadata<br /> {<br /> attributo readonly DomString serverUrl;<br /> attributo readonly DomString licenseId;<br /> attributi readonly DRMPolicyArray policy; <br /> };</p> </td> 
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
   <td><p>interfaccia DRMPlaybackTimeWindow {<br /> attributo readonly in playbackPeriodInSeconds;<br /> attributo readonly long playbackStartDate;<br /> attributo readonly long playbackEndDate;<br /> };</p> </td> 
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
   <td>Nessuna modifica per la versione 2.0.</td> 
   <td><p>interfaccia DRMLicense {<br /> attributi readonly Uint8Byte;<br /> attributo readonly Date licenseStartDate;<br /> attributo readonly Date licenseEndDate;<br /> attributo readonly Date offlineStorageStartDate;<br /> attributo readonly Date offlineStorageEndDate; <br /> attributo di sola lettura DomString serverUrl;<br /> attributo di sola lettura DomString licenseID;<br /> attributo di sola lettura DomString policyID;<br /> attributo di sola lettura DRMPlaybackTimeWindow playbackTimeWindow;<br /> attributo di sola lettura Object customProperties;<br /> }; </p> </td> 
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
   <td><p>interfaccia DRMLicenseDomain {<br /> attributo readonly DomString authenticationDomain;<br /> attributo readonly DRMAuthAuthenticationMethod authenticationMethod; <br /> attributo di sola lettura DomString serverUrl;<br /> };</p> </td> 
   <td><p>interfaccia DRMLicenseDomain {<br /> attributo readonly DomString authDomain;<br /> attributo readonly DRMAuthAuthenticationMethod authMethod; <br /> attributo di sola lettura DomString serverURL;<br /> };</p> </td> 
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
   <td><p>interfaccia DRMPolicy<br /> {<br /> attributo di sola lettura DomString authenticationDomain;<br /> attributo di sola lettura DRMAuthAuthenticationMethod;<br /> <br /> attributo di sola lettura DomString displayName;<br /> attributo di sola lettura DRMLicenseDomain licenseDomain;<br /> };</p> </td> 
   <td><p>interfaccia DRMPolicy<br /> {<br /> attributo di sola lettura DomString authDomain;<br /> attributo di sola lettura DRMAuthAuthenticationMethod authMethod;<br /> attributo di sola lettura DomString dispName;<br /> attributo di sola lettura DRMLicenseDomain licenseDomain;<br /> };</p> </td> 
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
   <td><p>Interfaccia DRMManager : EventTarget {<br /> void acquisitionLicense(DRMMetadata metadata, <br /> impostazione DRMAcquireLicenseSettings, <br /> listener DRMAquireLicenseListener);<br /> void acquisitionPreviewLicense(DRMMetadata metadata, <br /> listener DRMAquireLicenseListener);<br /> void authenticate(metadati DRMMetadata, <br /> URL DomString,<br /> DomString &amp;authenticationDomain, <br /> DomString user, <br /> password DomString, <br /> listener DRMAuthenticateListener);<br /> &lt;a1 2/&gt; DRMMetadata createMetadataFromBytes(<br /> Array Uint8Array, listener DRMErrorListener);<br /> void initialize(listener DRMOperationCompleteListener);<br /> attributo long maxOperationTime;<br /> <br /> void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> boolean forceRefresh, <br /> DRMOperationCompleteListener listener);<br /> void leaveLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> listener DRMOperationCompleteListener);<br /> <br /> void resetDRM(DRMOperationCompleteListener listener);<br /> void returnLicense(DomString serverURL, <br /> DomStringlicenseID, &lt;a222 8/&gt; DomString policyID, <br /> booleano commitImmediatamente,<br /> DRMReturnLicenseListener listener);<br /> void setAuthenticationToken(<br /> Metadati DRMMetadata, <br /> DomString authenticationDomain, &lt;a3 token Uint8Array, <br /> DRMOperationCompleteListener listener);<br /> void storeLicenseBytes(Uint8Array licenseBytes, <br /> DRMOperationCompleteListener listener);<br /> };<br /><br /><br /></p> </td> 
   <td><p>Interfaccia DRMManager : EventTarget {<br /> void acquisitionLicense(metadati DRMMetadata, <br /> impostazione DRMAcquireLicenseSettings, <br /> EventContext eventContext);<br /> void acquisitionPreviewLicense(metadati DRMMetadata, <br /> EventContext eventContext);<br /> void authenticate(DMM Metadati etadata, <br /> URL DomString,<br /> DomString &amp;authenticationDomain, <br /> Utente DomString, <br /> password DomString, <br /> EventContext eventContext);<br /> <br /> DRMMetadata createMetadataFromBytes(<br /> Array Uint8Array, EventContext eventContext);<br /> void initialize(EventContext eventContext);<br /> attributo long maxOperationTime;<br /> <br /> void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain <br /> booleano forceRefresh, <br /> EventContext eventContext);<br /> void leaveLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> EventContext eventContext);<br /> &lt;a25/ void DRM(EventContext eventContext);<br /> void returnLicense(DomString serverURL, <br /> DomString licenseID,<br /> DomString policyID, <br /> booleano commitImmediatamente,<br /> EventContext eventContext);&lt;a3 1/&gt; void setAuthenticationToken(<br /> metadati DRMMetadata, <br /> DomString authenticationDomain, <br /> Token Uint8Array, <br /> EventContext eventContext);<br /> void storeLicenseBytes(Uint8Array licenseBytes, &lt;a330 a37/&gt; EventContext eventContext);<br /> };<br /><br /><br /></p> </td> 
  </tr> 
  <tr> 
   <td><p>class DRMErrorListener : <br /> public psdkutils::PSDKInterfaceWithUserData {<br /> public:<br /> virtual void onDRMError(uint32_t major, <br /> uint32_t minor, <br /> const psdkutils: PSDKString&amp; errorString, <br /> const psdkutils::PSDKString&amp; errorServerUrl) = 0;<br /> <br /> protetto:<br /> virtuale ~DRMErrorListener() {}<br /> }</p> </td> 
   <td>Evento / Interfaccia / Descrizione 
    <ul> 
     <li>kEventDRMOperationError<p>/ DRMOperationErrorEvent</p> <p>Quando si verifica un errore durante uno dei metodi asincroni di DRMManger.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>classe DRMOperationCompleteListener : <br /> public DRMErrorListener {<br /> public:<br /> virtual void onDRMOperationComplete() = 0;<br /> <br /> protected:<br /> virtual ~DRMOperationCompleteListener() {}<br /> };</p> </td> 
   <td>Evento / Interfaccia / Descrizione 
    <ul> 
     <li>kEventDRMInitializationComplete<p>/ PSDKEvent</p> <p>Quando l’inizializzazione di DRM è completa.</p> </li> 
     <li>kEventDRMJoinLicenseDomainComplete<p>/ PSDKEvent</p> <p>Quando l’azione joinLicenseDomain() viene completata correttamente.</p> </li> 
     <li>kEventDRMLeaveLicenseDomainComplete<p>/ PSDKEvent</p> <p>Quando l’azione leaveLicenseDomain() viene completata correttamente.</p> </li> 
     <li>kEventDRMResetCompletePSDKEvent<p>/ PSDKEvent</p> <p>Quando l'azione resetDRM() viene completata correttamente.</p> </li> 
     <li>kEventDRMAuthAuthenticationTokenSet<p>/ PSDKEvent</p> <p>Quando l'azione setAuthenticationTokenSet() viene completata correttamente.</p> </li> 
     <li>kEventDRMLicenseStored<p>/ PSDKEvent</p> <p>Quando l'azione storeLicenseBytes() viene completata correttamente.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>class DRMAuthenticateListener : <br /> public DRMErrorListener {<br /> public:<br /> virtual void onAuthenticationComplete(<br /> psdkutils::PSDKImmutableByteArray* <br /> authenticationToken) = 0;<br /> <br /> protetto:<br /> virtual ~DRenticity ateListener() {}<br /> }</p> </td> 
   <td>Evento / Interfaccia / Descrizione 
    <ul> 
     <li>kEventDRMAuthAuthenticationComplete<p>/ DRMAuthAuthenticationCompleteEvent</p> <p>Quando la chiamata del metodo DRMManager::authenticate ha esito positivo.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>Classe DRMAquireLicenseListener: <br /> public DRMErrorListener {<br /> public:<br /> virtual void onLicenseAcquired(const DRMLicense*) = 0;<br /> <br /> protetto:<br /> virtuale ~DRMAquireLicenseListener() {}<br /> };</p> </td> 
   <td>Evento / Interfaccia / Descrizione 
    <ul> 
     <li>kEventDRMPreviewLicenseAcquisita<p>/ DRMLicenseAcquiredEvent</p> <p>Quando la chiamata del metodo DRMManager::acquisitionPreviewLicense ha esito positivo.</p> </li> 
     <li>kEventDRMLicenseAcquisito<p>/ DRMLicenseAcquiredEvent</p> <p>Quando la chiamata del metodo DRMManager::acquisitionLicense ha esito positivo.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>Classe DRMReturnLicenseListener: <br /> public DRMErrorListener {<br /> public:<br /> virtual void onLicenseReturnComplete(uint32_t numReturn ) = 0;<br /> <br /> protetto:<br /> virtuale ~DRMReturnLicenseListener() {}<br /> };</p> </td> 
   <td>Evento / Interfaccia / Descrizione 
    <ul> 
     <li>kEventDRMLicenseReturnComplete<p>/ DRMLicenseReturnCompleteEvent</p> <p>Quando la chiamata del metodo DRMManager::returnLicense ha esito positivo.</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## Modifiche dell&#39;elemento API di riproduzione generica per 2.0 {#generic-playback-api-element-changes-for}

Queste tabelle confrontano gli elementi API di riproduzione generici tra JavaScript TVSDK 1.3 e 2.0.

Tabelle in questo argomento:

* MediaResource
* MediaPlayer
* ABRControlParameters
* ParametriBufferControl
* Formato testo
* MediaPlayerItemLoader

### MediaResource {#mediaresource}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface MediaResource {<br /> attributo DomString url; <br /> attributo tipo breve non firmato;<br /> attributo Metadati oggetto;<br /> contiene short TYPE_HLS non firmato;<br /> const short TYPE_HDS non firmato;<br /> const unsigned short TYPE_DASH;<br /> const unsigned short TYPE_CUSTOM;<br /> const unsigned short_TYPE_UNKNOWN;<br /> };</p> </td> 
   <td><p>interfaccia MediaResource {<br /> attributo DomString url;<br /> attributo Tipo DomString;<br /> attributo Metadati oggetto;<br /> <br /> <br /> <br /> <br /> <br /> };</p> </td> 
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
   <td><p>interfaccia MediaPlayer : EventTarget<br /> {<br /> void PrepareToPlay( doppia posizione);<br /> void play();<br /> void pause();<br /> void search( doppia posizione);<br /> void searchToLocal( doppia posizione);<br /> void reset();<br /> void release();<br /> void release CurrentItem(MediaPlayerItem item);<br /> void replaceCurrentResource(MediaResource source, <br /> File di configurazione MediaPlayerItem); <br /> void suspend();<br /> void restore();<br /> void notifyClick();<br /> <br /> attributi readonly TimeRange;<br /> attributo readonly TimeRange cercaRange;<br /> attributo readonly doppio attuale Time;<br /> attributo di sola lettura doppio localTime;<br /> attributo di sola lettura TimeRange bufferedRange;<br /> attributo di sola lettura DRMManager drmManager;<br /> attributo di sola lettura MediaPlayerItem currentItem;<br /> <br /> / Stato<br /> <br /> <br /> const unsigned short PLAYER_STATUS_INITIALIZED;<br /> const unsigned short PLAYER_STATUS_PREPARING;<br /> const unsigned short PLAYER_STATUS_PREPARED;<br /> const non firmato short PLAYER_STATUS_PLAYING;<br /> const unsigned short PLAYER_STATUS_PAUSED;<br /> const unsigned short PLAYER_STATUS_SEEKING;<br /> const unsigned short PLAYER_STATUS_COMPLETE;<br /> const unsigned short PLAYER_STATUS_ERROR;<br /> const unsigned short PLAYER_STATUS_RELEASED;<br /> <br /> attributo readonly unsigned short status;<br /> <br /> attributo unsigned short volume;<br /> attributo ABRControlParameters abr ControlParameters;<br /> attributo BufferControlParameters bufferControlParameters;<br /> <br /> configura una breve VISIBLE non firmata; //Per la visibilità CC<br /> const unsigned short INVISIBLE; //Per visibilità CC<br /> attributo ccVisibility breve non firmato;<br /> attributo TextFormat ccStyle;<br /> attributo readonly PlaybackMetrics playbackMetrics;<br /> <br /> attributo double rate;<br /> attributo MediaPlayerView;&lt;a55 0/&gt; timeline dell'attributo di sola lettura;<br /> attributo double currentTimeUpdateInterval; <br /> // impostazione non supportata per 2.0<br /> };<br /></p> </td> 
   <td><p>interfaccia MediaPlayer : EventTarget<br /> {<br /> void PrepareToPlay( posizione int);<br /> void play();<br /> void pause();<br /> void search( posizione int);<br /> void searchToLocalTime( posizione int);<br /> void reset();<br /> void release();<br /> void release() void replaceCurrentItem(MediaResource source);<br /> <br /> <br /> <br /> <br /> <br /> <br /> attributo di sola lettura TimeRange playbackRange;<br /> attributo di sola lettura TimeRange SekableRange;&lt;a1 Attributo di sola lettura doppio currentTime;<br /> attributo di sola lettura doppio localTime;<br /> attributo di sola lettura TimeRange bufferedRange;<br /> attributo di sola lettura DRMManager drmManager;<br /> attributo di sola lettura MediaPlayerItem currentItem;<br /> &lt;a 23/&gt; // PlayerState<br /> const unsigned short PLAYER_STATE_IDLE;<br /> const unsigned short PLAYER_STATE_INITIALIZING;<br /> const unsigned short PLAYER_STATE_INITIALIZED;<br /> const unsigned short PLAYER_STATE_PREPARING;<br /> const unsigned short PLAYER_STATE_PREPARED;<br /> const short PLAYER_STATE_PLAYING;<br /> const unsigned short PLAYER_STATE_PAUSED;<br /> const unsigned short PLAYER_STATE_SEEKING;<br /> const unsigned short PLAYER_STATE_COMPLETE;<br /> const unsigned short PLAYER_STATE_ERROR;<br /> const unsigned short PLAYER_STATE_RELEASED;<br /> const unsigned short PLAYER_STATUS_SUSYER PENDED;<br /> attributi readonly senza stato breve firmato;<br /> <br /> attributo volume breve senza segno;<br /> attributo ABRControlParameters abrControlParameters;<br /> attributo BufferControlParameters bufferControlParameters;<br /> <br /> leggi solo non firmato breve visibile; //Per la visibilità CC<br /> solo lettura senza firma breve INVISIBLE; //Per la visibilità CC<br /> attributo abbreviato ccVisibility;<br /> attributo TextFormat ccStyle;<br /> attributo readonly PlaybackMetrics playbackMetrics;<br /> attributo MediaPlayerConfig mediaPlayerConfig;<br /> attributo a doppio rate;<br /> attributo Visualizzazione MediaPlayerView;<br /> timeline dell'attributo di sola lettura;<br /> <br /> <br /> };<br /><br /></p> </td> 
  </tr> 
  <tr> 
   <td><p>interfaccia MediaPlayerStatus<br /> {<br /> // PlayerStatus<br /> const short PLAYER_STATUS_IDLE non firmato;<br /> const unsigned short PLAYER_STATUS_INITIALIZING;<br /> const unsigned short PLAYER_STATUS_INITIALIZED;<br /> const unsigned short PLAYER_STATUS_PREPARING;<br /> const unsigned short PLAYER_STATUS_PREPARED;<br /> const unsigned short PLAYER_STATUS_PLAYING;<br /> const unsigned short PLAYER_STATUS_PAUSED;<br /> const unsigned short PLAYER_STATUS_SEEKING;&lt;a111 0/&gt; const short PLAYER_STATUS_COMPLETE senza segno;<br /> const unsigned short PLAYER_STATUS_ERROR;<br /> const unsigned short PLAYER_STATUS_RELEASED;<br /> const unsigned short PLAYER_STATUS_SUSPENDED;<br /> };<br /></p> </td> 
   <td>(Novità per la versione 2.0)</td> 
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
   <th>Interfaccia 1.3</th> 
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
   <td><p>aggiornato</p> <p>Quando il lettore multimediale ha aggiornato correttamente il contenuto multimediale.</p> </td> 
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
   <td>TtmelineUpdated</td> 
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
   <td>progresso</td> 
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
   <td>cercaBegin</td> 
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
   <td>prenotazioneRaggiunto</td> 
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
   <td>ratePlay</td> 
   <td>PlaybackRateEvent</td> 
   <td> </td> 
   <td>ratePlay</td> 
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
   <td>adClicked<br /> Quando l'utente fa clic su un annuncio.</td> 
   <td>AdClicEvent</td> 
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
   <td>searchPositionAdjusted<br /> Quando la posizione di ricerca si regola a causa di regole interne o esterne.</td> 
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
   <td>captionsAggiornato <br /> Quando un elemento del lettore multimediale viene aggiornato. Per i flussi in tempo reale/lineare, il client deve aggiornare periodicamente la risorsa multimediale per rilevare i nuovi contenuti disponibili. In questo caso, alcune caratteristiche del supporto potrebbero cambiare.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>Novità in 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>masterAggiornato <br /> Quando un elemento del lettore multimediale viene aggiornato. Per i flussi in tempo reale/lineare, il client deve aggiornare periodicamente la risorsa multimediale per rilevare i nuovi contenuti disponibili. In questo caso, alcune caratteristiche del supporto potrebbero cambiare.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>Novità in 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>playbackRangeUpdate<br /> Quando un elemento del lettore multimediale viene aggiornato. Per i flussi in tempo reale/lineare, il client deve aggiornare periodicamente la risorsa multimediale per rilevare i nuovi contenuti disponibili. In questo caso, alcune caratteristiche del supporto potrebbero cambiare.</td> 
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
   <td><p>interfaccia ABRControlParameters<br /> {<br /> const unsigned short ABR_POLICY_CONSERVATIVE = 0 ;<br /> const unsigned short ABR_POLICY_MODERATE = 1 ;<br /> const unsigned short ABR_POLICY_AGGRESIVE = 2 ;<br /> <br /> attributo non firmato abrPolicy;<br /> attributo unsigned int initialBitRate;<br /> attributo unsigned int minBitRate;<br /> attributo unsigned int maxBitRate;<br /> const unsigned short DEFAULT_ABR_INITIAL_BITRATE;<br /> const unsigned short DEFAULT_ABR_MIN_BITRATE ITRATE;<br /> const unsigned short DEFAULT_ABR_MAX_BITRATE;<br /> const ABRPolicy DEFAULT_ABR_POLICY;<br /> };</p> </td> 
   <td><p>interfaccia ABRControlParameters<br /> {<br /> const unsigned short ABR_POLICY_CONSERVATIVE = 0 ;<br /> const unsigned short ABR_POLICY_MODERATE = 1 ;<br /> const unsigned short ABR_POLICY_AGGRESIVE = 2 ;<br /> <br /> attributo non firmato abrPolicy;<br /> attributo non firmato int initialBitRate;<br /> attributo non firmato int minBitRate;<br /> attributo non firmato int maxBitRate;<br /> <br /> <br /> <br />  <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### ParametriBufferControl {#buffercontrolparameters}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interfaccia BufferControlParameters<br /> {<br /> attributo double initialBufferTime;<br /> attributo double playBufferTime;<br /> const double DEFAULT_INITIAL_BUFFER_TIME;<br /> const double DEFAULT_PLAY_BUFFER_TIME;<br /> };</p> </td> 
   <td><p>interfaccia BufferControlParameters<br /> {<br /> attributo double initialBufferTime;<br /> attributo double playBufferTime;<br /> <br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### Formato testo {#textformat}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td>Nessuna modifica per la versione 2.0</td> 
   <td><p>interfaccia TextFormat<br /> {<br /> // Color<br /> const unsigned short COLOR_DEFAULT = 0 ;<br /> const unsigned short COLOR_BLACK = 1 ;<br /> const unsigned short COLOR_GRAY = 2 ;<br /> const unsigned short COLOR_WHITE = 3 ;<br /> const COLOR_BRIGHT_WHITE senza segno = 4 ;<br /> const unsigned short COLOR_DARK_RED = 5 ;<br /> const unsigned short COLOR_RED = 6 ;<br /> const unsigned short COLOR_BRIGHT_RED = 7 ;<br /> const unsigned short COLOR_DARK_GREEN = 8 ;&lt;a 11/&gt; const unsigned short COLOR_GREEN = 9 ;<br /> const unsigned short COLOR_BRIGHT_GREEN = 10 ;<br /> const unsigned short COLOR_DARK_BLUE = 11 ;<br /> const unsigned short COLOR_BLUE = 12 ;&lt;a a15/&gt; const unsigned short COLOR_BRIGHT_BLUE = 13 ;<br /> const unsigned short COLOR_DARK_YELLOW = 14 ;<br /> const unsigned short COLOR_YELLOW = 15 ;<br /> const unsigned short COLOR_BRIGHT_YELLOW ELLOW = 16 ;<br /> const unsigned short COLOR_DARK_MAGENTA = 17 ;<br /> const unsigned short COLOR_MAGENTA = 18 ;<br /> const unsigned short COLOR_BRIGHT_MAGENTA = 19 ;<br /> const COLOR_DARK_CYAN senza segno = 20 ;<br /> const unsigned short COLOR_CYAN = 21 ;<br /> const unsigned short COLOR_BRIGHT_CYAN = 22 ;<br /> <br /> attributi readonly carattere breve senza segno;&lt;a22 7/&gt; attributo readonly unsigned short backgroundColor;<br /> attributo readonly unsigned short fillColor;<br /> attributo readonly unsigned short edgeColor;<br /> <br /> // Size<br /> const unsigned short SIZE_DEFAULT = 0 ;<br /> const SIZE_SMALL corto senza segno = 1 ;<br /> const unsigned short SIZE_MEDIUM = 2 ;<br /> const unsigned short SIZE_LARGE = 3 ;<br /> <br /> attributo readonly unsigned short size;<br /> <br /> // Font<br /> const unsigned short FONT_EDGE_DEFAULT = 0 ;<br /> const unsigned short FONT_EDGE_NONE = 1 ;<br /> const unsigned short FONT_EDGE_RAISED = 2 ;<br /> const unsigned short FONT_EDGE_DEPRESSED = 3 ;&lt;a4 4/&gt; const unsigned short FONT_EDGE_UNIFORM = 4 ;<br /> const unsigned short FONT_EDGE_DROP_SHADOW_LEFT = 5 ;<br /> const unsigned short FONT_EDGE_DROP_SHADOW_RIGHT = 6 ;<br /> readonly attribute unsigned short fontEdge;<br /> <br /> // Font<br /> const unsigned short FONT_DEFAULT = 0 ;<br /> const unsigned short FONT_MONOSPACED_WITH_SERIFS = 1 ;<br /> const unsigned short FONT_PROPORTIONAL_WITH_SERIFS = 2 ;&lt;a5 3/&gt; const unsigned short FONT_MONSPACED_WITHOUT_SERIFS = 3 ;<br /> const unsigned short FONT_CASUAL = 4 ;<br /> const unsigned short FONT_CURSIVE = 5 ;<br /> const unsigned short FONT_SMALL_readALS = 6 ;<br /> solo attributo carattere breve senza segno;<br /> attributo di sola lettura carattere breve senza segno Opacity;<br /> attributo di sola lettura senza segno backgroundOpacity;<br /> attributo di sola lettura senza segno short fillOpacity;<br /> attributo di sola lettura senza segno DEFAULT_OPACITY;<br /> };<br /><br /><br /><br /><br /></p> </td> 
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
   <td><p>interfaccia MediaPlayerItemLoader:<br /> {<br /> void load(MediaResource, long resourceId,<br /> Listener ItemLoaderListener, <br /> Configurazione MediaPlayerItemConfig) ;<br /> void cancel();<br /> attributi readonly MediaPlayerItem currentItem;<br /> };</p> </td> 
   <td>Novità per 2.0</td> 
  </tr> 
  <tr> 
   <td><p>interfaccia ItemLoaderListener<br /> {<br /> //onLoadCompleteCallbackFunc(MediaPlayerItem)<br /> var onLoadCompleteCallbackFunc;<br /> //onErrorCallbackFunc(PSDKErrorCode)<br /> var onErrorCallbackFunc; a5/&gt; }<br /></p> </td> 
   <td>Novità per 2.0</td> 
  </tr> 
 </tbody> 
</table>

## Modifiche dell&#39;elemento API per le caratteristiche dei file multimediali per 2.0 {#media-characteristics-api-element-changes-for}

Queste tabelle confrontano gli elementi API delle caratteristiche multimediali per l’SDK C++ TVSDK tra le versioni 1.3 e 2.0.

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
   <td><p>interfaccia MediaPlayerItem {<br /> attributo in sola lettura MediaResource;<br /> attributo in sola lettura long resourceId;<br /> attributo in sola lettura booleano live;<br /> <br /> attributo in sola lettura booleano hasAlternateAudio;<br /> attributo in sola lettura AudioTrackList audioTracks;<br /> attributo in sola lettura AudioTrack selectedAudio Track;<br /> void selectAudioTrack(AudioTrack track); <br /> <br /> l'attributo booleano di sola lettura haClosedCaptions;<br /> attributo di sola lettura ClosedCaptionsTrackList closedCaptionsTracks;<br /> attributo di sola lettura ClosedCaptionsTrack selectedClosedCaptionsTrack;<br /> void selectClosedCaptionsTrack(&lt;a 13/&gt; brano ClosedCaptionsTrack); <br /> <br /> attributo di sola lettura boolean hasTimedMetadata;<br /> attributo di sola lettura TimedMetadataList timedMetadata;<br /> attributo di sola lettura booleano dinamico;<br /> <br /> attributo di sola lettura boolean isProtected;<br /> solo lettura attributo DRMMetadataInfoList drmMetadataInfos;<br /> attributi di sola lettura Profili ProfileList;<br /> attributo di sola lettura Profilo selectedProfile;<br /> <br /> attributo di sola letturaTrucco booleanoPlaySupported;<br /> attributo di sola lettura FloatArray availablePlayback Tassi;<br /> attributo di sola lettura float selectedPlaybackRate;<br /> <br /> <br /> attributo di sola lettura MediaPlayer mediaPlayer;<br /> attributo di sola lettura MediaPlayerItemConfig;<br /> };<br /></p> </td> 
   <td><p>interfaccia MediaPlayerItem {<br /> attributo in sola lettura MediaResource;<br /> attributo in sola lettura long resourceId;<br /> attributo in sola lettura booleano live;<br /> <br /> attributo in sola lettura booleano hasAlternateAudio;<br /> attributo in sola lettura AudioTrackAudioTracks;<br /> attributo AudioTrack selectedAudioAudioTrack;<br /> <br /> <br /> l'attributo booleano di sola lettura haClosedCaptions;<br /> l'attributo di sola lettura ClosedCaptionsTrackList ccTracks;<br /> l'attributo ClosedCaptionsTrack selectedCCTrack;<br /> <br /> <br /> attributo di sola lettura booleano hasTimedMetadata;<br /> attributo di sola lettura TimedMetadataList timedMetadata;<br /> attributo di sola lettura booleano dynamic;<br /> <br /> attributo di sola lettura booleano isProtected;<br /> attributo di sola lettura DRMMetadata InformazioniInfoList drmMetadataInfos;<br /> attributi di sola lettura Profili di ProfileList;<br /> <br /> <br /> attributo di sola lettura booleanoPlaySupported;<br /> attributo di sola lettura Int32Array availablePlaybackRates;<br /> &lt;a attributo di sola lettura StringList adTags;<br /> <br /> attributo di sola lettura MediaPlayer mediaPlayer;<br /> <br /> };<br /><br /></p> </td> 
  </tr> 
 </tbody> 
</table>

### Track / AudioTrack / ClosedCaptionsTrack {#track-audiotrack-closedcaptionstrack}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface Track<br /> {<br /> nome DomString dell'attributo di sola lettura;<br /> lingua DomString dell'attributo di sola lettura;<br /> attributo booleano predefinito di sola lettura;<br /> attributo booleano autoSelect;<br /> }; </p> </td> 
   <td>Novità per 2.0</td> 
  </tr> 
  <tr> 
   <td><p>interfaccia AudioTrack : Track<br /> {<br /> nome dell'attributo di sola lettura DomString; //FromTrack<br /> lingue DomString dell'attributo readonly;//FromTrack<br /> attributi booleani predefiniti di sola lettura; // Da Track<br /> attributo booleano autoSelect;//FromTrack<br /> <br /> l'attributo readonly non firmato int pid;<br /> };</p> </td> 
   <td><p>interfaccia AudioTrack<br /> {<br /> nome attributo di sola lettura DomString;<br /> linguaggio DomString attributo di sola lettura; <br /> attributo booleano predefinito di sola lettura;<br /> attributo booleano autoSelect;<br /> attributo booleano forzato di sola lettura;<br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td>Nessuna modifica per la versione 2.0</td> 
   <td><p>interfaccia AudioTrackList<br /> {<br /> attributo readonly a lunga lunghezza senza segno;<br /> getter AudioTrack (indice lungo senza segno);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface ClosedCaptionsTrack : Track<br /> {<br /> nome dell'attributo di sola lettura DomString; //FromTrack<br /> lingue DomString dell'attributo readonly;//FromTrack<br /> attributi booleani predefiniti di sola lettura; // DallTrack<br /> attributo booleano autoSelect;//FromTrack<br /> <br /> <br /> const unsigned short SERVICE_608_CAPTIONS = 0;<br /> const unsigned short SERVICE_708_CAPTIONS = 1;<br /> const unsigned short SERVICE_WEB_VTT _CAPTIONS = 2;<br /> attributo di sola lettura unsigned short serviceType;<br /> attributo di sola lettura booleano forzato;<br /> };</p> </td> 
   <td><p>interfaccia ClosedCaptionsTrack<br /> {<br /> Attributo di sola lettura DomString name;<br /> attributo di sola lettura DomString language;<br /> attributo di sola lettura booleano predefinito;<br /> <br /> <br /> attributo di sola lettura booleano attivo;<br /> <br /> <br /> <br /> a11/&gt; <br /> };<br /></p> </td> 
  </tr> 
  <tr> 
   <td>Nessuna modifica per la versione 2.0</td> 
   <td><p>interfaccia ClosedCaptionsTrackList<br /> {<br /> attributi di sola lettura a lunga lunghezza senza firma;<br /> getter ClosedCaptionsTrack(unsigned long index);<br /> };</p> </td> 
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
   <td>Profilo: Nessuna modifica per la versione 2.0</td> 
   <td><p>profilo interfaccia<br /> {<br /> attributo readonly non firmato int width;<br /> attributo readonly non firmato int height;<br /> attributo readonly non firmato int bitRate;<br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td>Elenco profili: Nessuna modifica per la versione 2.0</td> 
   <td><p>interfaccia ProfileList<br /> {<br /> attributo readonly a lunga lunghezza senza segno;<br /> getter Profile(unsigned long index);<br /> };</p> </td> 
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
   <td><strong>DRMMetadataInfo</strong>: Nessuna modifica per la versione 2.0</td> 
   <td><p>interfaccia DRMMetadataInfo<br /> { <br /> attributi di sola lettura DRMMetadata metadata;<br /> attributo di sola lettura long prefetchTimestamp;<br /> attributo di sola lettura TimeRange;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>DRMMetadataInfoList</strong>: Nessuna modifica per la versione 2.0</td> 
   <td><p>interfaccia DRMMetadataInfoList<br /> {<br /> attributi di sola lettura a lunga lunghezza senza firma;<br /> getter DRMMetadataInfo(indice lungo senza segno);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

## Mappatura degli errori C++ alle eccezioni in lingue diverse {#mapping-c-errors-to-exceptions-in-different-languages}

È possibile mappare i codici di errore C++ alle eccezioni in lingue diverse.

Il PSDK di C++ dispone di un criterio di &quot;nessun lancio&quot; per le sue API. La maggior parte dei metodi API restituisce un valore PSDKErrorCode per indicare se il metodo è stato eseguito correttamente. Gli errori asincroni vengono notificati tramite gli eventi di errore.

I criteri PSDK per ActionScript e JAVA sono diversi. La maggior parte degli errori genera un ArgumentError o IllegalStateException per indicare che la parte sincrona del metodo non può essere eseguita. Queste eccezioni non vengono rilevate e il codice dell&#39;applicazione è responsabile della gestione delle eccezioni. In genere forniscono informazioni utili sul motivo per cui la chiamata del metodo non è riuscita. Ad esempio, se il comando PrepareToPlay viene chiamato in uno stato non valido, viene generata la seguente eccezione:

```shell
throw new IllegalStateException("Invalid player state. prepareToPlay method 
must be called only once after replaceCurrentItem or replaceCurrentResource method.");
```

Anche ActionScript/JAVA genera eccezioni dai costruttori per indicare che alcuni oggetti interni sono stati creati in modo errato. Queste eccezioni vengono gestite internamente e non vengono propagate all&#39;applicazione. Le eccezioni verranno incluse in una notifica di avviso inviata all’applicazione

Ad esempio, se non è stato trovato alcun file multimediale valido per la risposta all&#39;annuncio ricevuta, non è possibile creare un oggetto o un annuncio pubblicitario valido. Di conseguenza, non viene inserito alcun annuncio nella timeline e viene inviata una notifica NotificationEvent.OperationFailed .

I codici di errore o di avviso ricevuti in modo asincrono dal motore video di Adobe (AVE) vengono inviati all’applicazione come eventi normali. L&#39;evento di notifica contiene tutti i codici di errore ricevuti e tutti i metadati aggiuntivi, come l&#39;URL, l&#39;identificatore della risorsa, l&#39;handle e così via. Se l&#39;errore è grave e la riproduzione del contenuto multimediale corrente non può continuare, MediaPlayer passa allo stato ERROR e all&#39;evento callback StatusChanged o MediaPlayerStatusChanged.STATUS_CHANGED viene inviato. Se la riproduzione può continuare, viene inviato un normale evento di notifica.

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
   <td>kECInvalidArgument</td> 
   <td> </td> 
   <td>IllegalArgumentException</td> 
   <td>ArgumentError</td> 
   <td>Eccezione con codice = 1, descrizione = "INVALID_ARGUMENT" e AdditionalInfo= &lt;as passato dal metodo che ha lanciato questa eccezione&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNullPointer</td> 
   <td> </td> 
   <td>IllegalArgumentException</td> 
   <td>ArgumentError</td> 
   <td>Eccezione con codice = 2, descrizione = "GENERIC_ERROR" e AdditionalInfo= &lt;as passato dal metodo che ha generato questa eccezione&gt;</td> 
  </tr> 
  <tr> 
   <td>kECIllegalState</td> 
   <td> </td> 
   <td>EccezioneStatoIllegale</td> 
   <td>EccezioneStatoIllegale</td> 
   <td>Eccezione con codice = 3, descrizione = "ILLEGAL_STATE" e AdditionalInfo= &lt;as passato dal metodo che ha lanciato questa eccezione&gt;</td> 
  </tr> 
  <tr> 
   <td>kECInterfaceNotFound</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 4, descrizione = "GENERIC_ERROR" e AdditionalInfo= &lt;as passato dal metodo che ha generato questa eccezione&gt;</td> 
  </tr> 
  <tr> 
   <td>kECCreationFailed</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 5, descrizione = "CREATION_FAILED" e AdditionalInfo= &lt;as passato dal metodo che ha lanciato questa eccezione&gt;</td> 
  </tr> 
  <tr> 
   <td>kECUnsupportedOperation</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 5, descrizione = "CREATION_FAILED" e AdditionalInfo= &lt;as passato dal metodo che ha lanciato questa eccezione&gt;</td> 
  </tr> 
  <tr> 
   <td>kELataNotAvailable</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 7, descrizione = "DATA_NOT_AVAILABLE" e AdditionalInfo= &lt;as passato dal metodo che ha generato questa eccezione&gt;</td> 
  </tr> 
  <tr> 
   <td>kECSeekError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 8, descrizione = "SEEK_ERROR" e AdditionalInfo= &lt;as passato dal metodo che ha lanciato questa eccezione&gt;</td> 
  </tr> 
  <tr> 
   <td>kECUnsupportedFeature</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 9, descrizione = "UNSUPPORTED_FEATURE" e AdditionalInfo= &lt;as passato dal metodo che ha generato questa eccezione&gt;</td> 
  </tr> 
  <tr> 
   <td>kECRangeError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 10, descrizione = "RANGE_ERROR" e AdditionalInfo= &lt;as passato dal metodo che ha generato questa eccezione</td> 
  </tr> 
  <tr> 
   <td>kECCodecNotSupported</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 11, descrizione = "CODEC_NOT_SUPPORTED" e AdditionalInfo= &lt;as passato dal metodo che ha generato questa eccezione&gt;</td> 
  </tr> 
  <tr> 
   <td>kECMediaError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 12, descrizione = "MEDIA_ERROR" e AdditionalInfo= &lt;as passato dal metodo che ha generato questa eccezione&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNetworkError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 13, descrizione = "NETWORK_ERROR" e additionalInfo= &lt;as passato dal metodo che ha generato questa eccezione&gt;</td> 
  </tr> 
  <tr> 
   <td>kECGenericError</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Error o MediaPlayerNotification.Warning</td> 
   <td>MediaError o NotificationEvent</td> 
   <td>Eccezione con codice = 14, descrizione = "GENERIC_ERROR" e AdditionalInfo= &lt;as passato dal metodo che ha generato questa eccezione&gt;</td> 
  </tr> 
  <tr> 
   <td>kECInvalidSeekTime</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 15, descrizione = "INVALID_SEEK_TIME" e AdditionalInfo= &lt;as passato dal metodo che ha generato questa eccezione&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAudioTrackError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 16, descrizione = "AUDIO_TRACK_ERROR" e AdditionalInfo= &lt;as passato dal metodo che ha generato questa eccezione&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAccessFromDifferente<p>ThreadError</p> </td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 17, descrizione = "GENERIC_ERROR" e AdditionalInfo= &lt;as passato dal metodo che ha generato questa eccezione&gt;</td> 
  </tr> 
  <tr> 
   <td>kECElementNotFound</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 18, descrizione = "GENERIC_ERROR" e AdditionalInfo= &lt;as passato dal metodo che ha generato questa eccezione</td> 
  </tr> 
  <tr> 
   <td>kECNotImplemented</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 19, descrizione = "GENERIC_ERROR" e AdditionalInfo= &lt;as passato dal metodo che ha generato questa eccezione&gt;</td> 
  </tr> 
  <tr> 
   <td>kECPlaybackOperationFailed</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Eccezione con codice = 200, descrizione = "PLAYBACK_OPERATION_FAILED" e AdditionalInfo= &lt;as passato by method che ha lanciato questa eccezione&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNativeWarning</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Warning</td> 
   <td>NotificationEvent</td> 
   <td>Eccezione con codice = 201, descrizione = "NATIVE_WARNING" e AdditionalInfo= &lt;as passato dal metodo che ha generato questa eccezione</td> 
  </tr> 
  <tr> 
   <td>kECAdResolverFailed</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Warning</td> 
   <td>-</td> 
   <td>Eccezione con codice = 202, descrizione = "AD_RESOLVER_FAILED" e AdditionalInfo= &lt;as passato dal metodo che ha generato questa eccezione&gt;</td> 
  </tr> 
 </tbody> 
</table>

## Modifiche agli elementi API di Utility e Helper per per la versione 2.0 {#utility-and-helper-api-element-changes-for}

Queste tabelle confrontano gli elementi API Utility e Helper per il TVSDK JavaScript tra le versioni 1.3 e 2.0.

Tabelle in questo argomento:

* Versione
* TimeRange
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
   <td><p>interfaccia Versione<br /> {<br /> attributi di sola lettura Versione DomString;<br /> attributi di sola lettura Descrizione DomString;<br /> attributi di sola lettura long major;<br /> attributi di sola lettura long minor;<br /> revisione attributi di sola lettura;<br /> attributi di sola lettura long apiVersion;<br /> };</p> </td> 
   <td><p>interfaccia Versione<br /> {<br /> attributi di sola lettura Versione DomString;<br /> attributo di sola lettura Descrizione DomString;<br /> attributo di sola lettura DomString principale;<br /> attributo di sola lettura DomString secondario;<br /> attributo di sola lettura Revisione DomString;<br /> attributo di sola lettura DomString apiVersion;<br /> } ;</p> </td> 
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
   <td>Nessuna modifica per la versione 2.0</td> 
   <td><p>interfaccia TimeRange<br /> {<br /> attributo readonly unsigned long begin;<br /> attributo readonly unsigned long end;<br /> attributo readonly unsigned long duration;<br /> };</p> </td> 
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
   <td>Nessuna modifica per la versione 2.0</td> 
   <td><p>interfaccia QOSProvider<br /> {<br /> void attachMediaPlayer(MediaPlayer player);<br /> void detachMediaPlayer();<br /> <br /> attributi readonly DeviceInformation deviceInformation;<br /> attributo readonly PlaybackInformation playbackInformation;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### Informazioni sul dispositivo {#deviceinformation}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interfaccia DeviceInformation<br /> {<br /> attributo readonly DomString os;<br /> <br /> <br /> <br /> attributo readonly DomString id;<br /> attributo readonly int densitàDPI;<br /> attributo readonly int heightPixels;<br /> attributo readonly int widthPixels;<br /> attributo di sola lettura booleano searchToKeyFrame;<br /> };</p> </td> 
   <td><p>interfaccia DeviceInformation<br /> {<br /> attributo di sola lettura DomString os;<br /> attributo di sola lettura int sdk;<br /> modello DomString di attributi di sola lettura;<br /> produttore di attributi di sola lettura DomString;<br /> attributo di sola lettura DomString id;<br /> attributo di sola lettura int densityDPI;<br /> readonly attributo int heightPixels;<br /> attributo readonly int widthPixels;<br /> <br /> };</p> </td> 
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
   <td>Nessuna modifica per la versione 2.0</td> 
   <td><p>interfaccia LoadInfo<br /> {<br /> attributo readonly DomString url;<br /> attributo readonly int size;<br /> attributo readonly doppio downloadDuration;<br /> attributo readonly int periodIndex;<br /> attributo readonly double mediaDuration;<br /> attributo readonly short TRACK_TYPE_FRAGMENT;<br /> readonly attributo breve TRACK_TYPE_TRACK;<br /> attributo di sola lettura breve TRACK_TYPE_MANIFEST;<br /> tipo di attributo di sola lettura;<br /> attributo di sola lettura DomString trackName;<br /> attributo di sola lettura DomString trackType;<br /> attributo di sola lettura int trackIndex;&lt;a1 3/&gt; };<br /></p> </td> 
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
   <td>Nessuna modifica per la versione 2.0</td> 
   <td><p>interfaccia View<br /> {<br /> readonly attribute unsigned short x;<br /> readonly attribute unsigned short y;<br /> readonly attribute unsigned short width;<br /> readonly attribute unsigned short height;<br /> <br /> void setSize(unsigned short width, unsigned short height);<br /> void setPos(unsigned short) x, y senza segno);<br /> }</p> </td> 
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
   <td><p>interfaccia PlaybackInformation<br /> {<br /> attributi di sola lettura doppio timeToFirstByte;<br /> attributi di sola lettura doppio timeToLoad;<br /> attributi di sola lettura doppio timeToStart;<br /> attributi di sola lettura doppio timeToFail;<br /> attributi di sola lettura in totalSecondsPlayed;<br /> attributi di sola lettura totalSecondsSpent;<br /> attributo readonly double frameRate;<br /> attributo readonly int dropFrameCount;<br /> attributo readonly in perceppurchasedBandwidth;<br /> attributo readonly int bitrate;<br /> attributo readonly double bufferTime;<br /> attributo readonly int bufferLength;&lt;a1; a13/&gt; attributo readonly in emptyBufferCount;<br /> attributo readonly doppio bufferingTime;<br /> };<br /></p> </td> 
   <td><p>interfaccia PlaybackInformation<br /> {<br /> attributi di sola lettura doppio timeToFirstByte;<br /> attributi di sola lettura doppio timeToLoad;<br /> attributi di sola lettura doppio timeToStart;<br /> attributi di sola lettura doppio timeToFail;<br /> attributi di sola lettura in totalSecondsPlayed;<br /> attributi di sola lettura totalSecondsSpent;<br /> attributo readonly double frameRate;<br /> attributo readonly int dropFrameCount;<br /> <br /> attributo readonly int bitrate;<br /> attributo readonly double bufferTime;<br /> attributo readonly int bufferLength;<br /> attributo readonly emptyBufferCount;<br /> readonly attributo double bufferingTime;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

## Risorse utili {#helpful-resources}

* Consulta la documentazione completa della guida nella pagina [Informazioni e supporto per Adobe Primetime](https://helpx.adobe.com/support/primetime.html) .
