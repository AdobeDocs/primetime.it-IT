---
title: Panoramica sul precaricamento delle licenze per la riproduzione offline
description: Panoramica sul precaricamento delle licenze per la riproduzione offline
copied-description: true
exl-id: 0d49c0e4-821b-4354-b92d-bbe2c07e467b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---

# Precaricamento delle licenze per la riproduzione offline {#pre-loading-licenses-for-offline-playback}

È possibile precaricare le licenze necessarie per riprodurre i contenuti protetti da Primetime DRM. Le licenze precaricate consentono agli utenti di visualizzare il contenuto indipendentemente dal fatto che dispongano di una connessione Internet attiva.

Il processo di precaricamento stesso *fa* richiede una connessione a Internet. È possibile utilizzare `DRMManager.loadVoucher()` prima del tempo necessario per precaricare le licenze. Successivamente, quando il cliente desidera riprodurre il contenuto desiderato, il sistema DRM è stato precaricato e può riprodurre immediatamente il contenuto protetto.
