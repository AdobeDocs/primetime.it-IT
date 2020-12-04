---
seo-title: Panoramica sulla distribuzione dei certificati
title: Panoramica sulla distribuzione dei certificati
uuid: e6413f9f-69a5-4881-bb13-47a80cf32a48
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---


# Panoramica {#deploy-certificates-overview}

Per aggiungere certificati ai  file delle proprietà DRM di Adobe Primetime, convertite il file PKCS#7 in un file PFX utilizzando la chiave privata e generate un file PEM o DER.

* Quando è richiesta una credenziale (certificato e chiave privata), gli strumenti della riga di comando Primetime DRM e  Adobe packager richiedono un file PFX. L’SDK, l’implementazione di riferimento e il server DRM Primetime per lo streaming protetto possono accettare un file PFX e utilizzare anche una credenziale memorizzata in un HSM.
* Quando è richiesto solo un certificato, la maggior parte dei componenti DRM Primetime può utilizzare un file PEM, un file DER o un certificato su un HSM. Il packager per HTTP Dynamic Streaming di Adobe  accetta solo i file DER per i certificati.