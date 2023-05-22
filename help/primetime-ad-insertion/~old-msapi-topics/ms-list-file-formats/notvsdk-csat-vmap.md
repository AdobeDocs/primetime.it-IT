---
description: Se il client richiede informazioni di tracciamento, il server manifest invia nuovamente un file formattato. Il formato e il contenuto dipendono dal valore del parametro di query pttrackingversion
title: Formato VMAP per il tracciamento degli URL
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---


# Formato VMAP per il tracciamento degli URL {#vmap-format-for-tracking-urls}

Se il client richiede informazioni di tracciamento, il server manifest invia nuovamente un file formattato. Il formato e il contenuto dipendono dal valore del parametro di query `pttrackingversion`

## Formato VMAP singolo {#vmap}

Il file VMAP inviato dal server manifesto se `pttrackingversion=vmap` ha il formato del seguente esempio, che proviene da un tipico blocco VMAP. è stata accorciata per evitare inutili ripetizioni, in modo che la struttura sia più chiara. I puntini di sospensione (tre punti, separati da spazi) indicano informazioni omesse all’interno di alcuni URL e tra alcuni blocchi di codice. Gli URL non abbreviati vengono visualizzati su più righe, anche se vengono visualizzati su un&#39;unica riga nel file VMAP.

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?> 
<vmap:VMAP version="1.0.1" xmlns:vmap="https://www.iab.net/videosuite/vmap"> 
<vmap:AdBreak timeOffset="00:00:00.000" breakType="linear" breakId="0"> 
<vmap:AdSource><vmap:VASTAdData><VAST version="3.0"> 
<Ad id="334690" sequence="1"><InLine> 
<AdSystem>Auditude</AdSystem><AdTitle>lee_pre_266647</AdTitle> 
<Impression>https://ad.auditude.com/adserver/e? 
    type=adimp&a=334690&w=200&uid=hm7f2YHSQxiOqp1dNVqevw& 
    u=cecebae72a919de350b9ac52602623f3& 
    t=1476120645&s=d4b8307&z=266647&cid=1270337971&br=1& 
    pod=id:1,ctype:l,ptype:p,dur:150,lot:5,cpos:1&sq=1&ax=0,0,0,0 
</Impression> 
<Creatives> 
  <Creative AdID="334690"><Linear><Duration>00:00:15.139</Duration> 
    <TrackingEvents> 
      <Tracking event="creativeView">https://ad.auditude.com/adserver/i/; 
                       uid=hm7f2YHSQxiOqp1dNVqevw;u=cecebae72a919de350b9ac52602623f3; 
                       t=1476120645;s=d4b8307;z=266647;cid=1270337971;br=1; 
                       pod=id:1,ctype:l,ptype:p,dur:150,lot:5,cpos:1;sq=1;ax=0,0,0,0; 
                       a1=105;a=334690;w=200/c340x192.m3u8 
      </Tracking> 
      <Tracking event="start">https://ad.auditude.com/adserver/e?type=AD_PROGRESS& 
                       a=334690&a1=105&ref=urn:asset:334690:105&unit=percent& 
                       progress=0&uid=hm7f2YHSQxiOqp1dNVqevw& 
                       u=cecebae72a919de350b9ac52602623f3& 
                       t=1476120645&s=d4b8307&z=266647&cid=1270337971&br=1& 
                       pod=id:1,ctype:l,ptype:p,dur:150,lot:5,cpos:1&sq=1&ax=0,0,0,0 
      </Tracking> 
      <Tracking event="start">https://dpm.demdex.net/ibs:dpid=22619& 
                       dpuuid=hm7f2YHSQxiOqp1dNVqevw 
      </Tracking> 
      <Tracking event="firstQuartile">https://ad.auditude.com/adserver/e? 
                       type=AD_PROGRESS&a=334690&a1=105&ref=urn:asset:334690:105& 
                       unit=percent&progress=25& 
                       uid=hm7f2YHSQxiOqp1dNVqevw&u=cecebae72a919de350b9ac52602623f3& 
                       t=1476120645&s=d4b8307&z=266647&cid=1270337971&br=1& 
                       pod=id:1,ctype:l,ptype:p,dur:150,lot:5,cpos:1&sq=1&ax=0,0,0,0 
      </Tracking> 
      <Tracking event="midpoint">https://ad.auditude.com/adserver/e? 
                       type=AD_PROGRESS&a=334690&a1=105&ref=urn:asset:334690:105& 
                       unit=percent&progress=50& 
                       uid=hm7f2YHSQxiOqp1dNVqevw&u=cecebae72a919de350b9ac52602623f3& 
                       t=1476120645&s=d4b8307&z=266647&cid=1270337971&br=1& 
                       pod=id:1,ctype:l,ptype:p,dur:150,lot:5,cpos:1&sq=1&ax=0,0,0,0 
      </Tracking> 
      <Tracking event="thirdQuartile">https://ad.auditude.com/adserver/e? 
                       type=AD_PROGRESS&a=334690&a1=105&ref=urn:asset:334690:105& 
                       unit=percent&progress=75& 
                       uid=hm7f2YHSQxiOqp1dNVqevw&u=cecebae72a919de350b9ac52602623f3& 
                       t=1476120645&s=d4b8307&z=266647&cid=1270337971&br=1& 
                       pod=id:1,ctype:l,ptype:p,dur:150,lot:5,cpos:1&sq=1&ax=0,0,0,0 
      </Tracking> 
      <Tracking event="complete">https://ad.auditude.com/adserver/e? 
                       type=AD_PROGRESS&a=334690&a1=105&ref=urn:asset:334690:105& 
                       unit=percent&progress=100& 
                       uid=hm7f2YHSQxiOqp1dNVqevw&u=cecebae72a919de350b9ac52602623f3& 
                       t=1476120645&s=d4b8307&z=266647&cid=1270337971&br=1& 
                       pod=id:1,ctype:l,ptype:p,dur:150,lot:5,cpos:1&sq=1&ax=0,0,0,0 
      </Tracking> 
    </TrackingEvents> 
    <MediaFiles> 
      <MediaFile id="Auditude" delivery="streaming" type="application/x-mpegURL"  
                 width="0" height="0"> 
                 https://olyhdliveextra-vh.akamaihd.net/. . ..mp4.csmil/master.m3u8 
      </MediaFile> 
    </MediaFiles> 
  </Linear></Creative> 
