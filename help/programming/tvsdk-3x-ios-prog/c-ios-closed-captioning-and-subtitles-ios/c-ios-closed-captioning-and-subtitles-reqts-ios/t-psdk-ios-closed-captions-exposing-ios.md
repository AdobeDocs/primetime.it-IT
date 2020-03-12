---
description: Per rendere i sottotitoli codificati disponibili al lettore client, è necessario attivarli. È possibile attivare o disattivare i sottotitoli e selezionare la formattazione desiderata.
seo-description: Per rendere i sottotitoli codificati disponibili al lettore client, è necessario attivarli. È possibile attivare o disattivare i sottotitoli e selezionare la formattazione desiderata.
seo-title: Esposizione di sottotitoli codificati
title: Esposizione di sottotitoli codificati
uuid: 7057014a-b14a-4790-8f7f-37d7a1fb8194
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Esposizione di sottotitoli codificati {#expose-closed-captions}

Per rendere i sottotitoli codificati disponibili al lettore client, è necessario attivarli. È possibile attivare o disattivare i sottotitoli e selezionare la formattazione desiderata.

Per esporre i sottotitoli codificati:

1. In `PTMediaPlayer` object, impostare la `closedCaptionDisplayEnabled` proprietà.

   Se l&#39;utente ha attivato le didascalie, questo passaggio visualizza il testo.

   >[!NOTE]
   >
   >L&#39;utente client attiva o disattiva i sottotitoli codificati utilizzando le impostazioni di accessibilità di iOS e queste impostazioni forniscono anche le opzioni di formattazione.

   >[!NOTE]
   >
   >`closedCaptionDisplayEnabled` è obsoleto. Utilizzare `subtitlesOptions` proprietà di `PTMediaPlayerItem`. Consultate [Esporre i sottotitoli](../../../tvsdk-3x-ios-prog/c-ios-closed-captioning-and-subtitles-ios/c-ios-closed-captioning-and-subtitles-reqts-ios/t-ios-subtitles-exposing-ios.md) per utilizzare i sottotitoli codificati.