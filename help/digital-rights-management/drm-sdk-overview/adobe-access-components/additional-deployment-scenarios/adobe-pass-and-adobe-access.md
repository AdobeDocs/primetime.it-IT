---
title: Autenticazione di Adobe Primetime e Adobe Primetime DRM
description: Autenticazione di Adobe Primetime e Adobe Primetime DRM
copied-description: true
exl-id: 7239be8b-9725-48b6-a4e2-8d13461f297d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---

# Autenticazione di Adobe Primetime e Adobe Primetime DRM {#adobe-primetime-authentication-and-adobe-primetime-drm}

Autenticazione Adobe Primetime ( [https://www.adobe.com/products/adobepass/](https://www.adobe.com/products/adobepass/)) fornisce l&#39;autenticazione e l&#39;autorizzazione utente/dispositivo tra più provider di contenuti. L&#39;utente deve disporre di un abbonamento TV via cavo o satellitare valido.

<!--<a id="fig_cln_bc2_44"></a>-->

![](assets/AdobePass_web.png)

L’autenticazione Adobe Primetime può essere utilizzata insieme a Adobe Primetime DRM per proteggere il contenuto multimediale. In questo scenario, il lettore video (SWF) può caricare un altro SWF denominato *Access Enabler*, ospitato da Adobe Systems. Il *Access Enabler* viene utilizzato per connettersi al servizio di autenticazione di Adobe Primetime e facilitare l’integrazione di SSO SAML con i sistemi del provider di identità MVPD (Multichannel Video Programming Distributor). Questo comporta il reindirizzamento del browser dell’utente brevemente alla pagina di accesso MVPD, la persistenza di un token AuthN e infine il ritorno al sito web dei contenuti con una sessione AuthN memorizzata nella cache.

Il *Access Enabler* può quindi facilitare le autorizzazioni back-end tra il servizio di autenticazione di Adobe Primetime e MVPD. MVPD mantiene la logica di business e determina il contenuto a cui l’utente ha diritto. L’adesione viene mantenuta in un token AuthZ aggiuntivo per tale risorsa di contenuto e inviata nuovamente al client.

I token di autenticazione e autorizzazione vengono firmati utilizzando l’ID univoco e la chiave privata del client DRM Primetime per evitare manomissioni o spoofing. Questo token è accessibile solo tramite *Access Enabler*.

Il lettore video può attivare il processo chiamando `getAuthorization` il *Access Enabler*. Se sono presenti token AuthN/AuthZ validi, il *AccessEnabler* invia al lettore video un callback che includerà un token multimediale di breve durata per la riproduzione del contenuto video.

L’autenticazione Adobe Primetime fornisce una libreria Java di convalida del token multimediale che può essere distribuita su un server. Quando si utilizza il server DRM Primetime per la protezione dei contenuti, è possibile integrare la convalida dei token multimediali con un plug-in lato server DRM Primetime per rilasciare automaticamente una licenza generica dopo aver convalidato correttamente il token multimediale. Il contenuto viene quindi inviato in streaming dai server CDN al client. Per acquisire una licenza di contenuto, il token multimediale di breve durata può essere inviato al server DRM di Primetime, dove la validità del token viene verificata e può essere rilasciata una licenza.

Il token AuthN di lunga durata viene utilizzato in genere dal *Access Enabler* in tutti gli sviluppatori di contenuti per rappresentare l’AuthN per tale abbonato MVPD. Inoltre, il server DRM di Primetime e il Token Verifier possono essere gestiti dalla rete CDN o da un provider di servizi per conto del provider di contenuti.
