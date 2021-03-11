---
title: Panoramica sulla distribuzione dei certificati
description: Panoramica sulla distribuzione dei certificati
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---


# Panoramica {#deploy-certificates-overview}

Per aggiungere certificati ai file delle proprietà DRM di Adobe Primetime, convertire il file PKCS#7 in un file PFX utilizzando la chiave privata e generare un file PEM o DER.

* Quando è richiesta una credenziale (certificato e chiave privata), gli strumenti della riga di comando DRM di Primetime e il packager di Adobe HTTP Dynamic Streaming richiedono un file PFX. L’SDK, l’implementazione di riferimento e il server DRM di Primetime per lo streaming protetto possono accettare un file PFX e possono inoltre utilizzare una credenziale memorizzata in un HSM.
* Quando è richiesto solo un certificato, la maggior parte dei componenti DRM di Primetime può utilizzare un file PEM, un file DER o un certificato su un HSM. Il packager Adobe HTTP Dynamic Streaming accetta solo file DER per i certificati.