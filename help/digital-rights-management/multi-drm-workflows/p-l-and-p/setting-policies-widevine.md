---
title: Utilizzo dei criteri di protezione dell'output
description: Utilizzo dei criteri di protezione dell'output
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---


# Utilizzo dei criteri di protezione dell&#39;output{#using-output-protection-policies}

**Criteri di protezione dell&#39;output di Widevine**

Widevine supporta in modo nativo le restrizioni di protezione dell&#39;uscita analogica e digitale. Consulta la documentazione del provider di servizi Widevine su come allegare questi criteri alle licenze generate.

Se utilizzi Expressplay come provider di servizi Widevine, allega i criteri di protezione dell’output digitale al momento della generazione del token tramite il flag hdcpOutputControl:
I valori consentiti sono 0, 1, 2 dove 0 = HDCP_NONE, 1 = HDCP_V1, 2 = HDCP_V2. HDCP_V1 e HDCP_V2 applicano rispettivamente le versioni HDCP 1.X e 2.X.

Expressplay attualmente non supporta l&#39;associazione di restrizioni all&#39;uscita analogica

**Criteri di protezione dell&#39;output PlayReady**

PlayReady supporta inoltre in modo nativo restrizioni di protezione dell&#39;uscita analogica e digitale. I valori del livello di protezione dell&#39;output che è possibile impostare. La pagina [Livelli di protezione dell&#39;output](https://msdn.microsoft.com/en-us/library/dn468831.aspx) documenta i valori che è possibile impostare e il relativo comportamento client previsto.

Se utilizzi Expressplay, allega i valori del livello di protezione dell&#39;output al momento della generazione del token tramite i flag compressedDigitalAudioOPL, uncompressedDigitalAudioOPL, compressedDigitalVideoOPL, uncompressedDigitalVideoOPL e unknownOutputBehavior. Questi sono documentati in [PlayReady License Token Request](https://www.expressplay.com/developer/restapi/#playready-license-token-request)
