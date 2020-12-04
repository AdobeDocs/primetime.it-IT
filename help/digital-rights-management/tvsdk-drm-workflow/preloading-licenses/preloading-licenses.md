---
seo-title: Panoramica sul precaricamento delle licenze per la riproduzione offline
title: Panoramica sul precaricamento delle licenze per la riproduzione offline
uuid: 71e5169b-7f70-4723-9f9b-fdff822c5876
translation-type: tm+mt
source-git-commit: 9bbcb228d3367fbf53de811bf2941ca653ce3b0e
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---


# Precaricamento delle licenze per la riproduzione offline {#pre-loading-licenses-for-offline-playback}

Potete precaricare le licenze necessarie per riprodurre contenuto protetto da DRM di Primetime. Le licenze precaricate consentono agli utenti di visualizzare il contenuto indipendentemente dal fatto che dispongano o meno di una connessione Internet attiva.

Il processo di precaricamento *non* richiede una connessione Internet. È possibile utilizzare `DRMManager.loadVoucher()` in anticipo per precaricare le licenze. Successivamente, quando il cliente desidera riprodurre il contenuto desiderato, il sistema DRM è stato pre-preparato e può riprodurre immediatamente il contenuto protetto.
