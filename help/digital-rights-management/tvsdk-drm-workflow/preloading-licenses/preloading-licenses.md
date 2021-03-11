---
title: Panoramica sul precaricamento delle licenze per la riproduzione offline
description: Panoramica sul precaricamento delle licenze per la riproduzione offline
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---


# Licenze di precaricamento per la riproduzione offline {#pre-loading-licenses-for-offline-playback}

È possibile precaricare le licenze necessarie per riprodurre contenuti protetti da DRM di Primetime. Le licenze precaricate consentono agli utenti di visualizzare il contenuto indipendentemente dal fatto che abbiano o meno una connessione Internet attiva.

Il processo di precaricamento stesso *does* richiede una connessione Internet. È possibile utilizzare `DRMManager.loadVoucher()` in anticipo per precaricare le licenze. Successivamente, quando il cliente desidera riprodurre il contenuto desiderato, il sistema DRM è stato pre-preparato e può riprodurre immediatamente il contenuto protetto.
