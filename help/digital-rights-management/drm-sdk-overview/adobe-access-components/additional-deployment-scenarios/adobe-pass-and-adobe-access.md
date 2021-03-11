---
title: Autenticazione Adobe Primetime e DRM Adobe Primetime
description: Autenticazione Adobe Primetime e DRM Adobe Primetime
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---


# Autenticazione Adobe Primetime e DRM Adobe Primetime {#adobe-primetime-authentication-and-adobe-primetime-drm}

L’autenticazione Adobe Primetime ( [https://www.adobe.com/products/adobepass/](https://www.adobe.com/products/adobepass/)) fornisce l’autenticazione e l’autorizzazione utente/dispositivo per più fornitori di contenuti. L&#39;utente deve disporre di un abbonamento TV via cavo o satellitare valido.

<!--<a id="fig_cln_bc2_44"></a>-->

![](assets/AdobePass_web.png)

L’autenticazione Adobe Primetime può essere utilizzata insieme a DRM di Adobe Primeitme per proteggere il contenuto multimediale. In questo scenario, il lettore video (SWF) può caricare un altro file SWF denominato *Access Enabler*, ospitato da Adobe Systems. Il *Access Enabler* viene utilizzato per connettersi al servizio di autenticazione Adobe Primetime e per facilitare l&#39;integrazione SSO SAML con i sistemi del provider di identità MVPD (Multichannel Video Programming Distributor). Ciò comporta il reindirizzamento breve del browser dell&#39;utente alla pagina di accesso MVPD, la persistenza di un token AuthN e infine il ritorno al sito Web del contenuto con una sessione AuthN nella cache.

Il *Access Enabler* può quindi facilitare le autorizzazioni di back-end tra il servizio di autenticazione Adobe Primetime e l&#39;MVPD. L&#39;MVPD mantiene la logica di business e determina a quale contenuto l&#39;utente ha diritto. L&#39;adesione viene mantenuta in un token AuthZ aggiuntivo per la risorsa di contenuto e inviata nuovamente al client.

I token di autenticazione e autorizzazione sono firmati utilizzando l’ID univoco e la chiave privata del client DRM di Primetime per evitare manomissioni o spoofing. Questo token è accessibile solo tramite l&#39; *Access Enabler*.

Il lettore video può attivare il processo richiamando `getAuthorization` su *Access Enabler*. Se sono presenti token AuthN/AuthZ validi, l&#39; *AccessEnabler* invia al lettore video un callback che includerà un token multimediale di breve durata per la riproduzione del contenuto video.

L’autenticazione Adobe Primetime fornisce una libreria Java di convalida dei token multimediali che può essere distribuita su un server. Quando utilizzi il server DRM di Primetime per la protezione dei contenuti, puoi integrare la convalida del token multimediale con un plug-in lato server DRM di Primetime per emettere automaticamente una licenza generica dopo aver convalidato correttamente il token multimediale. Il contenuto viene quindi inviato in streaming dai server CDN al client. Per acquisire una licenza di contenuto, il token multimediale di breve durata può essere inviato al server DRM di Primetime, dove la validità del token è verificata e può essere rilasciata una licenza.

Il token AuthN longevo viene generalmente utilizzato da *Access Enabler* tra tutti gli sviluppatori di contenuti per rappresentare l&#39;AuthN per l&#39;utente con sottoscrizione MVPD. Inoltre, il server DRM e il verificatore token di Primetime possono essere gestiti dalla rete CDN o da un fornitore di servizi per conto del fornitore di contenuti.