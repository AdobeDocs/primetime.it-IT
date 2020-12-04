---
description: L'elemento chiave lato client della soluzione DRM Primetime è il manager DRM. L’applicazione di esempio inclusa nell’SDK per Android include anche una classe DRMHelper che può essere utilizzata per rendere alcune operazioni DRM più facili da implementare.
seo-description: L'elemento chiave lato client della soluzione DRM Primetime è il manager DRM. L’applicazione di esempio inclusa nell’SDK per Android include anche una classe DRMHelper che può essere utilizzata per rendere alcune operazioni DRM più facili da implementare.
seo-title: Panoramica dell'interfaccia DRM di Primetime
title: Panoramica dell'interfaccia DRM di Primetime
uuid: 9e6f6ae6-7193-40fe-bc9d-d8de33705f5d
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 0%

---


# Panoramica dell&#39;interfaccia DRM Primetime {#primetime-drm-interface-overview}

L&#39;elemento chiave lato client della soluzione DRM Primetime è il manager DRM. L&#39;applicazione di esempio inclusa con l&#39;SDK Android include anche una classe `DRMHelper` che può essere utilizzata per rendere alcune operazioni DRM più facili da implementare.

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
   >Questa API restituirà un oggetto `DRMManager` valido solo dopo l&#39;attivazione di `MediaPlayerEvent.DRM_METADATA`. Se si chiama `getDRMManager()` prima dell&#39;attivazione dell&#39;evento, è possibile che restituisca NULL.

* La classe helper `DRMHelper`, utile per l&#39;implementazione dei flussi di lavoro DRM.
* Un metodo di caricamento dei metadati `DRMHelper` che carica i metadati DRM quando questi si trovano in un URL separato dal supporto.

   ```java
   public static void loadDRMMetadata(final DRMManager drmManager,  
      final String drmMetadataUrl,  
      final DRMLoadMetadataListener loadMetadataListener);
   ```

* Un metodo `DRMHelper` per controllare i metadati DRM e determinare se l&#39;autenticazione è necessaria.

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

Per ulteriori informazioni su DRM, consultare la [documentazione DRM](https://helpx.adobe.com/primetime/user-guide.html).
