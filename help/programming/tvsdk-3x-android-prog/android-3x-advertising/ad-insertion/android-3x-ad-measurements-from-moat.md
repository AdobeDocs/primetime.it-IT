---
description: TVSDK prende informazioni da FreeWheel e altri server di annunci che forniscono risposte VAST. FreeWheel fornisce, nelle risposte VAST, informazioni dal servizio Moat. Il servizio Moat conta le impressioni degli annunci con una precisione che mostra meglio se i creativi catturano o trascurano gli interessi del pubblico.
title: Misurazioni di annunci da Moat
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 0%

---


# Misurazioni dell&#39;annuncio da Moat {#ad-measurements-from-moat}

TVSDK prende informazioni da FreeWheel e altri server di annunci che forniscono risposte VAST. FreeWheel fornisce, nelle risposte VAST, informazioni dal servizio Moat. Il servizio Moat conta le impressioni degli annunci con una precisione che mostra meglio se i creativi catturano o trascurano gli interessi del pubblico.

Moat è un servizio che misura e visualizza in molti usi, dai browser all&#39;interno delle applicazioni. Moat genera dati di analisi di marketing in tempo reale su più piattaforme.

L&#39;XML di risposta VAST ha una proprietà e un elemento leggibile dal codice, la proprietà `Ad id` più esterna e l&#39;elemento `Extension` più esterno. In entrambi i casi, il codice può utilizzare TVSDK per salvare le informazioni `Ad id` e `Extension`, quindi organizzare le informazioni in una struttura ad albero. Con questa organizzazione, il tuo codice può raccogliere i dati da qualsiasi livello e passarli ovunque debba andare. Il valore della proprietà `Ad id` più esterna consente al codice di coordinare le informazioni della campagna associata.

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

La ruota libera può anche impostare la proprietà `id` nell&#39;elemento `Ad` , come illustrato nell&#39;esempio seguente.

```xml
<Ad id="118566" sequence="1">
```

Per informazioni sulle API, consulta la documentazione API per la classe `NetworkAdInfo`.