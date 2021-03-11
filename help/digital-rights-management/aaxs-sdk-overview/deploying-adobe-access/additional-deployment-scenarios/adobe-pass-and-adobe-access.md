---
title: Accesso ad Adobe Pass e Adobe
description: Accesso ad Adobe Pass e Adobe
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---


# Accesso ad Adobe Pass e Adobe {#adobe-pass-and-adobe-access}

Adobe Pass ( [](https://www.adobe.com/products/adobepass/)) fornisce autenticazione e autorizzazione utente/dispositivo per più provider di contenuti. L&#39;utente deve disporre di un abbonamento TV via cavo o satellitare valido.

<!--<a id="fig_cln_bc2_44"></a>-->

![](assets/AdobePass_web.png)

Adobe Pass può essere utilizzato insieme ad Adobe Access per proteggere i contenuti multimediali. In questo scenario, il lettore video (SWF) può caricare un altro file SWF denominato *Access Enabler*, ospitato da Adobe Systems. Il *Access Enabler* viene utilizzato per connettersi al servizio Adobe Pass e per facilitare l&#39;integrazione SSO SAML con i sistemi di provider di identità MVPD (Multichannel Video Programming Distributor). Ciò comporta il reindirizzamento breve del browser dell&#39;utente alla pagina di accesso MVPD, la persistenza di un token AuthN e infine il ritorno al sito Web del contenuto con una sessione AuthN nella cache.

Il *Access Enabler* può quindi facilitare le autorizzazioni di back-end tra il servizio Adobe Pass e l&#39;MVPD. L&#39;MVPD mantiene la logica di business e determina a quale contenuto l&#39;utente ha diritto. L&#39;adesione viene mantenuta in un token AuthZ aggiuntivo per la risorsa di contenuto e inviata nuovamente al client.

I token di autenticazione e autorizzazione sono firmati utilizzando l’ID univoco e la chiave privata del client Adobe Access per evitare manomissioni o spoofing. Questo token è accessibile solo tramite l&#39; *Access Enabler*.

Il lettore video può attivare il processo richiamando `getAuthorization` su *Access Enabler*. Se sono presenti token AuthN/AuthZ validi, l&#39; *AccessEnabler* invia al lettore video un callback che includerà un token multimediale di breve durata per la riproduzione del contenuto video.

Adobe Pass fornisce una libreria Java di convalida dei token multimediali che può essere distribuita su un server. Quando si utilizza il server Accesso Flash per la protezione dei contenuti, è possibile integrare la convalida del token multimediale con un plug-in lato server di Adobe Access per rilasciare automaticamente una licenza generica dopo aver convalidato correttamente il token multimediale. Il contenuto viene quindi inviato in streaming dai server CDN al client. Per acquisire una licenza di contenuto, il token multimediale di breve durata può essere inviato al server Adobe Access, dove viene verificata la validità del token e può essere rilasciata una licenza.

Il token AuthN longevo viene generalmente utilizzato da *Access Enabler* tra tutti gli sviluppatori di contenuti per rappresentare l&#39;AuthN per l&#39;utente con sottoscrizione MVPD. Inoltre, Adobe Access Server e Token Verifier possono essere gestiti dal CDN o da un fornitore di servizi per conto del fornitore di contenuti.
