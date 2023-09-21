---
description: È possibile utilizzare le funzioni del Digital Rights Management Primetime (DRM) per fornire un accesso sicuro al contenuto video. In alternativa, è possibile utilizzare soluzioni DRM di terze parti in alternativa alla soluzione DRM di Primetime integrata di Adobe.
title: Panoramica dell’interfaccia DRM di Primetime
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# Panoramica {#primetime-drm-interface-overview}

È possibile utilizzare le funzioni del Digital Rights Management Primetime (DRM) per fornire un accesso sicuro al contenuto video. In alternativa, è possibile utilizzare soluzioni DRM di terze parti in alternativa alla soluzione DRM di Primetime integrata di Adobe.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Per informazioni aggiornate sulla disponibilità di soluzioni DRM di terze parti, rivolgersi al proprio rappresentante di Adobe.

L&#39;elemento chiave lato client del sistema DRM (Digital Rights Management) di Primetime è DRM Manager. L&#39;applicazione di esempio inclusa nell&#39;SDK per Android include `DRMHelper` classe che illustra come semplificare l&#39;implementazione di determinate operazioni DRM.

Primetime DRM fornisce un flusso di lavoro scalabile ed efficiente per implementare la protezione dei contenuti nelle applicazioni TVSDK. Per proteggere e gestire i diritti dei contenuti video, crea una licenza per ciascun file multimediale digitale.

Consulta il codice del sample player DRM incluso nel pacchetto TVSDK.

Questi sono gli elementi API più importanti per l’utilizzo di DRM:

* Riferimento nel lettore multimediale all&#39;oggetto di gestione DRM che implementa il sottosistema DRM:

  ```java
  MediaPlayer.getDRMManager();
  ```

  >[!TIP]
  >
  >Questa API restituirà un valore `DRMManager` solo dopo il `MediaPlayerEvent.DRM_METADATA` è stato licenziato. Se chiami `getDRMManager()` prima dell&#39;attivazione di questo evento, potrebbe restituire NULL.

* Il `DRMHelper` classe helper, utile quando si implementano flussi di lavoro DRM.

  Puoi vedere `DRMHelper` in `ReferencePlayer`.

* A `DRMHelper` il metodo metadata loader, che carica i metadati DRM quando si trovano in un URL separato dal supporto.

  ```java
  public static void loadDRMMetadata(final DRMManager drmManager,  
     final String drmMetadataUrl,  
     final DRMLoadMetadataListener loadMetadataListener);
  ```

* A `DRMHelper` per verificare i metadati DRM e determinare se è necessaria l&#39;autenticazione.

  ```java
  /** 
  * Return whether authentication is needed for the provided 
  * DRMMetadata. 
  * 
  * @param drmMetadata 
  * The desired DRMMetadata on which to check whether auth is needed. 
  * @return whether authentication is required for the provided metadata 
  */ 
  public static boolean isAuthNeeded(DRMMetadata drmMetadata);
  ```

* `DRMHelper` metodo per eseguire l&#39;autenticazione.

  ```java
  /** 
  * Helper method to perform DRM authentication. 
  * 
  * @param drmManager 
  * the DRMManager, used to perform the authentication. 
  * @param drmMetadata 
  * the DRMMetadata, containing the DRM specific information. 
  * @param authenticationListener 
  * the listener, on which the user can be notified about the 
  * authentication process status. 
  * @param authUser 
  * the DRM username provider by the user. 
  * @param authPass 
  * the DRM password provided by the user. 
  */ 
  public static void performDrmAuthentication(final DRMManager drmManager,  
  final DRMMetadata drmMetadata,  
  final String authUser,  
  final String authPass,  
  final DRMAuthenticationListener authenticationListener);
  ```

* Eventi che notificano all&#39;applicazione varie attività e lo stato del DRM.

<!--<a id="section_899BD9061D484E1BBA46E84617C36867"></a>-->

Elementi API rilevanti aggiuntivi:

* [com.adobe.ave.drm.DRMManager](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMManager.html)
* [com.adobe.ave.drm.DRMMetdata](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMMetadata.html)
* [com.adobe.ave.drm.DRMPolicy](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMPolicy.html)
* [com.adobe.ave.drm.DRMAuthenticationMethod](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMAuthenticationMethod.html)
* [com.adobe.ave.drm.DRMAuthenticationCompleteCallback](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMAuthenticationCompleteCallback.html)
* [com.adobe.ave.drm.DRMOperationErrorCallback](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMOperationErrorCallback.html)
* com.adobe.mediacore.drm.DRMAuthenticateListener

<!-- 
Comment Type: draft
(https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/drm/DRMAuthenticateListener.html)

-->
<!--<a id="section_F58941D68EB94A5EBD1C7454D2A1B17A"></a>-->

Per ulteriori informazioni su DRM, vedere [Documentazione di Adobe Primetime DRM](https://helpx.adobe.com/primetime/user-guide.html).
