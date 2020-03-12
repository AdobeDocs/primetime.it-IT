---
description: MediaResource rappresenta il contenuto che sta per essere caricato dall'istanza MediaPlayer.
seo-description: MediaResource rappresenta il contenuto che sta per essere caricato dall'istanza MediaPlayer.
seo-title: Classi MediaPlayer e MediaResource
title: Classi MediaPlayer e MediaResource
uuid: 7393c320-7dbb-4580-9425-a735f9d03ef5
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Classi MediaPlayer e MediaResource{#mediaplayer-and-mediaresource-classes}

MediaResource rappresenta il contenuto che sta per essere caricato dall&#39;istanza MediaPlayer.

<!--<a id="section_B09A012C97454AF58CE2269B800D8027"></a>-->

La libreria TVSDK fornisce un metodo semplice per caricare e preparare il contenuto per la riproduzione utilizzando il `replaceCurrentItem` metodo nell’interfaccia di MediaPlayer. Questo metodo riceve un&#39;istanza della classe MediaResource come unico argomento di input. La classe MediaResource è composta dalle seguenti informazioni:

* Un URL che rappresenta la posizione del contenuto che sta per essere caricato.
* Un tipo, che è il tipo di contenuto che sta per essere caricato.

   Si tratta di una semplice enumerazione nella `MediaResource` classe che definisce i tipi di contenuto che è possibile caricare da MediaPlayer. I valori possibili sono HLS e HDS. Ciascun valore è associato alla stringa che rappresenta le estensioni di file comunemente utilizzate, `m3u8` per HLS e `f4m` per HDS.
* Alcuni metadati, ovvero un&#39;istanza della `Metadata` classe.

   Questa struttura simile a un dizionario potrebbe contenere informazioni aggiuntive sul contenuto che sta per essere caricato, ad esempio informazioni sul contenuto alternativo/ad che dovrebbe essere inserito nel contenuto principale.

I metadati sono il mezzo attraverso il quale le informazioni relative a contenuti alternativi vengono trasmesse a TVSDK. L&#39; `Metadata` interfaccia definisce l&#39;API per un archivio chiave-valore generico, in cui sia la chiave che il valore sono stringhe semplici.
