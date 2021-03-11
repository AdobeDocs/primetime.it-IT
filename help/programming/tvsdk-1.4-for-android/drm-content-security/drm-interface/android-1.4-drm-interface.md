---
description: È possibile utilizzare le funzioni del Digital Rights Management Primetime (DRM) per fornire un accesso sicuro ai contenuti video. In alternativa, è possibile utilizzare soluzioni DRM di terze parti come alternativa alla soluzione DRM integrata di Adobe di Primetime.
title: Panoramica dell'interfaccia DRM di Primetime
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---


# Panoramica {#primetime-drm-interface-overview}

È possibile utilizzare le funzioni del Digital Rights Management Primetime (DRM) per fornire un accesso sicuro ai contenuti video. In alternativa, è possibile utilizzare soluzioni DRM di terze parti come alternativa alla soluzione DRM integrata di Adobe di Primetime.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Rivolgiti al tuo rappresentante di Adobe per ottenere informazioni aggiornate sulla disponibilità di soluzioni DRM di terze parti.

L&#39;elemento chiave lato client del sistema DRM (Digital Rights Management) di Primetime è il DRM Manager. L&#39;applicazione di esempio inclusa nell&#39;SDK per Android include una classe `DRMHelper` che dimostra come semplificare l&#39;implementazione di determinate operazioni DRM.

Primetime DRM fornisce un flusso di lavoro scalabile ed efficiente per implementare la protezione dei contenuti nelle applicazioni TVSDK. È possibile proteggere e gestire i diritti relativi ai contenuti video creando una licenza per ogni file multimediale digitale.

Fai riferimento al codice del sample player DRM incluso nel pacchetto TVSDK.

Questi sono gli elementi API più importanti per lavorare con DRM:

* Un riferimento nel lettore multimediale all&#39;oggetto manager DRM che implementa il sottosistema DRM:

   ```java
   MediaPlayer.getDRMManager();
   ```

   >[!TIP]
   >
   >Questa API restituirà un oggetto `DRMManager` valido solo dopo l&#39;attivazione di `MediaPlayerEvent.DRM_METADATA`. Se chiami `getDRMManager()` prima che questo evento venga attivato, potrebbe essere restituito NULL.

* La classe helper `DRMHelper`, utile quando si implementano i flussi di lavoro DRM.

   È possibile visualizzare `DRMHelper` in `ReferencePlayer`.

* Un metodo di caricamento dei metadati `DRMHelper` che carica i metadati DRM quando si trovano in un URL separato dal supporto multimediale.

   ```java
   public static void loadDRMMetadata(final DRMManager drmManager,  
      final String drmMetadataUrl,  
      final DRMLoadMetadataListener loadMetadataListener);
   ```

* Un metodo `DRMHelper` per controllare i metadati DRM per determinare se è necessaria l’autenticazione.

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

* Eventi che notificano all’applicazione varie attività e stato di DRM.

<!--<a id="section_899BD9061D484E1BBA46E84617C36867"></a>-->

Altri elementi API rilevanti:

* [com.adobe.ave.drm.DRMManager](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMManager.html)
* [com.adobe.ave.drm.DRMMetdata](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMMetadata.html)
* [com.adobe.ave.drm.DRMPolicy](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMPolicy.html)
* [com.adobe.ave.drm.DRMAuthAuthenticationMethod](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMAuthenticationMethod.html)
* [com.adobe.ave.drm.DRMAuthAuthenticationCompleteCallback](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMAuthenticationCompleteCallback.html)
* [com.adobe.ave.drm.DRMOperationErrorCallback](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMOperationErrorCallback.html)
* com.adobe.mediacore.drm.DRMAuthenticateListener

<!-- 
Comment Type: draft
(https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/drm/DRMAuthenticateListener.html)

-->
<!--<a id="section_F58941D68EB94A5EBD1C7454D2A1B17A"></a>-->

Per ulteriori informazioni su DRM, consulta la [documentazione Adobe Primetime DRM](https://helpx.adobe.com/primetime/user-guide.html).
