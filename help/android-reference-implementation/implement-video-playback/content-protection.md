---
description: Il lettore Primetime supporta l'integrazione DRM di Primetime come flussi di lavoro DRM personalizzati. Ciò significa che l'applicazione deve implementare i flussi di lavoro di autenticazione DRM prima di riprodurre il flusso.
seo-description: Il lettore Primetime supporta l'integrazione DRM di Primetime come flussi di lavoro DRM personalizzati. Ciò significa che l'applicazione deve implementare i flussi di lavoro di autenticazione DRM prima di riprodurre il flusso.
seo-title: Protezione dei contenuti DRM
title: Protezione dei contenuti DRM
uuid: 95c446f6-8304-4d70-9bef-7368b9364025
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---


# Protezione del contenuto DRM {#drm-content-protection}

Il lettore Primetime supporta l&#39;integrazione DRM di Primetime come flussi di lavoro DRM personalizzati. Ciò significa che l&#39;applicazione deve implementare i flussi di lavoro di autenticazione DRM prima di riprodurre il flusso.

Per abilitare questa opzione, TVSDK fornisce all&#39;utente il manager DRM per l&#39;autenticazione. L’implementazione di riferimento fornisce un esempio dei seguenti flussi di lavoro:

* Come caricare e riprodurre flussi HLS con protezione dei contenuti di Access, ottimizzati per basse frequenze di errore e avvio rapido.
* Come caricare e riprodurre flussi HLS con protezione dei contenuti AES128.
* Come caricare e riprodurre flussi HLS con protezione dei contenuti PHLS, ottimizzati per basse frequenze di errore e avvio rapido.

Tutto il contenuto protetto da DRM viene gestito automaticamente dalle librerie DRM integrate in TVSDK. Tuttavia, potete esporre la gestione degli errori, l&#39;ottimizzazione dell&#39;individualizzazione del dispositivo e l&#39;acquisizione della licenza tramite callback API TVSDK.

## Aggiunta protezione del contenuto al lettore {#section_F1FC4322C35C4FE8A3B47FDC0A74221B}

È possibile aggiungere la protezione del contenuto al lettore creando un manager riproduzione o utilizzando la fabbrica di gestione.

Per creare un gestore della protezione dei contenuti:

* Inizializzare il sistema DRM.

   L&#39;esempio di codice seguente mostra la chiamata `loadDRMServices` nella funzione `onCreate()` dell&#39;applicazione, per garantire che l&#39;inizializzazione necessaria per il sistema DRM sia avviata prima dell&#39;avvio della riproduzione.

   ```java
   @Override 
    public void onCreate() { 
        super.onCreate();  
        DrmManager.loadDRMServices(getApplicationContext()); 
    }
   ```

* Precaricare le licenze DRM.

   L&#39;esempio di codice seguente mostra il caricamento di `VideoItems` al termine del caricamento dell&#39;elenco dei contenuti. Ciò comporterà l&#39;acquisizione delle licenze DRM dal server licenze e la memorizzazione nella cache locale, in modo che all&#39;avvio della riproduzione il contenuto verrà caricato con un ritardo minimo.

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
   >Potete impostare le licenze DRM Precache su ON nell&#39;interfaccia utente Settings per prememorizzare le licenze DRM durante il caricamento del contenuto. Tuttavia, è consigliabile precaricare un elemento specifico invece di prememorizzare tutte le licenze nel catalogo.
   >
   >![](assets/precache-drm-licenses.jpg)

* Per utilizzare `ManagerFactory` per implementare la gestione degli errori DRM, assicurarsi che la seguente riga di codice sia nel file [!DNL PlayerFragment.java]:

   ```java
   drmManager = ManagerFactory.getDrmManager(config, mediaPlayer);
   ```

**Documentazione API correlata**

* [Classe DrmManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/DrmManager.html)
* [DrmManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/DrmManager.DrmManagerEventListener.html)