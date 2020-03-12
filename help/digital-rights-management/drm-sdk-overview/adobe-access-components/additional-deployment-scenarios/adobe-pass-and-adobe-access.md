---
seo-title: Autenticazione Adobe Primetime e Adobe Primetime DRM
title: Autenticazione Adobe Primetime e Adobe Primetime DRM
uuid: 44fe3956-efb5-4fc5-97e2-37abb6554322
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# Autenticazione Adobe Primetime e Adobe Primetime DRM {#adobe-primetime-authentication-and-adobe-primetime-drm}

L&#39;autenticazione Adobe Primetime ( [https://www.adobe.com/products/adobepass/](https://www.adobe.com/products/adobepass/)) fornisce l&#39;autenticazione utente/dispositivo e l&#39;autorizzazione per più fornitori di contenuti. L&#39;utente deve disporre di un&#39;iscrizione TV via cavo o satellitare valida.

<!--<a id="fig_cln_bc2_44"></a>-->

![](assets/AdobePass_web.png)

L&#39;autenticazione Adobe Primetime può essere utilizzata insieme ad Adobe Primetime DRM per proteggere il contenuto multimediale. In questo scenario, il lettore video (SWF) può caricare un altro file SWF denominato *Access Enabler*, ospitato da Adobe Systems. L&#39; *Access Enabler* viene utilizzato per connettersi al servizio di autenticazione Adobe Primetime e facilitare l&#39;integrazione SSO SAML con i sistemi provider di identità MVPD (Multicanale Video Programming Distributor). Ciò comporta il reindirizzamento breve del browser dell&#39;utente alla pagina di accesso MVPD, la persistenza di un token AuthN e infine il ritorno al sito Web del contenuto con una sessione AuthN nella cache.

L&#39; *utilità di abilitazione* di accesso può quindi facilitare le autorizzazioni di back-end tra il servizio di autenticazione Adobe Primetime e l&#39;MVPD. L&#39;MVPD mantiene la logica di business e determina a quale contenuto l&#39;utente ha diritto. L&#39;adesione è persistente in un token AuthZ aggiuntivo per la risorsa di contenuto e viene restituita al client.

I token di autenticazione e autorizzazione sono firmati utilizzando l&#39;ID univoco e la chiave privata del client DRM Primetime per evitare manomissioni o spoofing. È possibile accedere a questo token solo tramite *Access Enabler*.

Il lettore video può attivare il processo chiamando `getAuthorization` Access Enabler **. Se sono presenti token AuthN/AuthZ validi, *AccessEnabler* emette un callback al lettore video che includerà un token multimediale di breve durata per la riproduzione del contenuto video.

L&#39;autenticazione Adobe Primetime fornisce una libreria Java per la convalida dei token multimediali che può essere distribuita su un server. Quando utilizzate il server DRM di Primetime per la protezione dei contenuti, potete integrare la convalida del token multimediale con un plug-in server DRM di Primetime per rilasciare automaticamente una licenza generica dopo aver convalidato correttamente il token multimediale. Il contenuto viene quindi trasmesso in streaming dai server CDN al client. Per acquisire una licenza di contenuto, il token multimediale di breve durata può essere inviato al server DRM Primetime, dove viene verificata la validità del token e può essere rilasciata una licenza.

Il token AuthN di lunga durata viene generalmente utilizzato da *Access Enabler* in tutti gli sviluppatori di contenuti per rappresentare l&#39;AuthN per tale utente iscritto a MVPD. Inoltre, il server DRM Primetime e il verificatore token possono essere gestiti dal CDN o da un provider di servizi per conto del fornitore di contenuti.