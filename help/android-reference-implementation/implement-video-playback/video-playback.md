---
seo-title: Operazioni essenziali di riproduzione video
title: Operazioni essenziali di riproduzione video
description: PlaybackManager fornisce operazioni essenziali per lo streaming HLS
seo-description: PlaybackManager fornisce operazioni essenziali per lo streaming HLS
uuid: 7ac93f1f-9233-4462-a4be-528d1aa524a9
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---


# Operazioni essenziali di riproduzione video {#essential-operations-of-video-playback}

PlaybackManager fornisce le operazioni essenziali dello streaming HLS:

* Richiama [PlaybackManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.PlaybackManagerEventListener.html), che può rispondere in modo appropriato agli eventi video.
* Fornisce operazioni di riproduzione quali riproduzione, pausa e ricerca.
* Restituisce le informazioni sul lettore, ad esempio lo stato del lettore, la gamma di riproduzione e lo streaming video live.
* Determina se ABR è abilitato e imposta i parametri ABR e di controllo del buffer in base ai dati di configurazione forniti.
* Determina se il controllo del buffer è attivato e imposta i parametri del controllo del buffer in base ai dati di configurazione forniti.