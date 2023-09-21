---
title: Panoramica sulla distribuzione dei certificati
description: Panoramica sulla distribuzione dei certificati
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---

# Panoramica {#deploy-certificates-overview}

Per aggiungere certificati ai file delle proprietà Adobe Primetime DRM, convertite il file PKCS#7 in un file PFX utilizzando la chiave privata e generate un file PEM o DER.

* Quando è richiesta una credenziale (certificato e chiave privata), gli strumenti della riga di comando DRM di Primetime e Adobe HTTP Dynamic Streaming Packager richiedono un file PFX. SDK, Reference Implementation e Primetime DRM Server for Protected Streaming accettano un file PFX e possono anche utilizzare credenziali memorizzate su un HSM.
* Quando è richiesto solo un certificato, la maggior parte dei componenti DRM di Primetime può utilizzare un file PEM, un file DER o un certificato su un HSM. Adobe HTTP Dynamic Streaming Packager accetta solo i file DER per i certificati.
