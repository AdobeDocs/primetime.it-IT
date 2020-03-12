---
seo-title: Utilizzo dei criteri di protezione dell'output
title: Utilizzo dei criteri di protezione dell'output
uuid: f00d2a97-0036-41a6-ab44-391cc40b146e
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Utilizzo dei criteri di protezione dell&#39;output{#using-output-protection-policies}

**Criteri di protezione dell&#39;output di Widevine**

La tecnologia Widevine supporta in modo nativo sia le restrizioni di protezione dell&#39;uscita analogica che digitale. Per informazioni su come allegare tali criteri alle licenze generate, consulta la documentazione del provider di servizi Widevine.

Se utilizzate Expressplay come provider di servizi Widevine, allegate i criteri di protezione dell&#39;output digitale al momento della generazione del token tramite il flag hdcpOutputControl:
I valori consentiti sono 0, 1, 2 dove 0 = HDCP_NONE, 1 = HDCP_V1, 2 = HDCP_V2. HDCP_V1 e HDCP_V2 applicano rispettivamente le versioni HDCP 1.X e 2.X.

Expressplay attualmente non supporta l&#39;associazione di restrizioni all&#39;uscita analogica

**Criteri di protezione dell&#39;output di PlayReady**

PlayReady supporta inoltre in modo nativo le restrizioni di protezione dell&#39;uscita analogica e digitale. I valori del livello di protezione dell&#39;output che è possibile impostare. La pagina Livelli [di protezione dell&#39;](https://msdn.microsoft.com/en-us/library/dn468831.aspx) output documenta i valori che è possibile impostare e il comportamento previsto del cliente.

Se si utilizza Expressplay, allegare valori di livello di protezione dell&#39;output al momento della generazione del token tramite i formati compressoDigitalAudioOPL, non compressoDigitalAudioOPL, compressoDigitalVideoOPL, non compressoDigitalVideoOPL e il flag unknownOutputBehavior. Questi sono documentati in [PlayReady License Token Request](https://www.expressplay.com/developer/restapi/#playready-license-token-request)
