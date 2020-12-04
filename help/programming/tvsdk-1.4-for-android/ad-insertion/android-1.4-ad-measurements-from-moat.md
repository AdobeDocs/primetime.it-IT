---
description: TVSDK prende informazioni da FreeWheel e altri server di annunci che forniscono risposte VAST. FreeWheel fornisce, all'interno delle risposte VAST, informazioni dal servizio Moat. Il servizio Moat conta gli annunci con una precisione che mostra meglio se i creativi catturano o trascurano gli interessi del pubblico.
seo-description: TVSDK prende informazioni da FreeWheel e altri server di annunci che forniscono risposte VAST. FreeWheel fornisce, all'interno delle risposte VAST, informazioni dal servizio Moat. Il servizio Moat conta gli annunci con una precisione che mostra meglio se i creativi catturano o trascurano gli interessi del pubblico.
seo-title: Misurazioni di annunci da Moat
title: Misurazioni di annunci da Moat
uuid: 73ef3a14-7ad6-4e67-8ad3-eabbeb898a09
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---


# Aggiungi misurazioni da Moat{#ad-measurements-from-moat}

TVSDK prende informazioni da FreeWheel e altri server di annunci che forniscono risposte VAST. FreeWheel fornisce, all&#39;interno delle risposte VAST, informazioni dal servizio Moat. Il servizio Moat conta gli annunci con una precisione che mostra meglio se i creativi catturano o trascurano gli interessi del pubblico.

Moat è un servizio di misurazione e visualizzazione per molti usi, dai browser alle applicazioni interne. Moat genera dati di analisi di marketing in tempo reale su più piattaforme.

L&#39;XML di risposta VAST ha una proprietà e un elemento che il codice può leggere, la proprietà `Ad id` più esterna e l&#39;elemento `Extension` più esterno. In entrambi i casi, il codice può utilizzare TVSDK per salvare le informazioni `Ad id` e `Extension`, quindi organizzare le informazioni in una struttura ad albero. Con questa organizzazione, il codice può raccogliere i dati da qualsiasi livello e trasmetterli ovunque sia necessario. Il valore della proprietà `Ad id` più esterna consente al codice di coordinare le informazioni della campagna associata.

Ad esempio, FreeWheel può restituire i dati in un elemento Extensions. Di seguito è riportato un elemento di esempio.

```xml
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

La ruota libera può anche impostare la proprietà `id` nell&#39;elemento `Ad`, come illustrato nell&#39;esempio seguente.

```xml
<Ad id="118566" sequence="1">
```

Fate riferimento alla documentazione API per la classe `NetworkAdInfo`.
