---
description: Il server manifest restituisce le playlist master in formato M3U8, in conformità allo standard HTTP Live Streaming proposto. È costituito da una serie di flussi di trasporto varianti (TS), ciascuno contenente rappresentazioni dello stesso contenuto per diversi bit rate e formati. L'inserimento di annunci Adobe Primetime aggiunge il tag di direttiva EXT-X-MARKER, che deve essere interpretato dai lettori video client.
title: Direttiva EXT-X MARKER
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%

---


# Direttiva EXT-X-MARKER {#ext-x-marker-directive}

Il server manifest restituisce le playlist master in formato M3U8, in conformità allo standard HTTP Live Streaming proposto. È costituito da una serie di flussi di trasporto varianti (TS), ciascuno contenente rappresentazioni dello stesso contenuto per diversi bit rate e formati. L&#39;inserimento di annunci Adobe Primetime aggiunge il tag di direttiva EXT-X-MARKER, che deve essere interpretato dai lettori video client.

Per informazioni dettagliate sul tag EXT-X-MARKER, consulta [Profilo Adobe Primetime HTTP Live Streaming](https://wwwimages2.adobe.com/content/dam/acom/en/devnet/primetime/PrimetimeHLS_April2014.pdf).

>[!NOTE]
>
>Questa funzionalità è disponibile solo se l&#39;URL del server manifesto di bootstrap non contiene il parametro `pttrackingmode` .

>[!NOTE]
>
>Il tag EXT-X-MARKER viene aggiunto ai segmenti di annunci e non ai segmenti di contenuto.

Il progetto di standard su [HTTP Live Streaming](https://tools.ietf.org/html/draft-pantos-http-live-streaming-23) descrive il contenuto e il formato delle playlist varianti. Il tag EXT-X-MARKER indirizza il client a richiamare un callback. Contiene i seguenti componenti:

* **** Identificatore IDUnique (stringa) per questo evento di callback nel contesto del flusso di programma.

* **** TYPETType (stringa) dell&#39;evento di callback: PodBegin, PodEnd, PrerollPodBegin, PrerollPodEnd o AdBegin

* **** Durata del tempo (in secondi) dall’inizio del segmento che contiene il tag per il quale la direttiva rimane valida.

* **** OFFSETOfacoltativo. L’offset (in secondi) relativo all’inizio della riproduzione del segmento, quando deve essere invocato il callback.

   * `PodBegin` e  `PrerollPodBegin` contengono informazioni sul beacon nell&#39;attributo DATA e vengono attivate all&#39;inizio del segmento. Pertanto, il tag `OFFSET` non è disponibile qui.

   * `AdBegin` contiene informazioni sul beacon nell’attributo DATA e i tag impression vengono attivati all’inizio del segmento. Pertanto anche il tag `OFFSET` non è disponibile qui.

   * `PodEnd` e  `PrerollPodEnd` contengono informazioni sul beacon nell’attributo DATA , ma vengono attivate alla fine del segmento corrente, perché si prevede che questi tag vengano attivati alla fine dell’ultimo segmento dell’ultimo annuncio nel pod. In questo caso, `OFFSET` è impostato su `<duration of segment>` per specificare che il beacon deve essere attivato alla fine del segmento corrente.

* **** Stringa con codifica DATABase64 racchiusa tra virgolette doppie contenente i dati da passare all&#39;applicazione quando si richiama il callback. Contiene informazioni di tracciamento degli annunci conformi alle specifiche VMAP1.0 e VAST3.0.

* **** COUNTNnumero di annunci che verranno uniti nell’interruzione pubblicitaria.

   Applicabile solo se il componente TYPE è impostato su PodBegin o PrerollPodBegin.

* **** BREAKDURTodifica totale (in secondi) dell’interruzione pubblicitaria riempita.

   Applicabile solo se il componente TYPE è impostato su PodBegin o PrerollPodBegin.

Durante la costruzione del callback, interpreta i componenti EXT-X-MARKER come segue:

* Quando il tag contiene `OFFSET`, attiva il callback in corrispondenza dell’offset specificato rispetto all’inizio della riproduzione del contenuto in quel segmento. In caso contrario, attiva il callback non appena inizia la riproduzione del contenuto in quel segmento.
* Utilizza `DURATION` per tenere traccia dell’avanzamento del contenuto dell’annuncio e per richiedere gli URL per il tracciamento degli eventi.
* Passa `ID`, `TYPE` e `DATA` al callback.

Utilizza i valori `PrerollPodBegin` e `PrerollPodEnd` per `TYPE` per decidere quale segmento TS riprodurre per primo nei flussi live/lineari.

>[!NOTE]
>
>I valori `PrerollPodBegin` e `PrerollPodEnd` sono disponibili solo quando un annuncio pre-roll viene inserito in un flusso live.

Il server manifesto include i tag EXT-X-MARKER nei seguenti segmenti:

* Il primo segmento nell’interruzione pubblicitaria, per tracciare l’inizio di un annuncio pod.
* Il primo segmento dell’annuncio, per tenere traccia dell’inizio/completamento/avanzamento di un singolo annuncio all’interno di un ad pod.
* L’ultimo segmento nell’interruzione pubblicitaria, per tracciare la fine di un annuncio pod.

Il server manifest invia un documento XML `VMAP1.0-conformant` per tenere traccia dell&#39;inizio e della fine di ogni interruzione pubblicitaria. Si tratta di una versione filtrata dell&#39;effettiva risposta VMAP1.0 restituita dal server di annunci e contiene principalmente gli eventi di tracciamento come mostrato qui:

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

Per ogni annuncio creativo il server manifest inserisce nel contenuto del programma, invia un documento XML conforme a VAST3.0 per tenere traccia di quell&#39;annuncio. Ogni documento XML contiene un elemento `<InLine>` che descrive l’annuncio lineare inserito o un elemento `<Wrapper>` nel caso di annunci wrapper (ovvero annunci collegati o reindirizzati) e di annunci ed estensioni associate. Se la risposta VAST contiene un attributo di sequenza, ad esempio quando l’annuncio fa parte di un ad pod, il documento include tale attributo. Di seguito è riportato un documento XML conforme a VAST3.0 di esempio per il tracciamento di un singolo annuncio:

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