</Creatives> 
</InLine></Ad></VAST></vmap:VASTAdData></vmap:AdSource> 
<vmap:TrackingEvents> 
  <vmap:Tracking event="breakStart">https://ad.auditude.com/adserver/e? 
                        type=podprogress&event=start&uid=hm7f2YHSQxiOqp1dNVqevw& 
                        u=cecebae72a919de350b9ac52602623f3&t=1476120645& 
                        s=d4b8307&z=266647&cid=1270337971&br=1& 
                        pod=id:1,ctype:l,ptype:p,dur:150,lot:5,cpos:1 
  </vmap:Tracking> 
  <vmap:Tracking event="breakEnd">https://ad.auditude.com/adserver/e? 
                        type=podprogress&event=complete&uid=hm7f2YHSQxiOqp1dNVqevw& 
                        u=cecebae72a919de350b9ac52602623f3&t=1476120645& 
                        s=d4b8307&z=266647&cid=1270337971&br=1& 
                        pod=id:1,ctype:l,ptype:p,dur:150,lot:5,cpos:1 
  </vmap:Tracking> 
</vmap:TrackingEvents<vmap:Extensions/></vmap:AdBreak> 
<vmap:AdBreak timeOffset="00:06:15.139" breakType="linear" breakId="2"> 
<vmap:AdSource><vmap:VASTAdData><VAST version="3.0"><Ad id="334759" sequence="1"> 
<InLine><AdSystem>Auditude</AdSystem><AdTitle>lee_mid2_266652</AdTitle> 
<Impression>https://ad.auditude.com/adserver/e?type=adimp&a=334759&w=200& 
    uid=hm7f2YHSQxiOqp1dNVqevw&u=cecebae72a919de350b9ac52602623f3&t=1476120645& 
    s=d4b8307&z=266647&cid=1270337971&br=3& 
    pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=1&ax=0,0,0,0 
