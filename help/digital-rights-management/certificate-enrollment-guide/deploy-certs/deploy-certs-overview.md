---
title: Panoramica sulla distribuzione dei certificati
description: Panoramica sulla distribuzione dei certificati
copied-description: true
exl-id: 45a4bc7e-f987-4b9a-885d-d989d09566c5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---

# Panoramica {#deploy-certificates-overview}

Per aggiungere certificati ai file delle proprietà Adobe Primetime DRM, convertite il file PKCS#7 in un file PFX utilizzando la chiave privata e generate un file PEM o DER.

* Quando è richiesta una credenziale (certificato e chiave privata), gli strumenti della riga di comando DRM di Primetime e Adobe HTTP Dynamic Streaming Packager richiedono un file PFX. SDK, Reference Implementation e Primetime DRM Server for Protected Streaming accettano un file PFX e possono anche utilizzare credenziali memorizzate su un HSM.
* Quando è richiesto solo un certificato, la maggior parte dei componenti DRM di Primetime può utilizzare un file PEM, un file DER o un certificato su un HSM. Adobe HTTP Dynamic Streaming Packager accetta solo i file DER per i certificati.
