---
seo-title: Adobe Pass e Adobe Access
title: Adobe Pass e Adobe Access
uuid: 09e75cd7-00b3-4f0f-869e-43dc4d5c3bf7
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Adobe Pass e Adobe Access {#adobe-pass-and-adobe-access}

Adobe Pass ( [](https://www.adobe.com/products/adobepass/)) fornisce l&#39;autenticazione utente/dispositivo e l&#39;autorizzazione tra più fornitori di contenuti. L&#39;utente deve disporre di un&#39;iscrizione TV via cavo o satellitare valida.

<!--<a id="fig_cln_bc2_44"></a>-->

![](assets/AdobePass_web.png)

Adobe Pass può essere utilizzato insieme ad Adobe Access per proteggere i contenuti multimediali. In questo scenario, il lettore video (SWF) può caricare un altro file SWF denominato *Access Enabler*, ospitato da Adobe Systems. L&#39; *Access Enabler* viene utilizzato per connettersi al servizio Adobe Pass e per facilitare l&#39;integrazione SSO SAML con i sistemi provider di identità MVPD (Multicanale Video Programming Distributor). Ciò comporta il reindirizzamento breve del browser dell&#39;utente alla pagina di accesso MVPD, la persistenza di un token AuthN e infine il ritorno al sito Web del contenuto con una sessione AuthN nella cache.

L&#39;utilità *Access Enabler* può quindi facilitare le autorizzazioni di back-end tra il servizio Adobe Pass e l&#39;MVPD. L&#39;MVPD mantiene la logica di business e determina a quale contenuto l&#39;utente ha diritto. L&#39;adesione è persistente in un token AuthZ aggiuntivo per la risorsa di contenuto e viene restituita al client.

I token di autenticazione e autorizzazione sono firmati utilizzando l&#39;ID univoco e la chiave privata del client Adobe Access per evitare manomissioni o spoofing. È possibile accedere a questo token solo tramite *Access Enabler*.

Il lettore video può attivare il processo chiamando `getAuthorization` Access Enabler **. Se sono presenti token AuthN/AuthZ validi, *AccessEnabler* emette un callback al lettore video che includerà un token multimediale di breve durata per la riproduzione del contenuto video.

Adobe Pass fornisce una libreria Java per la convalida dei token multimediali che può essere distribuita su un server. Quando utilizzate il server Flash Access per la protezione dei contenuti, potete integrare la convalida del token multimediale con un plug-in lato server di Adobe Access per rilasciare automaticamente una licenza generica dopo aver convalidato correttamente il token multimediale. Il contenuto viene quindi trasmesso in streaming dai server CDN al client. Per acquisire una licenza di contenuto, il token multimediale di breve durata può essere inviato al server Adobe Access, dove viene verificata la validità del token e può essere rilasciata una licenza.

Il token AuthN di lunga durata viene generalmente utilizzato da *Access Enabler* in tutti gli sviluppatori di contenuti per rappresentare l&#39;AuthN per tale utente iscritto a MVPD. Inoltre, Adobe Access Server e Token Verifier possono essere gestiti dal CDN o da un provider di servizi per conto del fornitore di contenuti.
