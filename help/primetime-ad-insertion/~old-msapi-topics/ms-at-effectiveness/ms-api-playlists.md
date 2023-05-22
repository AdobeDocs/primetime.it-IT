---
description: Il server manifest restituisce playlist master in formato M3U8, conformi allo standard HTTP Live Streaming proposto. È costituito da un set di flussi di trasporto varianti (TS), ciascuno contenente rappresentazioni dello stesso contenuto per bit rate e formati diversi. Adobe Primetime ad insertion aggiunge il tag di direttiva EXT-X-MARKER, che deve essere interpretato dai lettori video client.
title: Direttiva EXT-X-MARKER
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%

---


# Direttiva EXT-X-MARKER {#ext-x-marker-directive}

Il server manifest restituisce playlist master in formato M3U8, conformi allo standard HTTP Live Streaming proposto. È costituito da un set di flussi di trasporto varianti (TS), ciascuno contenente rappresentazioni dello stesso contenuto per bit rate e formati diversi. Adobe Primetime ad insertion aggiunge il tag di direttiva EXT-X-MARKER, che deve essere interpretato dai lettori video client.

Per informazioni dettagliate sul tag EXT-X-MARKER, consulta [Profilo streaming HTTP Adobe Primetime](https://wwwimages2.adobe.com/content/dam/acom/en/devnet/primetime/PrimetimeHLS_April2014.pdf).

>[!NOTE]
>
>Questa funzionalità è disponibile solo se l&#39;URL del server del manifesto di avvio non contiene `pttrackingmode` parametro.

>[!NOTE]
>
>Il tag EXT-X-MARKER viene aggiunto ai segmenti di annuncio e non ai segmenti di contenuto.

La bozza di standard in [HTTP Live Streaming](https://tools.ietf.org/html/draft-pantos-http-live-streaming-23) descrive il contenuto e il formato delle playlist varianti. Il tag EXT-X-MARKER indica al client di richiamare un callback. Contiene i seguenti componenti:

* **ID** Identificatore univoco (stringa) per questo evento di callback nel contesto del flusso del programma.

* **TIPO** Tipo (stringa) dell&#39;evento di callback: PodBegin, PodEnd, PrerollPodBegin, PrerollPodEnd o AdBegin

* **DURATA** Periodo di tempo (in secondi) dall’inizio del segmento su cui è apposto il tag per il quale la direttiva resta valida.

* **OFFSET** Facoltativo. Offset (in secondi) relativo all’inizio della riproduzione del segmento, quando deve essere richiamato il callback.

   * `PodBegin` e `PrerollPodBegin` contengono informazioni sul beacon nell’attributo DATA e vengono attivati all’inizio del segmento. Quindi il `OFFSET` non è disponibile qui.

   * `AdBegin` contiene le informazioni sul beacon nell’attributo DATA e i tag di impression vengono attivati all’inizio di quel segmento. Quindi il `OFFSET` Il tag non è disponibile neanche qui.

   * `PodEnd` e `PrerollPodEnd` contengono informazioni sul beacon nell’attributo DATA, ma vengono attivati alla fine del segmento corrente perché si prevede che questi tag vengano attivati alla fine dell’ultimo segmento dell’ultimo annuncio nel pod. In questo caso, `OFFSET` è impostato su `<duration of segment>` per specificare che il beacon deve essere attivato alla fine del segmento corrente.

* **DATI** Stringa con codifica Base64 racchiusa tra virgolette doppie contenenti i dati da passare all&#39;applicazione quando si richiama il callback. Contiene informazioni di tracciamento degli annunci conformi alle specifiche VMAP1.0 e VAST3.0.

* **COUNT** Numero di annunci che verranno uniti nell’interruzione pubblicitaria.

   Applicabile solo se il componente TYPE è impostato su PodBegin o PrerollPodBegin.

* **BREAKDUR** Durata totale (in secondi) dell’interruzione pubblicitaria riempita.

   Applicabile solo se il componente TYPE è impostato su PodBegin o PrerollPodBegin.

Durante la costruzione del callback, interpretare i componenti EXT-X-MARKER come segue:

* Quando il tag contiene `OFFSET`, attiva il callback all&#39;offset specificato rispetto all&#39;inizio della riproduzione del contenuto in quel segmento. In caso contrario, attiva il callback non appena inizia la riproduzione del contenuto in tale segmento.
* Utilizzare `DURATION` per tenere traccia dell’avanzamento del contenuto dell’annuncio e per richiedere URL per il tracciamento degli eventi.
* Superato `ID`, `TYPE`, e `DATA` al callback.

Utilizza il `PrerollPodBegin`, e `PrerollPodEnd` valori per `TYPE` per decidere quale segmento TS riprodurre per primo nei flussi live/lineari.

>[!NOTE]
>
>Il `PrerollPodBegin`, e `PrerollPodEnd` i valori sono disponibili solo quando un annuncio pre-roll viene inserito in un flusso live.

Il server manifest include i tag EXT-X-MARKER nei seguenti segmenti:

* Il primo segmento nell’interruzione pubblicitaria, per tracciare l’inizio di un pod dell’annuncio.
* Il primo segmento dell’annuncio, per monitorare l’inizio/completamento/avanzamento di un singolo annuncio all’interno di un pod dell’annuncio.
* L’ultimo segmento nell’interruzione pubblicitaria, per tracciare la fine di un pod dell’annuncio.

Il server manifesto invia un `VMAP1.0-conformant` Documento XML per tenere traccia dell’inizio e della fine di ogni interruzione pubblicitaria. Si tratta di una versione filtrata della risposta VMAP1.0 effettiva restituita dal server di annunci e contiene principalmente gli eventi di tracciamento come mostrato di seguito:

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

Per ogni annuncio creativo inserito dal server manifesto nel contenuto del programma, invia un documento XML conforme a VAST3.0 per tenere traccia dell’annuncio. Ogni documento XML contiene un `<InLine>` elemento che descrive l’annuncio lineare e creativo inserito, oppure `<Wrapper>` nel caso di annunci wrapper (vale a dire, annunci collegati o reindirizzati) e di eventuali annunci ed estensioni correlati associati. Se la risposta VAST contiene un attributo di sequenza, ad esempio quando l’annuncio fa parte di un pod dell’annuncio, il documento lo include. Di seguito è riportato un esempio di documento XML conforme a VAST3.0 per il tracciamento di un singolo annuncio:

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
