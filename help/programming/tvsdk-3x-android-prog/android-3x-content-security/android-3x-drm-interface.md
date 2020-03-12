---
description: L'elemento chiave lato client della soluzione DRM Primetime è il manager DRM. L’applicazione di esempio inclusa nell’SDK per Android include anche una classe DRMHelper che può essere utilizzata per rendere alcune operazioni DRM più facili da implementare.
seo-description: L'elemento chiave lato client della soluzione DRM Primetime è il manager DRM. L’applicazione di esempio inclusa nell’SDK per Android include anche una classe DRMHelper che può essere utilizzata per rendere alcune operazioni DRM più facili da implementare.
seo-title: Panoramica dell'interfaccia DRM di Primetime
title: Panoramica dell'interfaccia DRM di Primetime
uuid: 9e6f6ae6-7193-40fe-bc9d-d8de33705f5d
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Panoramica dell&#39;interfaccia DRM di Primetime {#primetime-drm-interface-overview}

L&#39;elemento chiave lato client della soluzione DRM Primetime è il manager DRM. L’applicazione di esempio inclusa nell’SDK per Android include anche una `DRMHelper` classe che può essere utilizzata per rendere alcune operazioni DRM più facili da implementare.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Primetime DRM fornisce un flusso di lavoro scalabile ed efficiente per implementare la protezione dei contenuti nelle applicazioni TVSDK. Potete proteggere e gestire i diritti relativi ai contenuti video creando una licenza per ciascun file multimediale digitale.

Per ulteriori informazioni, consultate il codice del lettore di esempio DRM incluso nel pacchetto TVSDK.

Di seguito sono riportati gli elementi API più importanti per l&#39;utilizzo di DRM:

* Un riferimento nel lettore multimediale all&#39;oggetto manager DRM che implementa il sottosistema DRM:

   ```java
   MediaPlayer.getDRMManager();
   ```

   >[!TIP]
   >
   >Questa API restituirà un `DRMManager` oggetto valido solo dopo che l&#39; `MediaPlayerEvent.DRM_METADATA` evento è stato attivato. Se chiamate `getDRMManager()` prima dell&#39;attivazione di questo evento, potrebbe restituire NULL.

* La classe `DRMHelper` helper, utile per l&#39;implementazione di flussi di lavoro DRM.
* Un metodo `DRMHelper` di caricamento dei metadati, che carica i metadati DRM quando questi si trovano in un URL separato dal supporto.

   ```java
   public static void loadDRMMetadata(final DRMManager drmManager,  
      final String drmMetadataUrl,  
      final DRMLoadMetadataListener loadMetadataListener);
   ```

* Un `DRMHelper` metodo per controllare i metadati DRM e determinare se è necessaria l&#39;autenticazione.

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

Per ulteriori informazioni su DRM, consulta la documentazione [](https://helpx.adobe.com/primetime/user-guide.html)DRM.
