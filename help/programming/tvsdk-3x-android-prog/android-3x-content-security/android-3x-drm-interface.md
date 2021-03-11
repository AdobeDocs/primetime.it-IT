---
description: L'elemento chiave lato client della soluzione DRM di Primetime è il DRM Manager. L’applicazione di esempio inclusa con l’SDK per Android include anche una classe DRMHelper che può essere utilizzata per facilitare l’implementazione di determinate operazioni DRM.
title: Panoramica dell'interfaccia DRM di Primetime
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# Panoramica dell&#39;interfaccia DRM di Primetime {#primetime-drm-interface-overview}

L&#39;elemento chiave lato client della soluzione DRM di Primetime è il DRM Manager. L’applicazione di esempio inclusa con l’SDK per Android include anche una classe `DRMHelper` che può essere utilizzata per facilitare l’implementazione di determinate operazioni DRM.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Primetime DRM fornisce un flusso di lavoro scalabile ed efficiente per implementare la protezione dei contenuti nelle applicazioni TVSDK. È possibile proteggere e gestire i diritti relativi ai contenuti video creando una licenza per ogni file multimediale digitale.

Per ulteriori informazioni, vedi il codice del sample player DRM incluso nel pacchetto TVSDK.

Di seguito sono riportati gli elementi API più importanti per l’utilizzo di DRM:

* Un riferimento nel lettore multimediale all&#39;oggetto manager DRM che implementa il sottosistema DRM:

   ```java
   MediaPlayer.getDRMManager();
   ```

   >[!TIP]
   >
   >Questa API restituirà un oggetto `DRMManager` valido solo dopo l&#39;attivazione di `MediaPlayerEvent.DRM_METADATA`. Se chiami `getDRMManager()` prima che questo evento venga attivato, potrebbe essere restituito NULL.

* La classe helper `DRMHelper`, utile quando si implementano i flussi di lavoro DRM.
* Un metodo di caricamento dei metadati `DRMHelper` che carica i metadati DRM quando si trovano in un URL separato dal supporto multimediale.

   ```java
   public static void loadDRMMetadata(final DRMManager drmManager,  
      final String drmMetadataUrl,  
      final DRMLoadMetadataListener loadMetadataListener);
   ```

* Un metodo `DRMHelper` per controllare i metadati DRM e determinare se è necessaria l’autenticazione.

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

Per ulteriori informazioni su DRM, consulta la [documentazione DRM](https://helpx.adobe.com/primetime/user-guide.html).
