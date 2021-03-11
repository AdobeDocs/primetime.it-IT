---
description: Il Flash Runtime TVSDK necessita di un token firmato per verificare di avere il diritto di chiamare l'API TVSDK sul dominio in cui risiede l'applicazione.
title: Carica il token firmato
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---


# Carica il token firmato {#load-your-signed-token}

Il Flash Runtime TVSDK necessita di un token firmato per verificare di avere il diritto di chiamare l&#39;API TVSDK sul dominio in cui risiede l&#39;applicazione.

1. Ottieni un token firmato dal tuo rappresentante di Adobe per ciascuno dei tuoi domini (dove ogni dominio potrebbe essere un dominio specifico o un dominio con caratteri jolly).

       Per ottenere un token, fornisci un Adobe con il dominio in cui l’applicazione verrà memorizzata o caricata oppure, preferibilmente, con il dominio come hash SHA256. In cambio, Adobe fornisce un token firmato per ciascun dominio. Questi token assumono una delle seguenti forme:
   
   * Un file [!DNL .xml] che funge da token per un singolo dominio o dominio con caratteri jolly.

      >[!NOTE]
      >
      >Un token per un dominio con caratteri jolly copre tale dominio e tutti i relativi sottodomini. Ad esempio, un token jolly per il dominio [!DNL mycompany.com] includerebbe anche [!DNL vids.mycompany.com] e [!DNL private.vids.mycompany.com]; un token carattere jolly per [!DNL vids.mycompany.com] copre anche [!DNL private.vids.mycompany.com]. *I token di dominio jolly sono supportati solo per alcune versioni di Flash Player.*

   * Un file [!DNL .swf] contenente informazioni token per più domini (esclusi i caratteri jolly) (singolo o jolly), che l’applicazione può caricare dinamicamente.

1. Memorizza il file token nella stessa posizione o dominio dell&#39;applicazione.

   Per impostazione predefinita, TVSDK cerca il token in questa posizione. In alternativa, puoi specificare il nome e la posizione del token in `flash_vars` nel file HTML.
1. Se il file token è un singolo file XML:
   1. Utilizza `utils.AuthorizedFeaturesHelper.loadFrom` per scaricare i dati memorizzati nell&#39;URL specificato (il file token) ed estrarre le informazioni `authorizedFeatures` da esso.

      Questo passaggio può variare. Ad esempio, potrebbe essere utile eseguire l’autenticazione prima di avviare l’applicazione oppure ricevere il token direttamente dal sistema di gestione dei contenuti (CMS).

   1. TVSDK invia un evento `COMPLETED` se il caricamento ha esito positivo o un evento `FAILED` in caso contrario. Esegui le azioni appropriate quando rilevi uno degli eventi.

      L&#39;applicazione deve riuscire a fornire gli oggetti `authorizedFeatures` richiesti a TVSDK sotto forma di `MediaPlayerContext`.
   Questo esempio mostra come utilizzare un file [!DNL .xml] a token singolo.

   ```
   private function loadDirectTokenURL():void { 
       var url:String = constructAuthorizedFeatureTokenURL(); 
       _logger.debug("#onApplicationComplete Loading token from [{0}].", url); 
       _authorizedFeatureHelper = new AuthorizedFeaturesHelper(); 
       _authorizedFeatureHelper.addEventListener(Event.COMPLETE,  
           onFeatureComplete); 
       _authorizedFeatureHelper.addEventListener(ErrorEvent.ERROR,  
           onFeatureError); 
        _authorizedFeatureHelper.loadFrom(url); 
    }
   ```

