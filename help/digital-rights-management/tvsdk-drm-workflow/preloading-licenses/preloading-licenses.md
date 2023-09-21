---
title: Panoramica sul precaricamento delle licenze per la riproduzione offline
description: Panoramica sul precaricamento delle licenze per la riproduzione offline
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---

# Precaricamento delle licenze per la riproduzione offline {#pre-loading-licenses-for-offline-playback}

È possibile precaricare le licenze necessarie per riprodurre i contenuti protetti da Primetime DRM. Le licenze precaricate consentono agli utenti di visualizzare il contenuto indipendentemente dal fatto che dispongano di una connessione Internet attiva.

Il processo di precaricamento stesso *fa* richiede una connessione a Internet. È possibile utilizzare `DRMManager.loadVoucher()` prima del tempo necessario per precaricare le licenze. Successivamente, quando il cliente desidera riprodurre il contenuto desiderato, il sistema DRM è stato precaricato e può riprodurre immediatamente il contenuto protetto.
