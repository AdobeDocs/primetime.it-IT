---
description: L'elemento chiave lato client della soluzione DRM di Primetime è DRM Manager. L’applicazione di esempio inclusa con l’SDK per Android include anche una classe DRMHelper che può essere utilizzata per semplificare l’implementazione di alcune operazioni DRM.
title: Panoramica dell’interfaccia DRM di Primetime
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---

# Panoramica dell’interfaccia DRM di Primetime {#primetime-drm-interface-overview}

L&#39;elemento chiave lato client della soluzione DRM di Primetime è DRM Manager. L’applicazione di esempio inclusa con l’SDK per Android include anche una classe DRMHelper che può essere utilizzata per semplificare l’implementazione di alcune operazioni DRM.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Primetime DRM fornisce un flusso di lavoro scalabile ed efficiente per implementare la protezione dei contenuti nelle applicazioni TVSDK. Per proteggere e gestire i diritti dei contenuti video, crea una licenza per ciascun file multimediale digitale.

Per ulteriori informazioni, vedere il codice del lettore di esempio DRM incluso nel pacchetto TVSDK.

Di seguito sono riportati gli elementi API più importanti per l’utilizzo di DRM:

* Riferimento nel lettore multimediale all&#39;oggetto di gestione DRM che implementa il sottosistema DRM:

  ```java
  MediaPlayer.getDRMManager();
  ```

  >[!TIP]
  >
  >Questa API restituirà un valore `DRMManager` solo dopo il `MediaPlayerEvent.DRM_METADATA` è stato licenziato. Se chiami `getDRMManager()` prima dell&#39;attivazione di questo evento, potrebbe restituire NULL.

* Il `DRMHelper` classe helper, utile quando si implementano flussi di lavoro DRM.
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

<!--<a id="section_F58941D68EB94A5EBD1C7454D2A1B17A"></a>-->

Per ulteriori informazioni su DRM, vedere [Documentazione DRM](https://helpx.adobe.com/primetime/user-guide.html).
