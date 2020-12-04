---
description: Per rendere i sottotitoli codificati disponibili al lettore client, è necessario attivarli. È possibile attivare o disattivare i sottotitoli e selezionare la formattazione desiderata.
seo-description: Per rendere i sottotitoli codificati disponibili al lettore client, è necessario attivarli. È possibile attivare o disattivare i sottotitoli e selezionare la formattazione desiderata.
seo-title: Esposizione di sottotitoli codificati
title: Esposizione di sottotitoli codificati
uuid: 209b34ca-f14e-499e-af5f-2d8c7b359ef8
translation-type: tm+mt
source-git-commit: 25a0dfef12ecf10ba939500c4ba539468c41ee1b
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# Esporre i sottotitoli codificati {#expose-closed-captions}

Per rendere i sottotitoli codificati disponibili al lettore client, è necessario attivarli. È possibile attivare o disattivare i sottotitoli e selezionare la formattazione desiderata.

Per esporre i sottotitoli codificati:

1. In `PTMediaPlayer`, impostare la proprietà `closedCaptionDisplayEnabled`.

   Se l&#39;utente ha attivato le didascalie, questo passaggio visualizza il testo.

   >[!NOTE]
   >
   >L&#39;utente client attiva o disattiva i sottotitoli codificati utilizzando le impostazioni di accessibilità di iOS e queste impostazioni forniscono anche le opzioni di formattazione.

   >[!NOTE]
   >
   >`closedCaptionDisplayEnabled` è obsoleto. Utilizzare la proprietà `subtitlesOptions` di `PTMediaPlayerItem`. Per utilizzare i sottotitoli codificati, vedere [Esposizione dei sottotitoli](../../tvsdk-1.4-for-ios/c-psdk-ios-1.4-closed-captioning-and-subtitles-ios/t-psdk-ios-1.4-subtitles-exposing-ios.md).