</Impression> 
<Creatives> 
  <Creative AdID="334759"><Linear><Duration>00:00:15.000</Duration> 
    <TrackingEvents> 
      <Tracking event="creativeView">https://ad.auditude.com/adserver/i/; 
                       uid=hm7f2YHSQxiOqp1dNVqevw;u=cecebae72a919de350b9ac52602623f3; 
                       t=1476120645;s=d4b8307;z=266647;cid=1270337971;br=3; 
                       pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2; 
                       sq=1;ax=0,0,0,0;a1=105; 
                       a=334759;w=200/c320x240.m3u8 
      </Tracking> 
      <Tracking event="start">https://ad.auditude.com/adserver/e? 
                       type=AD_PROGRESS&a=334759&a1=105&ref=urn:asset:334759:105& 
                       unit=percent&progress=0&uid=hm7f2YHSQxiOqp1dNVqevw& 
                       u=cecebae72a919de350b9ac52602623f3& 
                       t=1476120645&s=d4b8307&z=266647&cid=1270337971&br=3& 
                       pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=1&ax=0,0,0,0 
      </Tracking> 
      <Tracking event="start">https://dpm.demdex.net/ibs:dpid=22619& 
                       dpuuid=hm7f2YHSQxiOqp1dNVqevw 
      </Tracking> 
      <Tracking event="firstQuartile">https://ad.auditude.com/adserver/e? 
                       type=AD_PROGRESS&a=334759&a1=105&ref=urn:asset:334759:105& 
                       unit=percent&progress=25&uid=hm7f2YHSQxiOqp1dNVqevw& 
                       u=cecebae72a919de350b9ac52602623f3&t=1476120645&s=d4b8307& 
                       z=266647&cid=1270337971&br=3& 
                       pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=1&ax=0,0,0,0 
      </Tracking> 
      <Tracking event="midpoint">https://ad.auditude.com/adserver/e? 
                       type=AD_PROGRESS&a=334759&a1=105&ref=urn:asset:334759:105& 
                       unit=percent&progress=50& 
                       uid=hm7f2YHSQxiOqp1dNVqevw&u=cecebae72a919de350b9ac52602623f3& 
                       t=1476120645&s=d4b8307&z=266647&cid=1270337971&br=3& 
                       pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=1&ax=0,0,0,0 
      </Tracking> 
      <Tracking event="thirdQuartile">https://ad.auditude.com/adserver/e? 
                       type=AD_PROGRESS&a=334759&a1=105&ref=urn:asset:334759:105& 
                       unit=percent&progress=75& 
                       uid=hm7f2YHSQxiOqp1dNVqevw&u=cecebae72a919de350b9ac52602623f3& 
                       t=1476120645&s=d4b8307&z=266647&cid=1270337971&br=3& 
                       pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=1&ax=0,0,0,0 
      </Tracking> 
      <Tracking event="complete">https://ad.auditude.com/adserver/e? 
                       type=AD_PROGRESS&a=334759&a1=105&ref=urn:asset:334759:105& 
                       unit=percent&progress=100& 
                       uid=hm7f2YHSQxiOqp1dNVqevw&u=cecebae72a919de350b9ac52602623f3& 
                       t=1476120645&s=d4b8307&z=266647&cid=1270337971&br=3& 
                       pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=1&ax=0,0,0,0 
      </Tracking> 
    </TrackingEvents> 
    <MediaFiles> 
      <MediaFile id="Auditude" delivery="streaming" type="application/x-mpegURL"  
                 width="0" height="0"> 
                 https://cdn2.auditude.com/assets/. . ..m3u8 
      </MediaFile> 
    </MediaFiles> 
  </Linear></Creative> 
</Creatives> 
</InLine></Ad> 
<Ad id="334691" sequence="2"><InLine> 
<AdSystem>Auditude</AdSystem><AdTitle>lee_mid1_266647</AdTitle> 
<Impression>https://ad.auditude.com/adserver/e?type=adimp&a=334691&w=200& 
    uid=hm7f2YHSQxiOqp1dNVqevw&u=cecebae72a919de350b9ac52602623f3&t=1476120645& 
    s=d4b8307&z=266647&cid=1270337971&br=3& 
    pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=2&ax=0,0,0,0 
