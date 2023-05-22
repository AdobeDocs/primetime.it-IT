---
title: Misurazione degli annunci da Moat
description: Misurazione degli annunci da Moat
copied-description: true
exl-id: 3d54ca34-0b75-4a8e-ab2d-bbe59683c2cf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# Misurazione degli annunci da Moat {#ad-measurement-from-moat}

TVSDK prende le informazioni da FreeWheel e da altri amministratori che forniscono risposte VAST. FreeWheel fornisce, all&#39;interno delle risposte VAST, informazioni dal servizio Moat. Il servizio Moat conta e impressiona con una precisione che mostra meglio che i creativi catturano o trascurano gli interessi di un pubblico.

Moat è un servizio che misura e visualizza molti utilizzi, dai browser all’interno delle applicazioni. Moat genera dati di analisi di marketing in tempo reale su più piattaforme.

Il file XML di risposta VAST include una proprietà e un elemento che può essere letto dal codice, la proprietà dell’ID annuncio più esterno e l’elemento di estensione più esterno. In entrambi i casi, il codice può utilizzare TVSDK per salvare sia le informazioni sull’ID annuncio che quelle sull’estensione e per organizzare le informazioni in una struttura ad albero. Con questa organizzazione, il codice può raccogliere i dati da qualsiasi livello e trasmetterli ovunque sia necessario. Il valore della proprietà dell’ID annuncio più esterno consente al codice di coordinare le informazioni della campagna associata.

Ad esempio, FreeWheel può restituire dati in un elemento Extensions. Di seguito è riportato un elemento di esempio.

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

La ruota libera può anche impostare la proprietà id nell&#39;elemento annuncio, come mostrato nell&#39;esempio seguente.

```
<Ad id="118566" sequence="1">
```

Consulta la documentazione API per la classe AdobePSDK.NetworkAdInfo.
