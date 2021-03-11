---
title: Operazioni essenziali di riproduzione video
description: PlaybackManager fornisce operazioni essenziali dello streaming HLS
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---


# Operazioni essenziali di riproduzione video {#essential-operations-of-video-playback}

PlaybackManager fornisce operazioni essenziali di streaming HLS:

* Richiama il [PlaybackManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.PlaybackManagerEventListener.html), che può rispondere in modo appropriato agli eventi video.
* Fornisce operazioni di riproduzione quali riproduzione, pausa e ricerca.
* Restituisce le informazioni sul lettore, ad esempio lo stato del lettore, l&#39;intervallo di riproduzione e lo streaming video in diretta.
* Determina se l&#39;ABR è abilitato e imposta i parametri di controllo ABR e buffer in base ai dati di configurazione forniti.
* Determina se il controllo del buffer è abilitato e imposta i parametri di controllo del buffer in base ai dati di configurazione forniti.