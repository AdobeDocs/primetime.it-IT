---
description: MediaResource rappresenta il contenuto che sta per essere caricato dall'istanza MediaPlayer.
title: Classi MediaPlayer e MediaResource
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---


# Classi MediaPlayer e MediaResource{#mediaplayer-and-mediaresource-classes}

MediaResource rappresenta il contenuto che sta per essere caricato dall&#39;istanza MediaPlayer.

<!--<a id="section_B09A012C97454AF58CE2269B800D8027"></a>-->

La libreria TVSDK fornisce un mezzo semplice per caricare e preparare il contenuto per la riproduzione utilizzando il metodo `replaceCurrentItem` nell&#39;interfaccia MediaPlayer. Questo metodo riceve un&#39;istanza della classe MediaResource come unico argomento di input. La classe MediaResource è composta dalle seguenti informazioni:

* Un URL che rappresenta la posizione del contenuto che sta per essere caricato.
* Un tipo, che è il tipo di contenuto che sta per essere caricato.

   Si tratta di una semplice enumerazione nella classe `MediaResource` che definisce i tipi di contenuto che possono essere caricati da MediaPlayer. I valori possibili sono HLS e HDS. Ogni valore è associato alla stringa che rappresenta le estensioni dei file comunemente utilizzate, `m3u8` per HLS e `f4m` per HDS.
* Alcuni metadati, che è un&#39;istanza della classe `Metadata`.

   Questa struttura simile a un dizionario potrebbe contenere informazioni aggiuntive sul contenuto che sta per essere caricato, ad esempio informazioni sul contenuto alternativo/annuncio che deve essere inserito nel contenuto principale.

I metadati sono il mezzo tramite il quale le informazioni relative al contenuto alternativo vengono trasmesse a TVSDK. L’interfaccia `Metadata` definisce l’API per un archivio chiave-valore generico, in cui sia la chiave che il valore sono stringhe semplici.