</Impression> 
<Creatives> 
  <Creative AdID="334691"><Linear><Duration>00:00:15.023</Duration> 
    <TrackingEvents> 
      <Tracking event="creativeView">https://ad.auditude.com/adserver/i/; 
                       uid=hm7f2YHSQxiOqp1dNVqevw;u=cecebae72a919de350b9ac52602623f3; 
                       t=1476120645;s=d4b8307;z=266647;cid=1270337971;br=3; 
                       pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2;sq=2;ax=0,0,0,0; 
                       a1=105;a=334691;w=200/c384x216.m3u8 
      </Tracking> 
      <Tracking event="start">https://ad.auditude.com/adserver/e? 
                       type=AD_PROGRESS&a=334691&a1=105&ref=urn:asset:334691:105& 
                       unit=percent&progress=0& 
                       uid=hm7f2YHSQxiOqp1dNVqevw&u=cecebae72a919de350b9ac52602623f3& 
                       t=1476120645&s=d4b8307&z=266647&cid=1270337971&br=3& 
                       pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=2&ax=0,0,0,0 
      </Tracking> 
      <Tracking event="start">https://dpm.demdex.net/ibs:dpid=22619& 
                       dpuuid=hm7f2YHSQxiOqp1dNVqevw 
      </Tracking> 
      <Tracking event="firstQuartile">https://ad.auditude.com/adserver/e? 
                       type=AD_PROGRESS&a=334691&a1=105&ref=urn:asset:334691:105& 
                       unit=percent&progress=25& 
                       uid=hm7f2YHSQxiOqp1dNVqevw&u=cecebae72a919de350b9ac52602623f3& 
                       t=1476120645&s=d4b8307&z=266647&cid=1270337971&br=3& 
                       pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=2&ax=0,0,0,0 
      </Tracking> 
      <Tracking event="midpoint">https://ad.auditude.com/adserver/e? 
                       type=AD_PROGRESS&a=334691&a1=105&ref=urn:asset:334691:105& 
                       unit=percent&progress=50& 
                       uid=hm7f2YHSQxiOqp1dNVqevw&u=cecebae72a919de350b9ac52602623f3& 
                       t=1476120645&s=d4b8307&z=266647&cid=1270337971&br=3& 
                       pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=2&ax=0,0,0,0 
      </Tracking> 
      <Tracking event="thirdQuartile">https://ad.auditude.com/adserver/e? 
                       type=AD_PROGRESS&a=334691&a1=105&ref=urn:asset:334691:105& 
                       unit=percent&progress=75& 
                       uid=hm7f2YHSQxiOqp1dNVqevw&u=cecebae72a919de350b9ac52602623f3& 
                       t=1476120645&s=d4b8307&z=266647&cid=1270337971&br=3& 
                       pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=2&ax=0,0,0,0 
      </Tracking> 
      <Tracking event="complete">https://ad.auditude.com/adserver/e? 
                       type=AD_PROGRESS&a=334691&a1=105&ref=urn:asset:334691:105& 
                       unit=percent&progress=100& 
                       uid=hm7f2YHSQxiOqp1dNVqevw&u=cecebae72a919de350b9ac52602623f3& 
                       t=1476120645&s=d4b8307&z=266647&cid=1270337971&br=3& 
                       pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=2&ax=0,0,0,0 
      </Tracking> 
    </TrackingEvents> 
    <MediaFiles> 
      <MediaFile id="Auditude" delivery="streaming" type="application/x-mpegURL"  
                 width="0" height="0"> 
                 https://olyhdliveextra-vh.akamaihd.net/. . ..mp4.csmil/master.m3u8 
      </MediaFile> 
    </MediaFiles> 
  </Linear></Creative> 
</Creatives> 
</InLine></Ad> 
<Ad id="334693" sequence="3"><InLine> 
<AdSystem>Auditude</AdSystem><AdTitle>lee_mid3_266647</AdTitle> 
<Impression>https://ad.auditude.com/adserver/e?type=adimp&a=334693&w=200& 
    uid=hm7f2YHSQxiOqp1dNVqevw&u=cecebae72a919de350b9ac52602623f3&t=1476120645& 
    s=d4b8307&z=266647&cid=1270337971&br=3& 
    pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=3&ax=0,0,0,0 
