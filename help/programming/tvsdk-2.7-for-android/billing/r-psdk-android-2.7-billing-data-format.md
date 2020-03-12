---
description: TVSDK invia le metriche di fatturazione ad Adobe in un formato XML.
seo-description: TVSDK invia le metriche di fatturazione ad Adobe in un formato XML.
seo-title: Trasmissione delle metriche di fatturazione
title: Trasmissione delle metriche di fatturazione
uuid: f4a7f50e-f457-434e-bf26-1e06cb15a038
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Trasmissione delle metriche di fatturazione {#transmit-billing-metrics}

TVSDK invia le metriche di fatturazione ad Adobe in un formato XML.

<!--<a id="example_13ABDB1CC0B549968A534765378DA3A0"></a>-->

Se utilizzi uno strumento di acquisizione di rete per monitorare le statistiche trasmesse da TVSDK ad Adobe, dovresti vedere le unità come segue:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<request>
    <sc_xml_ver>1.0</sc_xml_ver>
    <reportSuiteID>primesample2</reportSuiteID>
    <visitorID>947310128cb56f41</visitorID>
    <pageURL>https://. . ..m3u8</pageURL>
    <timestamp>2016-4-7T10:1:4</timestamp>
    <contextData>
        <billingMetrics>
            <publisherID>com.adobe.primetime.reference.PrimetimeReference</publisherID>
            <contentType>vod</contentType>
            <adsEnabled>true</adsEnabled>
            <midrollEnabled>true</midrollEnabled>
            <platform>Mac OSX 10.11.5</platform>
            <tvsdkVersion>2,4,0,1559</tvsdkVersion>
            <contentURL>https://. . ..m3u8</contentURL>
        </billingMetrics>
    </contextData>
</request>
```

Le proprietà booleane `drmProtected`, `adsEnabled`, e `midrollEnabled` vengono visualizzate solo se sono vere.