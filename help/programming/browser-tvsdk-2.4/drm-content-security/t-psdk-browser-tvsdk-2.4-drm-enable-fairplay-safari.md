---
description: È possibile abilitare FairPlay per Safari quando si lavora con Primetime DRM Cloud, con tecnologia ExpressPlay.
title: Abilita FairPlay per Safari HLS
exl-id: 761c7cb8-3068-44c9-8ceb-6411c509c0a7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# Abilita FairPlay per Safari HLS {#enable-fairplay-for-safari-hls}

È possibile abilitare FairPlay per Safari quando si lavora con Primetime DRM Cloud, con tecnologia ExpressPlay.

Assicurati di disporre dei seguenti elementi:

* App di esempio funzionante in grado di riprodurre video HLS.

   L’app di esempio deve essere in grado di riprodurre contenuti protetti da FairPlay con le licenze gestite tramite Primetime DRM con tecnologia ExpressPlay.
* Contenuto HLS di esempio (un manifesto M3U8) protetto da FairPlay.

Per utilizzare appieno le informazioni disponibili qui, scopri i flussi di lavoro Multi-DRM che iniziano con la sottosezione [Server di riferimento: Sample ExpressPlay Entitlement Server (SEES)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_multi_drm_workflows.pdf) nella guida Flussi di lavoro multi-DRM. Leggi innanzitutto la documentazione su come impostare l’adesione e il server chiave e le informazioni di seguito saranno molto più utili.
Sono necessari i seguenti elementi:

* Il tuo *produzione* Autenticatore del cliente da ExpressPlay
* La stessa chiave di contenuto e `iv` con cui il contenuto è stato confezionato.
* La posizione del certificato della chiave pubblica FairPlay.

Per modificare la tua app FairPlay / Safari:

1. Impostare la posizione del certificato di chiave pubblica FairPlay utilizzato nella richiesta del server di licenze FairPlay.

   Ad esempio:

   ```js
   var myServerCertificatePath = './my_fairplay.cer';
   ```

1. Eseguire una licenza FairPlay manuale *token* richiedere a ExpressPlay di ottenere un URL del token di licenza.

       Puoi completare questo passaggio in uno dei seguenti modi:
   
   * Utilizza il tuo programma di autenticazione cliente di produzione ExpressPlay.
   * Utilizza la stessa chiave di contenuto e `iv` in questa richiesta che è stata utilizzata per creare un pacchetto del contenuto da riprodurre.

      Esegui il comando seguente dalla shell e sostituisci l’autenticatore cliente ExpressPlay per ottenere l’URL del token di licenza per il contenuto di esempio:

      ```
      curl -v "https://fp-gen.service.expressplay.com/hms/fp/token? 
           customerAuthenticator=<ExpressPlay customer authenticator identifier>& 
           errorFormat=json& 
           contentKey=<your content key>& 
           iv=<your iv here>"
      ```

      La risposta con l’URL del token di licenza sarà simile alla seguente:

      ```
      https://fp.service.expressplay.com:80/hms/fp/rights/? 
           ExpressPlayToken=<base64-encoded ExpressPlay token>
      ```

1. Imposta una variabile con l’URL del token di licenza da ExpressPlay.

   Ad esempio:

   ```js
   var myServerProcessSPCPath = 'https://fp.service.expressplay.com:80/hms/fp/rights/? 
        ExpressPlayToken=<base64-encoded ExpressPlay token>';
   ```

1. Prima che l&#39;app possa riprodurre contenuto protetto, modifica lo schema URL del contenuto da `skd://` a `https://`.

   È necessario aggiungere questa modifica allo schema URL nell’app, prima della chiamata al server licenze che consente la riproduzione.

   I protocolli devono essere modificati perché l’ID contenuto, che fornisce l’accesso alla chiave del contenuto nel sistema di gestione delle chiavi, è incluso nel manifesto M3U8 con `skd://` protocollo. Quando il lettore è pronto per ottenere la licenza per riprodurre il contenuto protetto, deve prima cambiare i protocolli per comunicare con il server licenze ExpressPlay. Nell’esempio seguente, il `myServerProcessSPCPath` è stato modificato per contenere lo schema URL corretto per la richiesta del server licenze:

   ```js
   extractContentId(initData) {  
       contentId = arrayToString(initData); // contentId is passed up as a URI,  
                                            // from which the host must be extracted:  
       var link = document.createElement('a');  
       link.href = contentId;  
       var index = contentId.indexOf(':');  
       myServerProcessSPCPath = "https:" + contentId.substring(index+1);  
       console.log("severProcessSPCPAth = " + serverProcessSPCPath); return link.hostname;  
   }
   ```
