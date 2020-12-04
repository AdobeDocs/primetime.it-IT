---
description: 'null'
seo-description: 'null'
seo-title: Misurazione annunci da Moat
title: Misurazione annunci da Moat
uuid: a29c1e74-df15-47d2-9bd6-1d366c5cdf37
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---


# Misurazione annunci da Moat {#ad-measurement-from-moat}

TVSDK prende informazioni da FreeWheel e altri server adserver che forniscono risposte VAST. FreeWheel fornisce, all&#39;interno delle risposte VAST, informazioni dal servizio Moat. Il servizio Moat conta gli annunci con una precisione che mostra meglio che i creativi catturano o trascurano gli interessi del pubblico.

Moat è un servizio di misurazione e visualizzazione per molti usi, dai browser alle applicazioni interne. Moat genera dati di analisi di marketing in tempo reale su più piattaforme.

L&#39;XML di risposta VAST ha una proprietà e un elemento che il codice può leggere, la proprietà ad id più esterna e l&#39;elemento di estensione più esterno. In entrambi i casi, il codice può utilizzare TVSDK per salvare sia le informazioni ID annuncio che le informazioni di estensione e organizzare le informazioni in una struttura ad albero. Con questa organizzazione, il codice può raccogliere i dati da qualsiasi livello e trasmetterli ovunque sia necessario. Il valore della proprietà ad id più esterno consente al codice di coordinare le informazioni della campagna associata.

Ad esempio, FreeWheel può restituire i dati in un elemento Extensions. Di seguito è riportato un elemento di esempio.

```
<?xml version="1.0"?> 
    <Extensions> 
      <Extension type="FreeWheel"> 
        <Parameter name="moat"> 
          <MeasurementInfo renditionID="6398737" type="MediaFile"> 
            <MoatID><![CDATA[169843;56705;17860255;17860316;2509639;g8912342;103311138;g436558;530633]]></MoatID> 
          </MeasurementInfo> 
          <MeasurementInfo renditionID="6398739" type="MediaFile"> 
            <MoatID><![CDATA[169843;56705;17860255;17860316;2509639;g8912342;103311138;g436558;530633]]></MoatID> 
          </MeasurementInfo> 
        </Parameter> 
      </Extension> 
    </Extensions> 
```

La ruota libera può anche impostare la proprietà id nell&#39;elemento Ad, come mostrato nell&#39;esempio seguente.

```
<Ad id="118566" sequence="1">
```

Fate riferimento alla documentazione API per la classe AdobePSDK.NetworkAdInfo.