</Impression> 
<Creatives> 
  <Creative AdID="334693"><Linear><Duration>00:00:30.000</Duration> 
    <TrackingEvents> 
      <Tracking event="creativeView">https://ad.auditude.com/adserver/i/; 
                       uid=hm7f2YHSQxiOqp1dNVqevw;u=cecebae72a919de350b9ac52602623f3; 
                       t=1476120645;s=d4b8307;z=266647;cid=1270337971;br=3; 
                       pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2;sq=3; 
                       ax=0,0,0,0;a1=105;a=334693;w=200/c384x216.m3u8 
      </Tracking> 
      <Tracking event="start">https://ad.auditude.com/adserver/e? 
                       type=AD_PROGRESS&a=334693&a1=105&ref=urn:asset:334693:105& 
                       unit=percent&progress=0& 
                       uid=hm7f2YHSQxiOqp1dNVqevw&u=cecebae72a919de350b9ac52602623f3& 
                       t=1476120645&s=d4b8307&z=266647&cid=1270337971&br=3& 
                       pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=3&ax=0,0,0,0 
      </Tracking> 
      <Tracking event="start">https://dpm.demdex.net/ibs:dpid=22619& 
                       dpuuid=hm7f2YHSQxiOqp1dNVqevw 
      </Tracking> 
      <Tracking event="firstQuartile">https://ad.auditude.com/adserver/e? 
                       type=AD_PROGRESS&a=334693&a1=105&ref=urn:asset:334693:105& 
                       unit=percent&progress=25& 
                       uid=hm7f2YHSQxiOqp1dNVqevw&u=cecebae72a919de350b9ac52602623f3& 
                       t=1476120645&s=d4b8307&z=266647&cid=1270337971&br=3& 
                       pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=3&ax=0,0,0,0 
      </Tracking> 
      <Tracking event="midpoint">https://ad.auditude.com/adserver/e? 
                       type=AD_PROGRESS&a=334693&a1=105&ref=urn:asset:334693:105& 
                       unit=percent&progress=50& 
                       uid=hm7f2YHSQxiOqp1dNVqevw&u=cecebae72a919de350b9ac52602623f3& 
                       t=1476120645&s=d4b8307&z=266647&cid=1270337971&br=3& 
                       pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=3&ax=0,0,0,0 
      </Tracking> 
      <Tracking event="thirdQuartile">https://ad.auditude.com/adserver/e? 
                       type=AD_PROGRESS&a=334693&a1=105&ref=urn:asset:334693:105& 
                       unit=percent&progress=75& 
                       uid=hm7f2YHSQxiOqp1dNVqevw&u=cecebae72a919de350b9ac52602623f3& 
                       t=1476120645&s=d4b8307&z=266647&cid=1270337971&br=3& 
                       pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=3&ax=0,0,0,0 
      </Tracking> 
      <Tracking event="complete">https://ad.auditude.com/adserver/e? 
                       type=AD_PROGRESS&a=334693&a1=105&ref=urn:asset:334693:105& 
                       unit=percent&progress=100& 
                       uid=hm7f2YHSQxiOqp1dNVqevw&u=cecebae72a919de350b9ac52602623f3& 
                       t=1476120645&s=d4b8307&z=266647&cid=1270337971&br=3& 
                       pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=3&ax=0,0,0,0 
      </Tracking> 
    </TrackingEvents> 
    <MediaFiles> 
      <MediaFile id="Auditude" delivery="streaming" type="application/x-mpegURL"  
                 width="0" height="0"> 
                 https://olyhdliveextra-vh.akamaihd.net/. . ..mp4.csmil/master.m3u8 
      </MediaFile> 
    </MediaFiles> 
  </Linear></Creative> 
</Creatives> 
</InLine></Ad> 
<Ad id="334705" sequence="4"> 
<InLine> 
<AdSystem>Auditude</AdSystem> 
<AdTitle>lee_mid1_266652</AdTitle> 
<Impression>https://ad.auditude.com/adserver/e?type=adimp&a=334705&w=200& 
    uid=hm7f2YHSQxiOqp1dNVqevw&u=cecebae72a919de350b9ac52602623f3&t=1476120645& 
    s=d4b8307&z=266647&cid=1270337971&br=3& 
    pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=4&ax=0,0,0,0 
