---
description: Potete abilitare FairPlay per Safari quando lavorate con Primetime DRM Cloud, basato su ExpressPlay.
seo-description: Potete abilitare FairPlay per Safari quando lavorate con Primetime DRM Cloud, basato su ExpressPlay.
seo-title: Abilita FairPlay per Safari HLS
title: Abilita FairPlay per Safari HLS
uuid: 6a250a31-cc4b-4c4b-b1e9-893ee3ca5d78
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---


# Abilita FairPlay per Safari HLS {#enable-fairplay-for-safari-hls}

Potete abilitare FairPlay per Safari quando lavorate con Primetime DRM Cloud, basato su ExpressPlay.

Verificate di disporre dei seguenti elementi:

* Un&#39;app di esempio funzionante in grado di riprodurre video HLS.

   L&#39;app di esempio deve essere in grado di riprodurre contenuto protetto FairPlay con le licenze gestite tramite Primetime DRM fornito da ExpressPlay.
* Contenuto HLS di esempio (un manifesto M3U8) con protezione FairPlay.

Per utilizzare appieno le informazioni qui, scopri ulteriori informazioni sui flussi di lavoro DRM a partire dalla sottosezione [Server di riferimento: Esempio di ExpressPlay Entitlement Server (SEES)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_multi_drm_workflows.pdf) nella guida Flussi di lavoro multi-DRM. Leggete prima la documentazione su come impostare l&#39;adesione e il server chiave, e le informazioni riportate di seguito saranno molto più utili.
Sono necessari i seguenti elementi:

* Autenticatore *produzione* del cliente da ExpressPlay
* La stessa chiave di contenuto e `iv` con cui è stato creato il pacchetto del contenuto.
* Posizione del certificato della chiave pubblica FairPlay.

Per modificare l&#39;app FairPlay/Safari:

1. Imposta il percorso del certificato di chiave pubblica FairPlay utilizzato nella richiesta del server di licenze FairPlay.

   Ad esempio:

   ```js
   var myServerCertificatePath = './my_fairplay.cer';
   ```

1. Eseguite una richiesta manuale di licenza FairPlay *token* per ExpressPlay per ottenere un URL token di licenza.

       Puoi completare questo passaggio in uno dei modi seguenti:
   
   * Utilizza il tuo servizio di autenticazione clienti ExpressPlay Production.
   * Utilizzate in questa richiesta la stessa chiave di contenuto e `iv` utilizzata per creare pacchetti per il contenuto da riprodurre.

      Eseguite il comando seguente dalla shell e sostituite l&#39;autenticatore cliente ExpressPlay per ottenere l&#39;URL del token di licenza per il contenuto di esempio:

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

1. Impostate una variabile con l&#39;URL del token di licenza da ExpressPlay.

   Ad esempio:

   ```js
   var myServerProcessSPCPath = 'https://fp.service.expressplay.com:80/hms/fp/rights/? 
        ExpressPlayToken=<base64-encoded ExpressPlay token>';
   ```

1. Prima che l&#39;app possa riprodurre contenuto protetto, modificate lo schema URL per il contenuto da `skd://` a `https://`.

   È necessario aggiungere questa modifica allo schema URL nell&#39;app prima della chiamata al server delle licenze che consente la riproduzione.

   I protocolli devono essere modificati perché l&#39;ID contenuto, che fornisce l&#39;accesso alla chiave di contenuto nel sistema di gestione delle chiavi, viene incluso nel manifesto M3U8 con il protocollo `skd://`. Quando il lettore è pronto a ottenere la licenza per riprodurre il contenuto protetto, deve prima cambiare i protocolli per comunicare con il server licenze ExpressPlay. Nell&#39;esempio seguente, il `myServerProcessSPCPath` viene modificato in modo da contenere lo schema URL corretto per la richiesta del server licenze:

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

