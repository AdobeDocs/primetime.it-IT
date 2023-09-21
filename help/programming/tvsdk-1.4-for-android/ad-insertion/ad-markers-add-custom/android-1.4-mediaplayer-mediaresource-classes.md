---
description: Un oggetto MediaResource rappresenta il contenuto che verrà caricato dall'istanza di MediaPlayer.
title: Classi MediaPlayer e MediaResource
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# Classi MediaPlayer e MediaResource{#mediaplayer-and-mediaresource-classes}

Un oggetto MediaResource rappresenta il contenuto che verrà caricato dall&#39;istanza di MediaPlayer.

<!--<a id="section_B09A012C97454AF58CE2269B800D8027"></a>-->

La libreria TVSDK fornisce un modo semplice per caricare e preparare il contenuto per la riproduzione utilizzando `replaceCurrentItem` nell&#39;interfaccia MediaPlayer. Questo metodo riceve un&#39;istanza della classe MediaResource come unico argomento di input. La classe MediaResource è composta dalle informazioni seguenti:

* Un URL, che rappresenta la posizione del contenuto che sta per essere caricato.
* Un tipo, che è il tipo di contenuto che sta per essere caricato.

  Questa è una semplice enumerazione nel `MediaResource` classe che definisce i tipi di contenuto che possono essere caricati da MediaPlayer. I valori possibili sono HLS e HDS. Ogni valore è associato alla stringa che rappresenta le estensioni di file comunemente utilizzate, `m3u8` per HLS e `f4m` per HDS.
* Alcuni metadati, che è un’istanza di `Metadata` classe.

  Questa struttura simile al dizionario può contenere informazioni aggiuntive sul contenuto che sta per essere caricato, ad esempio informazioni sul contenuto alternativo/annuncio che deve essere inserito nel contenuto principale.

I metadati sono il mezzo attraverso il quale le informazioni relative al contenuto alternativo vengono passate a TVSDK. Il `Metadata` L’interfaccia definisce l’API per un archivio chiave-valore generico, dove sia la chiave che il valore sono stringhe semplici.
