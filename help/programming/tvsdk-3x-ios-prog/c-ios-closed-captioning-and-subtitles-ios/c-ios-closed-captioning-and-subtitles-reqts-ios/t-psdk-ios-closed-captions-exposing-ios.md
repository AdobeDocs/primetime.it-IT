---
description: Per rendere i sottotitoli codificati disponibili per il lettore client, devi abilitarli. L’utente può attivare o disattivare i sottotitoli codificati e selezionare la formattazione.
title: Mostra sottotitoli codificati
exl-id: 6383a2b2-04e3-4fe1-a573-5e1f1ef486ed
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---

# Mostra sottotitoli codificati {#expose-closed-captions}

Per rendere i sottotitoli codificati disponibili per il lettore client, devi abilitarli. L’utente può attivare o disattivare i sottotitoli codificati e selezionare la formattazione.

Per esporre sottotitoli codificati:

1. In entrata `PTMediaPlayer` oggetto, impostare `closedCaptionDisplayEnabled` proprietà.

   Se l’utente ha abilitato i sottotitoli codificati, questo passaggio visualizza il testo.

   >[!NOTE]
   >
   >L’utente client attiva o disattiva i sottotitoli codificati utilizzando le Impostazioni di accessibilità di iOS e queste impostazioni forniscono anche opzioni di formattazione.

   >[!NOTE]
   >
   >`closedCaptionDisplayEnabled` è obsoleto. Utilizzare `subtitlesOptions` proprietà di `PTMediaPlayerItem`. Consulta [Esposizione sottotitoli](../../../tvsdk-3x-ios-prog/c-ios-closed-captioning-and-subtitles-ios/c-ios-closed-captioning-and-subtitles-reqts-ios/t-ios-subtitles-exposing-ios.md) per utilizzare i sottotitoli.
