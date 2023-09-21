---
description: Un oggetto MediaResource rappresenta il contenuto che verrà caricato dall'istanza di MediaPlayer.
title: Classi MediaPlayer e MediaResource
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---

# Classi MediaPlayer e MediaResource {#mediaplayer-and-mediaresource-classes}

Un oggetto MediaResource rappresenta il contenuto che verrà caricato dall&#39;istanza di MediaPlayer.

<!--<a id="section_431AB7221E0249BF949EC72EEB9B428A"></a>-->

TVSDK consente di caricare e preparare il contenuto per la riproduzione utilizzando `replaceCurrentResource` metodo in `MediaPlayer`. Questo metodo accetta due argomenti, un&#39;istanza di `MediaPlayerResource` e, facoltativamente, un&#39;istanza di `MediaPlayerItemConfig`, che può essere utilizzato per trasmettere parametri personalizzati definiti dall&#39;applicazione.

* Per maggiori dettagli vedi mediaplayer-reuse-or-remove .
* Per informazioni dettagliate su `MediaPlayerResource`, consulta media-resource-create
