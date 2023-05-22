---
description: Il TVSDK di Flash Runtime richiede un token firmato per verificare di disporre dei diritti per chiamare l’API TVSDK sul dominio in cui risiede l’applicazione.
title: Carica il token firmato
exl-id: fef6b764-dc65-412e-a990-3f0b1fef94dd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# Carica il token firmato {#load-your-signed-token}

Il TVSDK di Flash Runtime richiede un token firmato per verificare di disporre dei diritti per chiamare l’API TVSDK sul dominio in cui risiede l’applicazione.

1. Ottieni un token firmato dal rappresentante dell’Adobe per ciascuno dei tuoi domini (dove ogni dominio potrebbe essere un dominio specifico o un dominio con caratteri jolly).

       Per ottenere un token, fornisci un Adobe con il dominio in cui verrà archiviata o caricata l’applicazione o, preferibilmente, con il dominio come hash SHA256. In cambio, Adobe ti fornisce un token firmato per ciascun dominio. Questi token possono assumere una delle seguenti forme:
   
   * Un [!DNL .xml] file che funge da token per un singolo dominio o dominio jolly.

      >[!NOTE]
      >
      >Un token per un dominio con caratteri jolly copre tale dominio e tutti i relativi sottodomini. Ad esempio, un token jolly per il dominio [!DNL mycompany.com] coprirebbe anche [!DNL vids.mycompany.com] e [!DNL private.vids.mycompany.com]; un token jolly per [!DNL vids.mycompany.com] coprirebbe anche [!DNL private.vids.mycompany.com]. *I token di dominio con caratteri jolly sono supportati solo per determinate versioni del Flash Player.*

   * A [!DNL .swf] file contenente informazioni sui token per più domini (esclusi i caratteri jolly) (singolo o jolly), che l’applicazione può caricare in modo dinamico.

1. Memorizza il file token nella stessa posizione o nello stesso dominio dell’applicazione.

   Per impostazione predefinita, TVSDK cerca il token in questa posizione. In alternativa, puoi specificare il nome e la posizione del token in `flash_vars` nel file HTML.
1. Se il file token è un singolo file XML:
   1. Utilizzare `utils.AuthorizedFeaturesHelper.loadFrom` per scaricare i dati memorizzati nell’URL specificato (il file token) ed estrarre il `authorizedFeatures` informazioni.

      Questo passaggio può variare. Ad esempio, potrebbe essere utile eseguire l’autenticazione prima di avviare l’applicazione oppure ricevere il token direttamente dal sistema di gestione dei contenuti (CMS).

   1. TVSDK invia `COMPLETED` evento se il caricamento ha esito positivo o un `FAILED` in caso contrario. Agisci in modo appropriato quando rilevi uno di questi eventi.

      Affinché l&#39;applicazione fornisca il necessario `authorizedFeatures` oggetti a TVSDK sotto forma di `MediaPlayerContext`.
   Questo esempio mostra come utilizzare un token singolo [!DNL .xml] file.

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

1. Se il token è un [!DNL .swf] file:
   1. Definisci un `Loader` classe per caricare dinamicamente il [!DNL .swf] file.
   1. Imposta il `LoaderContext` per specificare il caricamento nel dominio dell&#39;applicazione corrente, che consente a TVSDK di scegliere il token corretto all&#39;interno [!DNL .swf] file. Se `LoaderContext` non è specificato, l&#39;azione predefinita di `Loader.load` : per caricare il file con estensione swf nel dominio figlio del dominio corrente.
   1. Ascolta l’evento COMPLETE, che TVSDK invia se il caricamento ha esito positivo.

      Ascolta anche l’evento ERROR e apporta le correzioni necessarie.
   1. Se il caricamento ha esito positivo, utilizza `AuthorizedFeaturesHelper` per ottenere un `ByteArray` che contiene i dati di sicurezza con codifica PCKS-7.

      Questi dati vengono utilizzati tramite l’API AVE V11 per ottenere la conferma dell’autorizzazione dal lettore runtime di Flash. Se la matrice di byte non ha contenuto, utilizzare la procedura per cercare un file di token a dominio singolo.
   1. Utilizzare `AuthorizedFeatureHelper.loadFeatureFromData` per ottenere i dati richiesti dalla matrice di byte.
   1. Scarica il file [!DNL .swf] file.

   Gli esempi seguenti mostrano come utilizzare un token multiplo [!DNL .swf] file.

   **Esempio di token multipli 1:**

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

   **Esempio 2 di token multipli:**

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
