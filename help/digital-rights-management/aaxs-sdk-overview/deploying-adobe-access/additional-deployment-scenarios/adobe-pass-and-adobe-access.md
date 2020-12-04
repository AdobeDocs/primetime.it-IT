---
seo-title: ' accesso a Adobe Pass e  Adobe'
title: ' accesso a Adobe Pass e  Adobe'
uuid: 09e75cd7-00b3-4f0f-869e-43dc4d5c3bf7
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---


#  accesso a Adobe Pass e  Adobe {#adobe-pass-and-adobe-access}

 Adobe Pass ( [](https://www.adobe.com/products/adobepass/)) fornisce l&#39;autenticazione utente/dispositivo e l&#39;autorizzazione tra più fornitori di contenuti. L&#39;utente deve disporre di un&#39;iscrizione TV via cavo o satellitare valida.

<!--<a id="fig_cln_bc2_44"></a>-->

![](assets/AdobePass_web.png)

 Adobe Pass può essere utilizzato insieme  accesso al Adobe per proteggere i contenuti multimediali. In questo scenario, il lettore video (SWF) può caricare un altro file SWF denominato *Access Enabler*, ospitato da  Adobe Systems. L&#39; *Access Enabler* viene utilizzato per connettersi al servizio Adobe Pass  e per facilitare l&#39;integrazione SSO SAML con i sistemi provider di identità MVPD (Multicanale Video Programming Distributor). Ciò comporta il reindirizzamento breve del browser dell&#39;utente alla pagina di accesso MVPD, la persistenza di un token AuthN e infine il ritorno al sito Web del contenuto con una sessione AuthN nella cache.

L&#39; *Access Enabler* può quindi facilitare le autorizzazioni di back-end tra  servizio Adobe Pass e MVPD. L&#39;MVPD mantiene la logica di business e determina a quale contenuto l&#39;utente ha diritto. L&#39;adesione è persistente in un token AuthZ aggiuntivo per la risorsa di contenuto e viene restituita al client.

I token di autenticazione e autorizzazione sono firmati utilizzando l&#39;ID univoco e la chiave privata del client di accesso al Adobe  per evitare manomissioni o spoofing. È possibile accedere a questo token solo tramite *Access Enabler*.

Il lettore video può attivare il processo chiamando `getAuthorization` in *Access Enabler*. Se sono presenti token AuthN/AuthZ validi, *AccessEnabler* esegue un callback al lettore video che includerà un token multimediale di breve durata per la riproduzione del contenuto video.

 Adobe Pass fornisce una libreria Java per la convalida dei token multimediali che può essere distribuita su un server. Quando utilizzate il server Flash Access per la protezione dei contenuti, potete integrare il validatore del token multimediale con un plug-in lato server di accesso  Adobe per rilasciare automaticamente una licenza generica dopo aver convalidato correttamente il token multimediale. Il contenuto viene quindi trasmesso in streaming dai server CDN al client. Per acquisire una licenza di contenuto, il token multimediale di breve durata può essere inviato al server di accesso al Adobe , dove viene verificata la validità del token e può essere rilasciata una licenza.

Il token AuthN a lunga vita è generalmente utilizzato da *Access Enabler* tra tutti gli sviluppatori di contenuti per rappresentare l&#39;AuthN per tale utente iscritto MVPD. Inoltre, Adobe Access Server e Token Verifier possono essere gestiti dal CDN o da un provider di servizi per conto del fornitore di contenuti.
