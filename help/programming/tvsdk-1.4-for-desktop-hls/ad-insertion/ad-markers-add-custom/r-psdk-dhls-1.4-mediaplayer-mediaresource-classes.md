---
description: MediaResource rappresenta il contenuto che sta per essere caricato dall'istanza MediaPlayer.
seo-description: MediaResource rappresenta il contenuto che sta per essere caricato dall'istanza MediaPlayer.
seo-title: Classi MediaPlayer e MediaResource
title: Classi MediaPlayer e MediaResource
uuid: 36ef75f3-08f7-4fc5-88a7-9bab9198b917
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Classi MediaPlayer e MediaResource{#mediaplayer-and-mediaresource-classes}

MediaResource rappresenta il contenuto che sta per essere caricato dall&#39;istanza MediaPlayer.

<!--<a id="section_B09A012C97454AF58CE2269B800D8027"></a>-->

La libreria TVSDK fornisce uno strumento semplice per caricare e preparare il contenuto per la riproduzione utilizzando il `replaceCurrentResource` metodo nell&#39; `MediaPlayer` interfaccia. Questo metodo riceve un&#39;istanza della `MediaResource` classe come unico argomento di input. La `MediaResource` classe è composta dalle seguenti informazioni:

* Un URL che rappresenta la posizione del contenuto che sta per essere caricato.
* Un tipo, che è il tipo di contenuto che sta per essere caricato.

   Si tratta di una stringa che definisce i tipi di contenuto che possono essere caricati dall&#39; `MediaPlayer`. I valori possibili sono HLS e HDS. Ogni valore è associato alla stringa che rappresenta le estensioni di file comunemente utilizzate, &quot;m3u8&quot; per HLS e &quot;f4m&quot; per HDS.
* Alcuni metadati, ovvero un&#39;istanza della `Metadata` classe.

   Questa struttura simile a un dizionario potrebbe contenere informazioni aggiuntive sul contenuto che sta per essere caricato, ad esempio informazioni sul contenuto alternativo/ad che dovrebbe essere inserito nel contenuto principale.

I metadati sono il mezzo attraverso il quale le informazioni relative a contenuti alternativi vengono trasmesse a TVSDK. L&#39; `Metadata` interfaccia definisce l&#39;API per un archivio chiave-valore generico, in cui sia la chiave che il valore sono stringhe semplici.
