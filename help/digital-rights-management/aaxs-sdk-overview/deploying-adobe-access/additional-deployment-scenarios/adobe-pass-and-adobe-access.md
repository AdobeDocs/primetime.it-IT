---
title: Accesso ad Adobe Pass e Adobe
description: Accesso ad Adobe Pass e Adobe
copied-description: true
exl-id: b9a90297-da24-416f-91de-6a31322f35fb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# Accesso ad Adobe Pass e Adobe {#adobe-pass-and-adobe-access}

ADOBE PASS ( [](https://www.adobe.com/products/adobepass/)) fornisce l&#39;autenticazione e l&#39;autorizzazione utente/dispositivo tra più provider di contenuti. L&#39;utente deve disporre di un abbonamento TV via cavo o satellitare valido.

<!--<a id="fig_cln_bc2_44"></a>-->

![](assets/AdobePass_web.png)

Adobe Pass può essere utilizzato insieme ad Adobe Access per proteggere il contenuto multimediale. In questo scenario, il lettore video (SWF) può caricare un altro SWF denominato *Access Enabler*, ospitato da Adobe Systems. Il *Access Enabler* viene utilizzato per connettersi al servizio Adobe Pass e facilitare l&#39;integrazione di SSO SAML con i sistemi provider di identità MVPD (Multichannel Video Programming Distributor). Questo comporta il reindirizzamento del browser dell’utente brevemente alla pagina di accesso MVPD, la persistenza di un token AuthN e infine il ritorno al sito web dei contenuti con una sessione AuthN memorizzata nella cache.

Il *Access Enabler* può quindi facilitare le autorizzazioni back-end tra il servizio Adobe Pass e MVPD. MVPD mantiene la logica di business e determina il contenuto a cui l’utente ha diritto. L’adesione viene mantenuta in un token AuthZ aggiuntivo per tale risorsa di contenuto e inviata nuovamente al client.

I token di autenticazione e autorizzazione vengono firmati utilizzando l’ID univoco e la chiave privata del client Adobe Access per evitare manomissioni o spoofing. Questo token è accessibile solo tramite *Access Enabler*.

Il lettore video può attivare il processo chiamando `getAuthorization` il *Access Enabler*. Se sono presenti token AuthN/AuthZ validi, il *AccessEnabler* invia al lettore video un callback che includerà un token multimediale di breve durata per la riproduzione del contenuto video.

Adobe Pass fornisce una libreria Java di convalida del token multimediale che può essere distribuita su un server. Quando si utilizza il server Accesso Flass per la protezione dei contenuti, è possibile integrare la convalida del token multimediale con un plug-in lato server di Accesso Adobe per rilasciare automaticamente una licenza generica dopo aver convalidato correttamente il token multimediale. Il contenuto viene quindi inviato in streaming dai server CDN al client. Per acquisire una licenza per contenuti, il token multimediale di breve durata può essere inviato al server di accesso Adobe, dove la validità del token viene verificata ed è possibile rilasciare una licenza.

Il token AuthN di lunga durata viene utilizzato in genere dal *Access Enabler* in tutti gli sviluppatori di contenuti per rappresentare l’AuthN per tale abbonato MVPD. Inoltre, Adobe Access Server e Token Verifier possono essere gestiti dalla CDN o da un fornitore di servizi per conto del fornitore di contenuti.
