---
description: TVSDK invia le metriche di fatturazione all’Adobe in formato XML.
title: Trasmettere le metriche di fatturazione
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '58'
ht-degree: 0%

---

# Trasmettere le metriche di fatturazione {#transmit-billing-metrics}

TVSDK invia le metriche di fatturazione all’Adobe in formato XML.

<!--<a id="example_13ABDB1CC0B549968A534765378DA3A0"></a>-->

Se utilizzi uno strumento di acquisizione di rete per monitorare le statistiche trasmesse da TVSDK ad Adobe, dovresti visualizzare unità simili alle seguenti:

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
