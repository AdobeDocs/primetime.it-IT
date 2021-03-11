---
description: Per soddisfare i clienti che desiderano pagare solo ciò che utilizzano, anziché un tasso fisso indipendentemente dall’uso effettivo, Adobe raccoglie le metriche di utilizzo e utilizza queste metriche per determinare quanto fatturare ai clienti.
title: Metriche di fatturazione
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---


# Metriche di fatturazione {#billing-metrics}

Per soddisfare i clienti che desiderano pagare solo ciò che utilizzano, anziché un tasso fisso indipendentemente dall’uso effettivo, Adobe raccoglie le metriche di utilizzo e utilizza queste metriche per determinare quanto fatturare ai clienti.

Ogni volta che il lettore genera un evento di avvio del flusso, TVSDK inizia a inviare periodicamente messaggi HTTP al sistema di fatturazione di Adobe. Il periodo, noto come durata fatturabile, può essere diverso per VOD standard, pro VOD (annunci mid-roll abilitati) e contenuti live. La durata predefinita di ciascun tipo di contenuto è di 30 minuti, ma il contratto con Adobe determina i valori effettivi.

I messaggi contengono le seguenti informazioni:

* Tipo di contenuto (live, lineare o VOD)
* URL contenuto
* Se gli annunci sono abilitati
* Se gli annunci mid-roll sono abilitati (solo VOD)
* Se il flusso è protetto da DRM
* Versione e piattaforma TVSDK

L&#39;Adobe preconfigura questa disposizione, ma se desideri modificarla, rivolgiti al tuo rappresentante di abilitazione Adobe.

Per monitorare le statistiche inviate ad Adobe da TVSDK, ottieni l’URL dal tuo rappresentante di abilitazione Adobe e utilizza uno strumento di acquisizione della rete, ad esempio Charles, per vedere i dati.

## Configurare le metriche di fatturazione {#configure-billing-metrics}

Se utilizzi la configurazione predefinita, non è necessario eseguire altre operazioni per abilitare o configurare la fatturazione. Se hai ottenuto diversi parametri di configurazione dal tuo rappresentante di abilitazione Adobe, utilizza la classe PTBillingMetricsConfiguration per impostare questi parametri prima di inizializzare il lettore multimediale.

La maggior parte dei clienti deve utilizzare la configurazione predefinita.

>[!IMPORTANT]
>
>La configurazione impostata rimane attiva per tutta la durata del lettore multimediale. Una volta inizializzato il lettore multimediale, non è possibile modificare la configurazione.

Per configurare le metriche di fatturazione:

1. Immetti il seguente codice di esempio.

   ```
   PTBillingMetricsConfiguration *billingConfig = [[[PTBillingMetricsConfiguration alloc] init] autorelease]; 
   billingConfig.enabled = YES; 
   billingConfig.stdVODBillableDurationMinutes = 60.0; 
   billingConfig.proVODBillableDurationMinutes = 30.0; 
   billingConfig.liveBillableDurationMinutes = 15.0; 
   
   // metadata is the PTMetadata instance set on PTMediaPlayerItem 
   [metadata setMetadata:billingConfig forKey:PTBillingMetricsConfigurationMetadataKey];
   ```

## Trasmettere le metriche di fatturazione {#transmit-billing-metrics}

TVSDK invia le metriche di fatturazione ad Adobe in un formato XML.

<!--<a id="example_13ABDB1CC0B549968A534765378DA3A0"></a>-->

Se utilizzi uno strumento di acquisizione di rete per monitorare le statistiche trasmesse ad Adobe da TVSDK, dovresti vedere unità come le seguenti:

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

Le proprietà booleane `drmProtected`, `adsEnabled` e `midrollEnabled` vengono visualizzate solo se sono vere.