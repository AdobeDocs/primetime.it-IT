---
title: Operazioni essenziali di riproduzione video
description: PlaybackManager offre operazioni essenziali per lo streaming HLS
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
