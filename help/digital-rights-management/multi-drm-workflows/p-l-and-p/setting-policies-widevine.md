---
title: Utilizzo dei criteri di protezione dell'output
description: Utilizzo dei criteri di protezione dell'output
copied-description: true
exl-id: d91c9181-a6b2-4982-a3ba-57c4b56428eb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---

# Utilizzo dei criteri di protezione dell&#39;output{#using-output-protection-policies}

**Criteri di protezione dell&#39;output widevine**

Widevine supporta in modo nativo restrizioni di protezione dell&#39;uscita sia analogica che digitale. Per informazioni su come allegare questi criteri alle licenze generate, consultare la documentazione del provider di servizi Widevine.

Se si utilizza Expressplay come provider di servizi Widevine, allegare i criteri di protezione dell&#39;output digitale al momento della generazione del token tramite il flag hdcpOutputControl: i valori consentiti sono 0, 1, 2 dove 0 = HDCP_NONE, 1 = HDCP_V1, 2 = HDCP_V2. Sia HDCP_V1 che HDCP_V2 impongono rispettivamente le versioni 1.X e 2.X di HDCP.

Expressplay attualmente non supporta il collegamento di restrizioni di output analogico

**Criteri di protezione dell&#39;output PlayReady**

PlayReady supporta inoltre in modalità nativa restrizioni di protezione dell&#39;output sia analogico che digitale. I valori del livello di protezione dell&#39;output che è possibile impostare. La pagina [Livelli di protezione dell&#39;output](https://msdn.microsoft.com/en-us/library/dn468831.aspx) documenta i valori che è possibile impostare e il comportamento previsto del cliente.

Se utilizzi Expressplay, allega i valori del livello di protezione dell’output al momento della generazione del token tramite compressedDigitalAudioOPL, uncompressedDigitalAudioOPL, compressedDigitalVideoOPL, uncompressedDigitalVideoOPL e il flag unknownOutputBehavior. Questi sono documentati all&#39;indirizzo [Richiesta token di licenza PlayReady](https://www.expressplay.com/developer/restapi/#playready-license-token-request)