1. Se il token è un file [!DNL .swf]:
   1. Definire una classe `Loader` per caricare dinamicamente il file [!DNL .swf].
   1. Imposta il `LoaderContext` per specificare il caricamento da includere nel dominio dell&#39;applicazione corrente, che consente a TVSDK di scegliere il token corretto all&#39;interno del file [!DNL .swf]. Se `LoaderContext` non è specificato, l&#39;azione predefinita di `Loader.load` consiste nel caricare il file .swf nel dominio figlio del dominio corrente.
   1. Ascolta l’evento COMPLETE, che TVSDK invia se il caricamento ha esito positivo.

      Inoltre, ascolta l&#39;evento ERROR e adotta le azioni appropriate.
   1. Se il caricamento ha esito positivo, utilizza `AuthorizedFeaturesHelper` per ottenere un `ByteArray` contenente i dati di sicurezza codificati PCKS-7.

      Questi dati vengono utilizzati tramite l&#39;API AVE V11 per ottenere il riconoscimento dell&#39;autorizzazione da Flash Runtime Player. Se l&#39;array di byte non ha contenuto, utilizzare la procedura per cercare un file di token a dominio singolo.
   1. Utilizzare `AuthorizedFeatureHelper.loadFeatureFromData` per ottenere i dati richiesti dall&#39;array di byte.
   1. Scaricare il file [!DNL .swf].

   Gli esempi seguenti mostrano come utilizzare un file [!DNL .swf] con più token.

   **Esempio 1 con più token:**

   ```
   private function onApplicationComplete(event:FlexEvent):void { 
       var url:String = constructAuthorizedFeatureTokenURLFromSwf();   
       _loader = new Loader(); 
       var swfUrl:URLRequest = new URLRequest(url); 
       var loaderContext:LoaderContext =  
           new LoaderContext(false, ApplicationDomain.currentDomain, null); 
       _loader.contentLoaderInfo.addEventListener(Event.COMPLETE,  
           modEventHandler); 
       _loader.contentLoaderInfo.addEventListener(IOErrorEvent.IO_ERROR,  
           errEventHandler); 
       _loader.contentLoaderInfo.addEventListener(ProgressEvent.PROGRESS,  
           onProgressHandler); 
       _loader.uncaughtErrorEvents.addEventListener(UncaughtErrorEvent. 
           UNCAUGHT_ERROR, uncaughtEventHandler); 
       _logger.debug("# Loading token swf with context from [{0}].", url); 
       _loader.load(swfUrl, loaderContext); 
   } 
   
   private function modEventHandler(e:Event):void { 
       _logger.debug("loadSWF with domainID {0}",  
       SecurityDomain.currentDomain.domainID); 
       var loader : Loader = e.currentTarget.loader as Loader; 
       var myAuthorizedTokensLoaderClass:Class =  
           loader.contentLoaderInfo.applicationDomain. 
           getDefinition("AuthorizedTokensLoader") as Class; 
       var myTokens:Object = new myAuthorizedTokensLoaderClass(); 
       _authorizedFeatureHelper = new AuthorizedFeaturesHelper(); 
       _authorizedFeatureHelper.addEventListener(Event.COMPLETE, onFeatureComplete); 
       _authorizedFeatureHelper.addEventListener(ErrorEvent.ERROR, onFeatureError); 
       var byteArray:ByteArray = myTokens. 
           FetchToken(SecurityDomain.currentDomain.domainID); 
       if (myTokens == null || byteArray == null || byteArray.length == 0) 
           loadDirectTokenURL(); 
       else { 
           _logger.debug("token bytearry size {0}", byteArray.length); 
           _authorizedFeatureHelper.loadFeatureFromData(byteArray); 
       } 
       _loader.unload(); 
   } 
   ```

   **Esempio 2 con più token:**

   ```
   private function tokenSwfLoadedHandler(e:Event):void { 
       trace("loadSWF with domainID {0}", SecurityDomain.currentDomain.domainID); 
       var loader : Loader = e.currentTarget.loader as Loader; 
       var myAuthorizedTokensLoaderClass:Class =  
         loader.contentLoaderInfo.applicationDomain. 
         getDefinition("AuthorizedTokensLoader") as Class; 
       var myTokens:Object = new myAuthorizedTokensLoaderClass(); 
       authorizedFeatureHelper = new AuthorizedFeaturesHelper(); 
       authorizedFeatureHelper.addEventListener(Event.COMPLETE, onFeatureComplete); 
       authorizedFeatureHelper.addEventListener(ErrorEvent.ERROR, onFeatureError); 
       var byteArray:ByteArray =  
           myTokens.FetchToken(SecurityDomain.currentDomain.domainID); 
       var myDomains:Array = ["domain.com"]; 
       if (byteArray == null || byteArray.length == 0) { 
           // check for wildcard tokens 
           if (myTokens.hasOwnProperty("FetchWildCardToken") == true) { 
               // contains wildcard domains 
               for each (var domain:String in myDomains) { 
                   byteArray = myTokens.FetchWildCardToken(domain); 
                   if (byteArray != null && byteArray.length != 0) { 
                       break; 
                   } 
               }; 
           } 
       } 
   
       if (myTokens == null || byteArray == null || byteArray.length == 0) 
           loadDirectTokenURL(); 
       else { 
           trace("token bytearry size {0}", byteArray.length); 
           authorizedFeatureHelper.loadFeatureFromData(byteArray); 
       } 
       _loader.unload(); 
   } 
   
   private function loadDirectTokenURL():void { 
       trace("#onApplicationComplete Loading token from [{0}].", tokenUrl); 
       authorizedFeatureHelper = new AuthorizedFeaturesHelper(); 
       authorizedFeatureHelper.addEventListener(Event.COMPLETE, onFeatureComplete); 
       authorizedFeatureHelper.addEventListener(ErrorEvent.ERROR, onFeatureError); 
       authorizedFeatureHelper.loadFrom(tokenUrl); 
   }
   ```

