---
title: Operazioni essenziali di riproduzione video
description: PlaybackManager offre operazioni essenziali per lo streaming HLS
exl-id: b4d1b41a-7a16-47f5-be88-6b52f0451813
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---

# Operazioni essenziali di riproduzione video {#essential-operations-of-video-playback}

PlaybackManager offre le operazioni essenziali per lo streaming HLS:

* Richiama [PlaybackManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.PlaybackManagerEventListener.html), in grado di rispondere in modo appropriato agli eventi video.
* Fornisce operazioni di riproduzione come riproduzione, pausa e ricerca.
* Restituisce le informazioni sul lettore, ad esempio lo stato, l’intervallo di riproduzione e il flusso live del video.
* Determina se ABR è abilitato e imposta i parametri di controllo ABR e buffer in base ai dati di configurazione forniti.
* Determina se il controllo del buffer è abilitato e imposta i parametri di controllo del buffer in base ai dati di configurazione forniti.
