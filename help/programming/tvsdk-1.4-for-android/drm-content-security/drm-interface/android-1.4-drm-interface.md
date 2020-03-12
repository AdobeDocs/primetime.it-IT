---
description: Potete utilizzare le funzioni del sistema DRM (Digital Rights Management) di Primetime per fornire un accesso protetto ai contenuti video. In alternativa, puoi utilizzare soluzioni DRM di terze parti come alternativa alla soluzione DRM integrata di Adobe Primetime.
seo-description: Potete utilizzare le funzioni del sistema DRM (Digital Rights Management) di Primetime per fornire un accesso protetto ai contenuti video. In alternativa, puoi utilizzare soluzioni DRM di terze parti come alternativa alla soluzione DRM integrata di Adobe Primetime.
seo-title: Panoramica dell'interfaccia DRM di Primetime
title: Panoramica dell'interfaccia DRM di Primetime
uuid: 71479464-8356-4732-9774-da9f6084e6ad
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Panoramica {#primetime-drm-interface-overview}

Potete utilizzare le funzioni del sistema DRM (Digital Rights Management) di Primetime per fornire un accesso protetto ai contenuti video. In alternativa, puoi utilizzare soluzioni DRM di terze parti come alternativa alla soluzione DRM integrata di Adobe Primetime.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Per informazioni aggiornate sulla disponibilità di soluzioni DRM di terze parti, contattate il vostro rappresentante Adobe.

L&#39;elemento chiave lato client del sistema DRM (Digital Rights Management) di Primetime è il manager DRM. L’applicazione di esempio inclusa nell’SDK per Android include una `DRMHelper` classe che dimostra come rendere alcune operazioni DRM più facili da implementare.

Primetime DRM fornisce un flusso di lavoro scalabile ed efficiente per implementare la protezione dei contenuti nelle applicazioni TVSDK. Potete proteggere e gestire i diritti relativi ai contenuti video creando una licenza per ciascun file multimediale digitale.

Fate riferimento al codice del lettore di esempio DRM incluso nel pacchetto TVSDK.

Questi sono gli elementi API più importanti per lavorare con DRM:

* Un riferimento nel lettore multimediale all&#39;oggetto manager DRM che implementa il sottosistema DRM:

   ```java
   MediaPlayer.getDRMManager();
   ```

   >[!TIP]
   >
   >Questa API restituirà un `DRMManager` oggetto valido solo dopo che l&#39; `MediaPlayerEvent.DRM_METADATA` evento è stato attivato. Se chiamate `getDRMManager()` prima dell&#39;attivazione di questo evento, potrebbe restituire NULL.

* La classe `DRMHelper` helper, utile per l&#39;implementazione di flussi di lavoro DRM.

   Potete vedere `DRMHelper` in `ReferencePlayer`.

* Un metodo `DRMHelper` di caricamento dei metadati, che carica i metadati DRM quando questi si trovano in un URL separato dal supporto.

   ```java
   public static void loadDRMMetadata(final DRMManager drmManager,  
      final String drmMetadataUrl,  
      final DRMLoadMetadataListener loadMetadataListener);
   ```

* Un `DRMHelper` metodo per controllare i metadati DRM per determinare se è necessaria l&#39;autenticazione.

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

* `DRMHelper` per eseguire l&#39;autenticazione.

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

* Eventi che notificano all’applicazione le varie attività e lo stato di DRM.

<!--<a id="section_899BD9061D484E1BBA46E84617C36867"></a>-->

Altri elementi API rilevanti:

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

Per ulteriori informazioni su DRM, consulta la documentazione [DRM di](https://helpx.adobe.com/primetime/user-guide.html)Adobe Primetime.
