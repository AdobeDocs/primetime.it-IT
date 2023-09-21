---
description: TVSDK prende informazioni da FreeWheel e altri server di annunci che forniscono risposte VAST. FreeWheel fornisce, all'interno delle risposte VAST, informazioni dal servizio Moat. Il servizio Moat conta le impression con una precisione che mostra meglio se i creativi catturano o trascurano gli interessi di un pubblico.
title: Misurazioni degli annunci da Moat
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# Misurazioni degli annunci da Moat{#ad-measurements-from-moat}

TVSDK prende informazioni da FreeWheel e altri server di annunci che forniscono risposte VAST. FreeWheel fornisce, all&#39;interno delle risposte VAST, informazioni dal servizio Moat. Il servizio Moat conta le impression con una precisione che mostra meglio se i creativi catturano o trascurano gli interessi di un pubblico.

Moat è un servizio che misura e visualizza molti utilizzi, dai browser all’interno delle applicazioni. Moat genera dati di analisi di marketing in tempo reale su più piattaforme.

Il file XML di risposta VAST include una proprietà e un elemento che il codice è in grado di leggere, il più esterno `Ad id` proprietà e l&#39;ambiente più esterno `Extension` elemento. In entrambi i casi, il codice può utilizzare TVSDK per salvare entrambi `Ad id` informazioni e `Extension` informazioni, quindi organizzarle in una struttura ad albero. Con questa organizzazione, il codice può raccogliere i dati da qualsiasi livello e trasmetterli ovunque sia necessario. Il valore della `Ad id` consente al codice di coordinare le informazioni della campagna associata.

Ad esempio, FreeWheel può restituire dati in un elemento Extensions. Di seguito è riportato un elemento di esempio.

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

La ruota libera può anche impostare `id` proprietà in `Ad` come mostrato nell’esempio di seguito.

```xml
<Ad id="118566" sequence="1">
```

Per informazioni API, consulta la documentazione API per la classe [NetworkAdInfo](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.7/)
