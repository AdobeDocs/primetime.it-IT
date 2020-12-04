---
description: Il Flash Runtime TVSDK necessita di un token firmato per verificare di avere il diritto di chiamare l'API TVSDK sul dominio in cui risiede l'applicazione.
seo-description: Il Flash Runtime TVSDK necessita di un token firmato per verificare di avere il diritto di chiamare l'API TVSDK sul dominio in cui risiede l'applicazione.
seo-title: Carica il token firmato
title: Carica il token firmato
uuid: 8760eab3-3d6d-47c6-9aa7-f64f6aa5ddcf
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---


# Carica il token firmato {#load-your-signed-token}

Il Flash Runtime TVSDK necessita di un token firmato per verificare di avere il diritto di chiamare l&#39;API TVSDK sul dominio in cui risiede l&#39;applicazione.

1. Ottenete un token firmato dal rappresentante del Adobe  per ciascuno dei vostri domini (dove ogni dominio potrebbe essere un dominio specifico o un dominio con caratteri jolly).

       Per ottenere un token, fornite  Adobe con il dominio in cui verrà memorizzata o caricata l&#39;applicazione oppure, preferibilmente, il dominio come hash SHA256. In cambio,  Adobe fornisce un token firmato per ciascun dominio. Questi token hanno una delle seguenti forme:
   
   * Un file [!DNL .xml] che funge da token per un dominio singolo o un dominio con caratteri jolly.

      >[!NOTE]
      >
      >Un token per un dominio con caratteri jolly copre tale dominio e tutti i relativi sottodomini. Ad esempio, un token carattere jolly per il dominio [!DNL mycompany.com] includerebbe anche [!DNL vids.mycompany.com] e [!DNL private.vids.mycompany.com]; un token carattere jolly per [!DNL vids.mycompany.com] coprirebbe anche [!DNL private.vids.mycompany.com]. *I token di dominio jolly sono supportati solo per alcune versioni di Flash Player.*

   * Un file [!DNL .swf] contenente informazioni di token per più domini (esclusi i caratteri jolly) (singoli o caratteri jolly), che l&#39;applicazione può caricare dinamicamente.

1. Archiviate il file di token nello stesso percorso o dominio dell&#39;applicazione.

   Per impostazione predefinita, TVSDK cerca il token in questa posizione. In alternativa, potete specificare il nome e la posizione del token in `flash_vars` nel file HTML.
1. Se il file token è un singolo file XML:
   1. Utilizzare `utils.AuthorizedFeaturesHelper.loadFrom` per scaricare i dati memorizzati nell&#39;URL specificato (il file del token) ed estrarre le informazioni `authorizedFeatures` da esso.

      Questo passaggio può variare. Ad esempio, potrebbe essere necessario eseguire l&#39;autenticazione prima di avviare l&#39;applicazione, oppure ricevere il token direttamente dal sistema di gestione dei contenuti (CMS).

   1. TVSDK invia un evento `COMPLETED` se il caricamento ha esito positivo o un evento `FAILED` in caso contrario. Eseguite le azioni appropriate quando rilevate entrambi gli eventi.

      Per consentire all&#39;applicazione di fornire gli oggetti `authorizedFeatures` richiesti a TVSDK sotto forma di `MediaPlayerContext`, questo deve essere eseguito correttamente.
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
   1. Definire una classe `Loader` per caricare in modo dinamico il file [!DNL .swf].
   1. Impostate `LoaderContext` per specificare il caricamento nel dominio applicazione corrente, in modo che TVSDK possa scegliere il token corretto all&#39;interno del file [!DNL .swf]. Se `LoaderContext` non è specificato, l&#39;azione predefinita di `Loader.load` consiste nel caricare il file .swf nel dominio figlio del dominio corrente.
   1. Ascoltare l’evento COMPLETE, che TVSDK invia se il caricamento ha esito positivo.

      Inoltre, ascoltare l&#39;evento ERROR e intervenire in modo appropriato.
   1. Se il caricamento ha esito positivo, utilizzare il simbolo `AuthorizedFeaturesHelper` per ottenere un elemento `ByteArray` contenente i dati di sicurezza codificati PCKS-7.

      Questi dati vengono utilizzati tramite l&#39;API AVE V11 per ottenere il riconoscimento dell&#39;autorizzazione da parte del lettore runtime di Flash. Se l&#39;array di byte non ha contenuto, utilizzare la procedura per cercare un file di token a dominio singolo.
   1. Utilizzare `AuthorizedFeatureHelper.loadFeatureFromData` per ottenere i dati richiesti dall&#39;array di byte.
   1. Scaricate il file [!DNL .swf].

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

