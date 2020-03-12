---
description: Per consentire ai clienti che desiderano pagare solo ciò che utilizzano, anziché un tasso fisso indipendentemente dall'uso effettivo, Adobe raccoglie le metriche di utilizzo e utilizza queste metriche per determinare quanto addebitare ai clienti.
seo-description: Per consentire ai clienti che desiderano pagare solo ciò che utilizzano, anziché un tasso fisso indipendentemente dall'uso effettivo, Adobe raccoglie le metriche di utilizzo e utilizza queste metriche per determinare quanto addebitare ai clienti.
seo-title: Metriche di fatturazione
title: Metriche di fatturazione
uuid: 658ffbcd-dedc-464c-8ec7-aa3bdfcb1512
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Metriche di fatturazione {#billing-metrics}

Per consentire ai clienti che desiderano pagare solo ciò che utilizzano, anziché un tasso fisso indipendentemente dall&#39;uso effettivo, Adobe raccoglie le metriche di utilizzo e utilizza queste metriche per determinare quanto addebitare ai clienti.

Ogni volta che il lettore genera un evento di avvio del flusso, TVSDK inizia a inviare periodicamente messaggi HTTP al sistema di fatturazione di Adobe. Il periodo, noto come durata fatturabile, può essere diverso per VOD standard, pro VOD (annunci mid-roll abilitati) e contenuti live. La durata predefinita di ciascun tipo di contenuto è di 30 minuti, ma il contratto con Adobe determina i valori effettivi.

I messaggi contengono le informazioni seguenti:

* Tipo di contenuto (live, lineare o VOD)
* URL contenuto
* Se gli annunci pubblicitari sono abilitati
* Se gli annunci mid-roll sono abilitati (solo VOD)
* Se il flusso è protetto da DRM
* La versione e la piattaforma TVSDK

Adobe preconfigura questa disposizione, ma se desideri modificarla, collabora con il tuo rappresentante Adobe Enablement.

Per monitorare le statistiche inviate da TVSDK ad Adobe, ottenere l’URL dal rappresentante Adobe Enablement e utilizzare uno strumento di acquisizione di rete, ad esempio Charles, per visualizzare i dati.

## Configurare le metriche di fatturazione {#configure-billing-metrics}

Se utilizzi la configurazione predefinita, non è necessario fare altro per abilitare o configurare la fatturazione. Se avete ottenuto diversi parametri di configurazione dal rappresentante Adobe Enablement, utilizzate la classe PTBillingMetricsConfiguration per impostare questi parametri prima di inizializzare il lettore multimediale.

La maggior parte dei clienti deve utilizzare la configurazione predefinita.

>[!IMPORTANT]
>
>La configurazione impostata rimane attiva per tutta la durata del lettore multimediale. Una volta inizializzato il lettore multimediale, non è possibile modificare la configurazione.

Per configurare le metriche di fatturazione:

1. Inserire il seguente esempio di codice.

   ```
   PTBillingMetricsConfiguration *billingConfig = [[[PTBillingMetricsConfiguration alloc] init] autorelease]; 
   billingConfig.enabled = YES; 
   billingConfig.stdVODBillableDurationMinutes = 60.0; 
   billingConfig.proVODBillableDurationMinutes = 30.0; 
   billingConfig.liveBillableDurationMinutes = 15.0; 
   
   // metadata is the PTMetadata instance set on PTMediaPlayerItem 
   [metadata setMetadata:billingConfig forKey:PTBillingMetricsConfigurationMetadataKey];
   ```

## Trasmissione delle metriche di fatturazione {#transmit-billing-metrics}

TVSDK invia le metriche di fatturazione ad Adobe in un formato XML.

<!--<a id="example_13ABDB1CC0B549968A534765378DA3A0"></a>-->

Se utilizzi uno strumento di acquisizione di rete per monitorare le statistiche trasmesse da TVSDK ad Adobe, dovresti vedere le unità come segue:

```
<request> 
     <sc_xml_ver>1.0</sc_xml_ver> 
     <reportSuiteID>ptebilling</reportSuiteID> 
     <visitorID>5536C629-5EF7-4F02-8E5D-9FA136CB3CED</visitorID> 
     <pageName>com.adobe.primetime.psdksample</pageName> 
     <timestamp>2016-11-22T18:06:30+0000</timestamp> 
     <userAgent>Mozilla/5.0 (iPad; CPU OS 9_1 like Mac OS X) AppleWebKit/601.1.46 (KHTML, like Gecko) Mobile/13B143</userAgent> 
     <contextData> 
         <billingMetrics> 
                 <contentDuration>1799111</contentDuration> 
                 <contentURL>https%3A%2F%2Fdevimages.apple.com.edgekey.net%2Fstreaming%2Fexamples%2Fbipbop_16x9%2Fbipbop_16x9_variant.m3u8</contentURL> 
                 <contentType>vod</contentType> 
                 <midrollEnabled>true</midrollEnabled> 
                 <tvsdkVersion>1.0.211</tvsdkVersion> 
                 <platform>Mozilla/5.0 (iPad; CPU OS 9_1 like Mac OS X) AppleWebKit/601.1.46 (KHTML, like Gecko) Mobile/13B143</platform> 
                 <publisherID>com.adobe.primetime.psdksample</publisherID> 
                 <adsEnabled>true</adsEnabled> 
                 <type>start</type> 
         </billingMetrics> 
     </contextData> 
</request>
```

Le proprietà booleane `drmProtected`, `adsEnabled`, e `midrollEnabled` vengono visualizzate solo se sono vere.