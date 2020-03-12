---
description: Il server manifesto restituisce gli elenchi di riproduzione principali in formato M3U8, in conformità allo standard di streaming HTTP Live proposto. È costituito da un insieme di flussi di trasporto (TS) variabili, ciascuno contenente rappresentazioni dello stesso contenuto per diversi bitrate e formati. L'inserimento di annunci Adobe Primetime aggiunge il tag di direttiva EXT-X-MARKER, che deve essere interpretato dai lettori video client.
seo-description: Il server manifesto restituisce gli elenchi di riproduzione principali in formato M3U8, in conformità allo standard di streaming HTTP Live proposto. È costituito da un insieme di flussi di trasporto (TS) variabili, ciascuno contenente rappresentazioni dello stesso contenuto per diversi bitrate e formati. L'inserimento di annunci Adobe Primetime aggiunge il tag di direttiva EXT-X-MARKER, che deve essere interpretato dai lettori video client.
seo-title: Direttiva EXT-X MARKER
title: Direttiva EXT-X MARKER
uuid: e349bf89-b196-47b4-a362-9913fa28b2c6
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9

---


# Direttiva EXT-X MARKER {#ext-x-marker-directive}

Il server manifesto restituisce gli elenchi di riproduzione principali in formato M3U8, in conformità allo standard di streaming HTTP Live proposto. È costituito da un insieme di flussi di trasporto (TS) variabili, ciascuno contenente rappresentazioni dello stesso contenuto per diversi bitrate e formati. L&#39;inserimento di annunci Adobe Primetime aggiunge il tag di direttiva EXT-X-MARKER, che deve essere interpretato dai lettori video client.

