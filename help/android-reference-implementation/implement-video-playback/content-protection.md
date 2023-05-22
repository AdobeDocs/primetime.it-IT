---
description: Il lettore Primetime supporta l’integrazione di Primetime DRM come flussi di lavoro DRM personalizzati. Ciò significa che l'applicazione deve implementare i flussi di lavoro di autenticazione DRM prima di riprodurre il flusso.
title: Protezione dei contenuti DRM
exl-id: c1904d15-023f-49fb-95f9-d157d17b3516
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---

# Protezione dei contenuti DRM {#drm-content-protection}

Il lettore Primetime supporta l’integrazione di Primetime DRM come flussi di lavoro DRM personalizzati. Ciò significa che l&#39;applicazione deve implementare i flussi di lavoro di autenticazione DRM prima di riprodurre il flusso.

Per abilitare questa funzione, TVSDK fornisce il gestore DRM per l&#39;autenticazione. L’implementazione di riferimento fornisce un esempio dei seguenti flussi di lavoro:

* Come caricare e riprodurre flussi HLS con protezione dei contenuti di Access, ottimizzati per tassi di errore bassi e avvio rapido.
* Come caricare e riprodurre flussi HLS con protezione dei contenuti AES128.
* Come caricare e riprodurre flussi HLS con protezione dei contenuti PHLS, ottimizzati per tassi di errore bassi e avvio rapido.

Tutti i contenuti protetti da DRM vengono gestiti automaticamente dalle librerie DRM integrate in TVSDK. Tuttavia, puoi esporre la gestione degli errori, l’ottimizzazione della personalizzazione del dispositivo e l’acquisizione delle licenze utilizzando i callback API TVSDK.

## Aggiungere la protezione dei contenuti al lettore {#section_F1FC4322C35C4FE8A3B47FDC0A74221B}

Puoi aggiungere la protezione dei contenuti al lettore creando un gestore della riproduzione o utilizzando il programma di fabbrica del gestore.

Per creare un gestore della protezione dei contenuti:

* Inizializzare il sistema DRM.

   Esempio Nell&#39;esempio di codice riportato di seguito viene illustrato come chiamare `loadDRMServices` nell’applicazione `onCreate()` per garantire che qualsiasi inizializzazione necessaria per il sistema DRM venga avviata prima dell&#39;avvio della riproduzione.

   ```java
   @Override 
    public void onCreate() { 
        super.onCreate();  
        DrmManager.loadDRMServices(getApplicationContext()); 
    }
   ```

* Precaricare le licenze DRM.

   Nell&#39;esempio di codice riportato di seguito viene illustrato come caricare `VideoItems` al termine del caricamento dell’elenco dei contenuti. In questo modo, le licenze DRM vengono acquisite dal server licenze e memorizzate nella cache locale, in modo che all’avvio della riproduzione il contenuto venga caricato con il minimo ritardo.

   ```java
   DrmManager.preLoadDrmLicenses(item.getUrl(),  
     new MediaPlayerItemLoader.LoaderListener() { 
   
       @Override 
       public void onLoadComplete(MediaPlayerItem item) { 
           Player.logger.w(LOG_TAG + "::DRMPreload#onLoadComplete", item.getResource().getUrl()); 
       } 
   
       @Override 
       public void onError(MediaErrorCode errorCode, String s) { 
           Player.logger.e(LOG_TAG + "::DRMPreload#onError", s); 
       } 
   } 
   ```

   >[!NOTE]
   >
   >È possibile impostare Precache DRM license (Licenze DRM precedenti) su ON (Attivate) nell&#39;interfaccia utente Settings (Impostazioni) per prememorizzare le licenze DRM nella cache durante il caricamento del contenuto. Tuttavia, si consiglia di precaricare un elemento specifico invece di prememorizzare nella cache tutte le licenze nel catalogo.
   >
   >![](assets/precache-drm-licenses.jpg)

* Da utilizzare `ManagerFactory` per implementare la gestione degli errori DRM, assicurarsi che la seguente riga di codice sia nel [!DNL PlayerFragment.java] file:

   ```java
   drmManager = ManagerFactory.getDrmManager(config, mediaPlayer);
   ```

**Documentazione API correlata**

* [Classe DrmManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/DrmManager.html)
* [DrmManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/DrmManager.DrmManagerEventListener.html)
