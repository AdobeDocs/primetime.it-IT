---
title: Note sulla versione di Primetime
description: Note sulla versione di Primetime
copied-description: true
translation-type: tm+mt
source-git-commit: 944bfb0f3bd0050a9d2974a37f4fabddaaac8a93
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 29%

---


# Note sulla versione di Primetime

Benvenuto nelle note sulla versione di Adobe Primetime. I documenti elencati nella navigazione a sinistra forniscono informazioni specifiche sulla versione, requisiti di sistema, limitazioni, problemi risolti e problemi noti.

## Miglioramenti e correzioni in TVSDK 3.13 iOS

Il rilascio introduce il supporto per gli annunci DEMUXED &quot;HLS/CMAF&quot; (preroll, midroll e postroll) per flussi LIVE, VOD e FER.

Per altre correzioni e dettagli, consulta [TVSDK per le note sulla versione iOS](../release-notes/tvsdk-3x-ios.md)

## Miglioramenti e correzioni in PTAI 21.2.2

Il rilascio include il supporto per l&#39;inserimento/sincronizzazione del flusso EXT-X-IMAGE-STREAM-INF nei flussi HLS. La funzione viene abilitata tramite una configurazione lato server. Contatta il rappresentante del tuo account tecnico per abilitare la funzione.

## Correzioni in TVSDK 3.13 Android

Questo rilascio fornisce una soluzione al problema del congelamento del flusso DRM Widevine o la visualizzazione di fotogrammi neri sull&#39;interruttore ABR su dispositivi FireTV, che includono Fire TV 3rd generation Pendant e Fire TV Cube 1st e 2a generazione dispositivi.

Per risolvere il problema, impostare l&#39;API `MediaPlayer.flushVideoDecoderOnHeaderChange(true)` per i dispositivi Fire TV specificati prima di avviare la riproduzione. Il valore predefinito è false.

Per ulteriori informazioni, consulta le [Note sulla versione TVSDK per Android](../release-notes/tvsdk-3x-android.md) .

## Miglioramenti e correzioni nelle note sulla versione di TVSDK 3.12 iOS

Il rilascio si è concentrato sulla soluzione dei principali problemi dei clienti.

Per ulteriori informazioni sulla versione rilasciata corrente, consulta [iOS](../release-notes/tvsdk-3x-ios.md) .

## Vedi anche

| Guida utente | Descrizione |
|--- |--- |
| [Guida alla programmazione per Primetime](/help/programming/home.md) | Consente di imparare a sviluppare applicazioni e lettori video utilizzando Java su dispositivi Android e Objective-C su dispositivi iOS. |
| [Guida alla migrazione e alla conversione di Primetime](/help/migration-guides/home.md) | Illustra il processo di conversione e migrazione per passare dalla suite TVSDK Primetime esistente alla suite di nuova generazione. |
| [Implementazione di riferimento](/help/android-reference-implementation/home.md) | Consente di comprendere il TVSDK e modificare i gestori delle funzioni per personalizzare il lettore personale. |
| [Riferimenti API di Primetime](/help/reference/api-references.md) | Fornisce informazioni dettagliate sulle funzioni TVSDK, le strutture di dati e altri costrutti di programmazione. |
| [Digital Rights Management](/help/digital-rights-management/home.md) | Consente di ottenere ulteriori informazioni sui vari scenari utente nel Digital Rights Management (DRM) |
| [Guida di Primetime Ad Insertion](/help/primetime-ad-insertion/home.md) | Spiega come monetizzare i contenuti inserendo sul server annunci dinamici mirati agli utenti e coinvolgendo il pubblico con annunci personalizzati. |
| [Archivi](https://helpx.adobe.com/primetime/archives.html) | Scarica i PDF della documentazione archiviata. |

## Risorse utili

* [Scopri Adobe Primetime](https://www.adobe.com/in/marketing/primetime.html)

* [Monitoraggio della concorrenza](https://tve.helpdocsonline.com/concurrency-monitoring-introduction)

* [Autenticazione Primetime](https://tve.helpdocsonline.com/home)

* [Forum DRM di Adobe Primetime](https://forums.adobe.com/community/adobe_access)

* [Risorse per sviluppatori di Adobe Primetime](https://www.adobe.com/devnet/primetime.html)
