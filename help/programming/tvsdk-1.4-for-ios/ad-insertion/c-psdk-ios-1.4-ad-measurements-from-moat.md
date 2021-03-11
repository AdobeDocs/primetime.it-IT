---
description: TVSDK prende informazioni da FreeWheel e da altri server di amministrazione che forniscono risposte VAST. FreeWheel fornisce, nelle risposte VAST, informazioni dal servizio Moat. Il servizio Moat conta le impressioni degli annunci con una precisione che dimostra meglio che i creativi catturano o trascurano gli interessi del pubblico.
title: Misurazioni di annunci da Moat
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---


# Misure annunci da Moat{#ad-measurements-from-moat}

TVSDK prende informazioni da FreeWheel e da altri server di amministrazione che forniscono risposte VAST. FreeWheel fornisce, nelle risposte VAST, informazioni dal servizio Moat. Il servizio Moat conta le impressioni degli annunci con una precisione che dimostra meglio che i creativi catturano o trascurano gli interessi del pubblico.

Moat è un servizio che misura e visualizza in molti usi, dai browser all&#39;interno delle applicazioni. Moat genera dati di analisi di marketing in tempo reale su più piattaforme.

L&#39;XML di risposta VAST dispone di una proprietà e di un elemento leggibile dal codice, della proprietà dell&#39;ad id più esterno e dell&#39;elemento dell&#39;estensione più esterno. In entrambi i casi, il codice può utilizzare TVSDK per salvare sia le informazioni sull’id dell’annuncio che le informazioni sull’estensione e organizzare le informazioni in una struttura ad albero. Con questa organizzazione, il tuo codice può raccogliere i dati da qualsiasi livello e passarli ovunque debba andare. Il valore della proprietà id annuncio esterno consente al codice di coordinare le informazioni della campagna associata.

Ad esempio, FreeWheel può restituire i dati in un elemento Extensions. Di seguito è riportato un elemento di esempio.

```xml
<Extensions> 
   <Extension type="FreeWheel"> 
    <Parameter name="moat"> 
     <MeasurementInfo renditionID="6398737" type="MediaFile"> 
      <MoatID> 
       <![CDATA[169843;56705;17860255;17860316;2509639;g8912342;103311138;g436558;530633]]]]> 
       <![CDATA[> 
        </MoatID> 
      </MeasurementInfo> 
      <MeasurementInfo renditionID="6398739" type="MediaFile"> 
        <MoatID> 
        <![CDATA[169843;56705;17860255;17860316;2509639;g8912342;103311138;g436558;530633]]]]> 
        <![CDATA[> 
        </MoatID> 
      </MeasurementInfo> 
    </Parameter> 
  </Extension> 
</Extensions>
```

La ruota libera può anche impostare la proprietà id nell’elemento Ad , come mostrato nell’esempio di seguito.

```
<Ad id="118566" sequence="1">
```

Fai riferimento alla documentazione API per la classe `PTNetworkAdInfo` in `PTAdAsset`.