Per informazioni dettagliate sul tag EXT-X-MARKER, consultate [Adobe Primetime HTTP Live Streaming Profile](https://wwwimages2.adobe.com/content/dam/acom/en/devnet/primetime/PrimetimeHLS_April2014.pdf).

>[!NOTE]
>
>Questa funzionalità è disponibile solo se l&#39;URL del server del manifesto di avvio non contiene il `pttrackingmode` parametro.

>[!NOTE]
>
>Il tag EXT-X-MARKER viene aggiunto ai segmenti di annunci e non ai segmenti di contenuto.

Lo standard bozza di [HTTP Live Streaming](https://tools.ietf.org/html/draft-pantos-http-live-streaming-23) descrive il contenuto e il formato delle playlist diverse. Il tag EXT-X-MARKER indirizza il client a richiamare un callback. Contiene i seguenti componenti:

* **ID** Identificatore univoco (stringa) per questo evento di callback nel contesto del flusso del programma.

* **TYPE** Tipo (stringa) dell&#39;evento di callback: PodBegin, PodEnd, PrerollPodBegin, PrerollPodEnd o AdBegin

* **DURATA** Durata (in secondi) dall&#39;inizio del segmento che contiene il tag per il quale la direttiva rimane valida.

* **OFFSET** Facoltativo. L&#39;offset (in secondi) relativo all&#39;inizio della riproduzione del segmento, quando il callback deve essere invocato.

   * `PodBegin` e `PrerollPodBegin` contengono informazioni sul beacon nell&#39;attributo DATA e vengono attivate all&#39;inizio del segmento. Quindi il `OFFSET` tag non è disponibile qui.

   * `AdBegin` contiene informazioni sul beacon nell&#39;attributo DATA e i tag impression vengono attivati all&#39;inizio del segmento. Quindi anche il `OFFSET` tag non è disponibile qui.

   * `PodEnd` e `PrerollPodEnd` contengono informazioni sul beacon nell&#39;attributo DATA, ma vengono attivate alla fine del segmento corrente perché è previsto che tali tag vengano attivati alla fine dell&#39;ultimo segmento dell&#39;ultimo annuncio nel contenitore. In questo caso, `OFFSET` è impostato per `<duration of segment>` specificare che il beacon deve essere attivato alla fine del segmento corrente.

* **Stringa con codifica DATA** Base64 racchiusa tra virgolette doppie contenenti i dati da trasmettere all’applicazione quando si richiama il callback. Contiene informazioni di tracciamento annunci conformi alle specifiche VMAP1.0 e VAST3.0.

* **COUNT** Numero di annunci che verranno cuciti nell&#39;interruzione di annuncio.

   Applicabile solo se il componente TYPE è impostato su PodBegin o PrerollPodBegin.

* **BREAKDUR** Durata totale (in secondi) dell&#39;interruzione pubblicitaria riempita.

   Applicabile solo se il componente TYPE è impostato su PodBegin o PrerollPodBegin.

Durante la costruzione del callback, interpretate i componenti EXT-X-MARKER come segue:

* Quando il tag contiene `OFFSET`, avvia il callback in corrispondenza dell’offset specificato relativo all’inizio della riproduzione del contenuto in quel segmento. In caso contrario, viene attivata la richiamata non appena inizia la riproduzione del contenuto in quel segmento.
* Utilizzate `DURATION` per monitorare l&#39;avanzamento del contenuto dell&#39;annuncio e per richiedere gli URL per il tracciamento degli eventi.
* Passa `ID`, `TYPE`e `DATA` al callback.

Utilizzate i `PrerollPodBegin`e `PrerollPodEnd` i valori per `TYPE` decidere quale segmento TS riprodurre per primo nei flussi live/lineari.

>[!NOTE]
>
>I valori `PrerollPodBegin`, e `PrerollPodEnd` sono disponibili solo quando un annuncio pre-roll viene inserito in un flusso live.

Il server manifesto include i tag EXT-X-MARKER nei segmenti seguenti:

* Il primo segmento nell&#39;interruzione dell&#39;annuncio, per tracciare l&#39;inizio di un contenitore annuncio.
* Il primo segmento dell&#39;annuncio, per tenere traccia dell&#39;inizio/completamento/avanzamento di un singolo annuncio all&#39;interno di un contenitore di annunci.
* L&#39;ultimo segmento nell&#39;interruzione dell&#39;annuncio, per tenere traccia della fine di un contenitore annuncio.

Il server manifesto invia un documento `VMAP1.0-conformant` XML per tenere traccia dell’inizio e della fine di ogni interruzione di annuncio. Si tratta di una versione filtrata della risposta VMAP1.0 effettiva restituita dal server di annunci e contiene principalmente gli eventi di tracciamento come mostrato di seguito:

```xml
<?xml version="1.0"?> 
<AdTrackingFragments> 
<AdTrackingFragment> 
<vmap:VMAP xmlns:vmap="https://www.iab.net/vmap-1.0" version="1.0"> 
    <vmap:AdBreak breakType="linear" breakId="mypre" timeOffset="start"> 
        <vmap:TrackingEvents> 
            <vmap:Tracking event="breakStart"> 
                https://MyServer.com/breakstart.gif 
            </vmap:Tracking> 
            <vmap:Tracking event="breakEnd"> 
                https://MyServer.com/breakend.gif 
            </vmap:Tracking> 
            <vmap:Tracking event="error"> 
                https://MyServer.com/error.gif 
            </vmap:Tracking> 
        </vmap:TrackingEvents> 
    </vmap:AdBreak> 
</vmap:VMAP> 
</AdTrackingFragment> 
</AdTrackingFragments>
```

Per ogni annuncio creativo il server manifesto inserisce nel contenuto del programma, invia un documento XML conforme a VAST3.0 per tenere traccia di tale annuncio. Ogni documento XML contiene un `<InLine>` elemento che descrive l&#39;annuncio pubblicitario lineare inserito, o un `<Wrapper>` elemento nel caso di annunci wrapper (vale a dire, annunci collegati o reindirizzati), e tutti gli annunci ed estensioni associati. Se la risposta VAST contiene un attributo di sequenza, ad esempio quando l&#39;annuncio fa parte di un contenitore di annunci, il documento include tale attributo. Segue un esempio di documento XML conforme alla versione VAST3.0 per il tracciamento di un singolo annuncio:

```xml
<?xml version="1.0"?> 
<AdTrackingFragments> 
<AdTrackingFragment> 
<VAST xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"  
      version="3.0"  
      xsi:noNamespaceSchemaLocation="https://service.videoplaza.com/schema/iab/vast-3.0.xsd"> 
<Ad id="903395"> 
    <InLine> 
      <AdSystem version="1.0">Auditude</AdSystem> 
      <AdTitle/> 
      <Error>https://ad.qa.auditude.com/adserver/?ErrAd1=[ERRORCODE]</Error> 
      <Impression id="urn:aeid:903395">https://ad.qa.auditude.com/adserver/e?type=adimp&amp; 
                 cid=127860991&amp; 
                 z=50183&amp; 
                 a=903395&amp; 
                 s=ef8c51dc&amp; 
                 t=1355309735&amp; 
                 w=100000&amp; 
                 uid=_CxLm0b1SeKD8KXco__5TQ&amp; 
                 l=1355280906&amp; 
                 u=956c3cd141086a1da44dcae8ea4ed14a&amp; 
                 br=1&amp; 
                 sq=1&amp; 
                 pod=id:1,ctype:l,ptype:p,dur:400,lot:8,cpos:1,edur:400,elot:8&amp; 
                 ax=0,0,1720,0/?ContentPosition=[CONTENTPLAYHEAD] 
                               ?Cashcash=[CACHEBUSTING] 
                               ?Asset=[ASSETURI] 
      </Impression> 
      <Creatives> 
        <Creative> 
          <Linear> 
            <Duration>00:00:15</Duration> 
            <TrackingEvents> 
              ... 
              <Tracking event="firstQuartile"> 
                https://ad.qa.auditude.com/adserver/e?type=AD_PROGRESS&amp; 
                  a=903395&amp; 
                  a1=105&amp; 
                  ref=urn:asset:903395:105&amp; 
                  unit=percent&amp; 
                  progress=25&amp; 
                  cid=127860991&amp; 
                  z=50183&amp; 
                  a=903395&amp; 
                  s=ef8c51dc&amp; 
                  t=1355309735&amp; 
                  w=100000&amp; 
                  uid=_CxLm0b1SeKD8KXco__5TQ&amp; 
                  l=1355280906&amp; 
                  u=956c3cd141086a1da44dcae8ea4ed14a&amp; 
                  br=1&amp; 
                  sq=1&amp; 
                  pod=id:1,ctype:l,ptype:p,dur:400,lot:8,cpos:1,edur:400,elot:8&amp; 
                  ax=0,0,1720,0/?ContentPosition=[CONTENTPLAYHEAD] 
                                ?Cashcash=[CACHEBUSTING] 
                                ?Asset=[ASSETURI] 
              </Tracking>                
              <Tracking event="midpoint"> 
                https://ad.qa.auditude.com/adserver/e?type=AD_PROGRESS&amp; 
                  a=903395&amp; 
                  a1=105&amp; 
                  ref=urn:asset:903395:105&amp; 
                  unit=percent&amp; 
                  progress=50&amp; 
                  cid=127860991&amp; 
                  z=50183&amp; 
                  a=903395&amp; 
                  s=ef8c51dc&amp; 
                  t=1355309735&amp; 
                  w=100000&amp; 
                  uid=_CxLm0b1SeKD8KXco__5TQ&amp; 
                  l=1355280906&amp; 
                  u=956c3cd141086a1da44dcae8ea4ed14a&amp; 
                  br=1&amp; 
                  sq=1&amp; 
                  pod=id:1,ctype:l,ptype:p,dur:400,lot:8,cpos:1,edur:400,elot:8&amp; 
                  ax=0,0,1720,0/?ContentPosition=[CONTENTPLAYHEAD] 
                                ?Cashcash=[CACHEBUSTING] 
                                ?Asset=[ASSETURI] 
              </Tracking> 
              <Tracking event="firstQuartile"> 
                https://www.Tweeeen.com/?ContentPosition=[CONTENTPLAYHEAD] 
                                       ?Cashcash=[CACHEBUSTING] 
                                       ?Asset=[ASSETURI] 
              </Tracking> 
              <Tracking event="midpoint"> 
                https://www.Fiftyyyy.com/?ContentPosition=[CONTENTPLAYHEAD] 
                                        ?Cashcash=[CACHEBUSTING] 
                                        ?Asset=[ASSETURI] 
              </Tracking> 
              ... 
            </TrackingEvents> 
            <VideoClicks> 
              <ClickTracking> 
                https://www.MP4-Vid-ClickTrack.com/?ContentPosition=[CONTENTPLAYHEAD] 
                                                  ?Cashcash=[CACHEBUSTING] 
                                                  ?Asset=[ASSETURI] 
              </ClickTracking> 
              <ClickThrough> 
                https://www.cnn.com/?ContentPosition=[CONTENTPLAYHEAD] 
                                   ?Cashcash=[CACHEBUSTING] 
                                   ?Asset=[ASSETURI] 
              </ClickThrough> 
              ... 
            </VideoClicks> 
            <AdParameters>campaign_id=7012</AdParameters> 
            <MediaFiles> 
              ...            
            </MediaFiles> 
          </Linear> 
        </Creative> 
        <Creative> 
          <CompanionAds> 
            <Companion id="103" width="300" height="250"> 
              <StaticResource creativeType="image/jpeg"> 
                https://ad.qa.auditude.com/adserver/c/z=50183; 
                  l=1355280906; 
                  u=956c3cd141086a1da44dcae8ea4ed14a; 
                  uid=_CxLm0b1SeKD8KXco__5TQ; 
                  cid=127860991; 
                  s=ef8c51dc; 
                  t=1355309735; 
                  br=1; 
                  sq=1; 
                  pod=id%3a1%2cctype%3al%2cptype%3ap%2cdur 
                    %3a400%2clot%3a8%2ccpos%3a1%2cedur%3a400%2celot%3a8; 
                  ax=0%2c0%2c1720%2c0; 
                  w=100000; 
                  a=903395; 
                  a1=103/c300x250.jpeg 
              </StaticResource> 
              <CompanionClickThrough> 
                https://ad.qa.auditude.com/adserver/l/a=903395%3Ba1=103 
                  %3Ba2=1%3Bz=50183%3Bl=1355280906%3Bu=956c3cd141086a1da44dcae8ea4ed14a 
                  %3Bcid=127860991%3Bs=ef8c51dc%3Buid=_CxLm0b1SeKD8KXco__5TQ 
                  %3Bt=1355309735%3Bbr=1%3Bsq=1%3Bpod=id%3a1%2cctype%3al%2cptype 
                  %3ap%2cdur%3a400%2clot%3a8%2ccpos%3a1%2cedur%3a400%2celot%3a8 
                  %3Bax=0%2c0%2c1720%2c0 
              </CompanionClickThrough> 
              <AdParameters>campaign_id=7012</AdParameters> 
            </Companion> 
          </CompanionAds> 
        </Creative> 
        ... 
      </Creatives> 
      <Extensions> 
        <Extension type="Behavior"> 
          ... 
        </Extension> 
      </Extensions> 
    </InLine> 
  </Ad> 
  </VAST> 
</AdTrackingFragment> 
</AdTrackingFragments> 
```
