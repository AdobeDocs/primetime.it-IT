---
description: È possibile abilitare FairPlay per Safari quando si lavora con Primetime DRM Cloud, basato su ExpressPlay.
title: Abilita FairPlay per Safari HLS
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---


# Abilita FairPlay per Safari HLS {#enable-fairplay-for-safari-hls}

È possibile abilitare FairPlay per Safari quando si lavora con Primetime DRM Cloud, basato su ExpressPlay.

Assicurati di avere quanto segue:

* Un&#39;app di esempio funzionante in grado di riprodurre video HLS.

   L&#39;app di esempio deve essere in grado di riprodurre contenuti protetti da FairPlay con le licenze gestite tramite DRM di Primetime con tecnologia ExpressPlay.
* Contenuto HLS campione (un manifesto M3U8) imballato con protezione FairPlay.

Per sfruttare appieno le informazioni qui, scopri i flussi di lavoro Multi-DRM a partire dalla sottosezione [Server di riferimento: Esempio di ExpressPlay Entitlement Server (SEES)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_multi_drm_workflows.pdf) nella guida Flussi di lavoro multi-DRM. Per prima cosa, leggi la documentazione su come impostare l&#39;adesione e il server chiave e le informazioni riportate di seguito saranno molto più utili.
Sono necessari i seguenti elementi:

* Autenticatore *produzione* del cliente da ExpressPlay
* La stessa chiave di contenuto e `iv` con cui è stato compilato il pacchetto del contenuto.
* Posizione del certificato della chiave pubblica FairPlay.

Per modificare la tua app FairPlay / Safari:

1. Imposta la posizione del tuo certificato di chiave pubblica FairPlay che è stato utilizzato nella richiesta del server di licenza FairPlay.

   Ad esempio:

   ```js
   var myServerCertificatePath = './my_fairplay.cer';
   ```

1. Esegui una richiesta manuale di licenza FairPlay *token* a ExpressPlay per ottenere un URL del token di licenza.

       Puoi completare questo passaggio in uno dei seguenti modi:
   
   * Utilizza il tuo Authenticator per clienti di produzione ExpressPlay.
   * Utilizza la stessa chiave di contenuto e `iv` in questa richiesta utilizzata per creare un pacchetto del contenuto da riprodurre.

      Esegui il seguente comando dalla shell e sostituisci l’autenticatore del cliente ExpressPlay per ottenere l’URL del token di licenza per il contenuto di esempio:

      ```
      curl -v "https://fp-gen.service.expressplay.com/hms/fp/token? 
           customerAuthenticator=<ExpressPlay customer authenticator identifier>& 
           errorFormat=json& 
           contentKey=<your content key>& 
           iv=<your iv here>"
      ```

      La risposta con l’URL del token di licenza avrà un aspetto simile al seguente:

      ```
      https://fp.service.expressplay.com:80/hms/fp/rights/? 
           ExpressPlayToken=<base64-encoded ExpressPlay token>
      ```

1. Imposta una variabile con l&#39;URL del token di licenza da ExpressPlay.

   Ad esempio:

   ```js
   var myServerProcessSPCPath = 'https://fp.service.expressplay.com:80/hms/fp/rights/? 
        ExpressPlayToken=<base64-encoded ExpressPlay token>';
   ```

1. Prima che l’app possa riprodurre contenuto protetto, cambia lo schema URL per il contenuto da `skd://` a `https://`.

   È necessario aggiungere questa modifica allo schema URL nell&#39;app prima della chiamata al server licenze che consente la riproduzione.

   I protocolli devono essere modificati perché l’ID contenuto, che fornisce l’accesso alla chiave di contenuto nel sistema di gestione delle chiavi, viene inserito nel manifesto M3U8 con il protocollo `skd://` . Quando il lettore è pronto a ottenere la licenza per riprodurre i contenuti protetti, deve prima cambiare i protocolli per comunicare con il server licenze ExpressPlay. Nell’esempio seguente, il `myServerProcessSPCPath` viene modificato in modo da contenere lo schema URL corretto per la richiesta del server licenze:

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