</Impression> 
<Creatives> 
  <Creative AdID="334705"><Linear><Duration>00:00:30.069</Duration> 
    <TrackingEvents> 
      <Tracking event="creativeView">https://ad.auditude.com/adserver/i/; 
                       uid=hm7f2YHSQxiOqp1dNVqevw;u=cecebae72a919de350b9ac52602623f3; 
                       t=1476120645;s=d4b8307;z=266647;cid=1270337971;br=3; 
                       pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2;sq=4; 
                       ax=0,0,0,0;a1=105;a=334705;w=200/c340x192.m3u8 
      </Tracking> 
      <Tracking event="start">https://ad.auditude.com/adserver/e? 
                       type=AD_PROGRESS&a=334705&a1=105&ref=urn:asset:334705:105& 
                       unit=percent&progress=0& 
                       uid=hm7f2YHSQxiOqp1dNVqevw&u=cecebae72a919de350b9ac52602623f3& 
                       t=1476120645&s=d4b8307&z=266647&cid=1270337971&br=3& 
                       pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=4&ax=0,0,0,0 
      </Tracking> 
      <Tracking event="start">https://dpm.demdex.net/ibs:dpid=22619& 
                       dpuuid=hm7f2YHSQxiOqp1dNVqevw 
      </Tracking> 
      <Tracking event="firstQuartile">https://ad.auditude.com/adserver/e? 
                       type=AD_PROGRESS&a=334705&a1=105&ref=urn:asset:334705:105& 
                       unit=percent&progress=25& 
                       uid=hm7f2YHSQxiOqp1dNVqevw&u=cecebae72a919de350b9ac52602623f3& 
                       t=1476120645&s=d4b8307&z=266647&cid=1270337971&br=3& 
                       pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=4&ax=0,0,0,0 
      </Tracking> 
      <Tracking event="midpoint">https://ad.auditude.com/adserver/e? 
                       type=AD_PROGRESS&a=334705&a1=105&ref=urn:asset:334705:105& 
                       unit=percent&progress=50& 
                       uid=hm7f2YHSQxiOqp1dNVqevw&u=cecebae72a919de350b9ac52602623f3& 
                       t=1476120645&s=d4b8307&z=266647&cid=1270337971&br=3& 
                       pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=4&ax=0,0,0,0 
      </Tracking> 
      <Tracking event="thirdQuartile">https://ad.auditude.com/adserver/e? 
                       type=AD_PROGRESS&a=334705&a1=105&ref=urn:asset:334705:105& 
                       unit=percent&progress=75& 
                       uid=hm7f2YHSQxiOqp1dNVqevw&u=cecebae72a919de350b9ac52602623f3& 
                       t=1476120645&s=d4b8307&z=266647&cid=1270337971&br=3& 
                       pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=4&ax=0,0,0,0 
      </Tracking> 
      <Tracking event="complete">https://ad.auditude.com/adserver/e? 
                       type=AD_PROGRESS&a=334705&a1=105&ref=urn:asset:334705:105& 
                       unit=percent&progress=100& 
                       uid=hm7f2YHSQxiOqp1dNVqevw&u=cecebae72a919de350b9ac52602623f3& 
                       t=1476120645&s=d4b8307&z=266647&cid=1270337971&br=3& 
                       pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2&sq=4&ax=0,0,0,0 
      </Tracking> 
    </TrackingEvents> 
    <MediaFiles> 
      <MediaFile id="Auditude" delivery="streaming" type="application/x-mpegURL"  
                 width="0" height="0"> 
                 https://olyhdliveextra-vh.akamaihd.net/. . ..mp4.csmil/master.m3u8 
      </MediaFile> 
    </MediaFiles> 
  </Linear></Creative> 
</Creatives> 
</InLine> 
</Ad> 
</VAST></vmap:VASTAdData></vmap:AdSource> 
<vmap:TrackingEvents> 
  <vmap:Tracking event="breakStart">https://ad.auditude.com/adserver/e? 
                        type=podprogress&event=start&uid=hm7f2YHSQxiOqp1dNVqevw& 
                        u=cecebae72a919de350b9ac52602623f3&t=1476120645&s=d4b8307& 
                        z=266647&cid=1270337971&br=3& 
                        pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2 
  </vmap:Tracking> 
  <vmap:Tracking event="breakEnd">https://ad.auditude.com/adserver/e? 
                        type=podprogress&event=complete&uid=hm7f2YHSQxiOqp1dNVqevw& 
                        u=cecebae72a919de350b9ac52602623f3&t=1476120645&s=d4b8307& 
                        z=266647&cid=1270337971&br=3& 
                        pod=id:3,ctype:l,ptype:m,dur:150,lot:5,cpos:2 
  </vmap:Tracking> 
</vmap:TrackingEvents> 
<vmap:Extensions/> 
</vmap:AdBreak></vmap:VMAP>
```
