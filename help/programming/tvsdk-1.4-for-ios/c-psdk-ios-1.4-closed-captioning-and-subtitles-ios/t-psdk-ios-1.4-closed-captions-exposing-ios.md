---
description: Per rendere i sottotitoli codificati disponibili al lettore client, è necessario attivarli. L’utente può attivare o disattivare i sottotitoli codificati e selezionare la formattazione.
title: Esporre sottotitoli codificati
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---


# Esporre sottotitoli codificati {#expose-closed-captions}

Per rendere i sottotitoli codificati disponibili al lettore client, è necessario attivarli. L’utente può attivare o disattivare i sottotitoli codificati e selezionare la formattazione.

Per esporre i sottotitoli codificati:

1. Nell&#39;oggetto `PTMediaPlayer`, impostare la proprietà `closedCaptionDisplayEnabled` .

   Se l’utente ha abilitato le didascalie, in questo passaggio viene visualizzato il testo.

   >[!NOTE]
   >
   >L’utente client attiva o disattiva i sottotitoli codificati utilizzando le impostazioni di accessibilità di iOS e queste impostazioni forniscono anche opzioni di formattazione.

   >[!NOTE]
   >
   >`closedCaptionDisplayEnabled` è obsoleta. Utilizzare la proprietà `subtitlesOptions` di `PTMediaPlayerItem`. Per utilizzare i sottotitoli codificati, vedere [Esporre i sottotitoli](../../tvsdk-1.4-for-ios/c-psdk-ios-1.4-closed-captioning-and-subtitles-ios/t-psdk-ios-1.4-subtitles-exposing-ios.md) .