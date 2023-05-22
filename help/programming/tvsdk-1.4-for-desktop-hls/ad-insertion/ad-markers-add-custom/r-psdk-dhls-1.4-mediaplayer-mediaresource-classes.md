---
description: Un oggetto MediaResource rappresenta il contenuto che verrà caricato dall'istanza di MediaPlayer.
title: Classi MediaPlayer e MediaResource
exl-id: c431c9f9-98a3-402c-b799-450f30f668dd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# Classi MediaPlayer e MediaResource{#mediaplayer-and-mediaresource-classes}

Un oggetto MediaResource rappresenta il contenuto che verrà caricato dall&#39;istanza di MediaPlayer.

<!--<a id="section_B09A012C97454AF58CE2269B800D8027"></a>-->

La libreria TVSDK fornisce un modo semplice per caricare e preparare il contenuto per la riproduzione utilizzando `replaceCurrentResource` metodo in `MediaPlayer` di rete. Questo metodo riceve un&#39;istanza del `MediaResource` come unico argomento di input. Il `MediaResource` la classe è composta dalle seguenti informazioni:

* Un URL, che rappresenta la posizione del contenuto che sta per essere caricato.
* Un tipo, che è il tipo di contenuto che sta per essere caricato.

   Si tratta di una stringa che definisce i tipi di contenuto che possono essere caricati da `MediaPlayer`. I valori possibili sono HLS e HDS. Ogni valore è associato alla stringa che rappresenta le estensioni di file comunemente utilizzate, &quot;m3u8&quot; per HLS e &quot;f4m&quot; per HDS.
* Alcuni metadati, che è un’istanza di `Metadata` classe.

   Questa struttura simile al dizionario può contenere informazioni aggiuntive sul contenuto che sta per essere caricato, ad esempio informazioni sul contenuto alternativo/annuncio che deve essere inserito nel contenuto principale.

I metadati sono il mezzo attraverso il quale le informazioni relative al contenuto alternativo vengono passate a TVSDK. Il `Metadata` L’interfaccia definisce l’API per un archivio chiave-valore generico, dove sia la chiave che il valore sono stringhe semplici.
