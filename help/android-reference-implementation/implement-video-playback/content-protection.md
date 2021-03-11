---
description: Il lettore Primetime supporta l'integrazione DRM di Primetime come flussi di lavoro DRM personalizzati. Ciò significa che l’applicazione deve implementare i flussi di lavoro di autenticazione DRM prima di riprodurre il flusso.
title: Protezione dei contenuti DRM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---


# Protezione dei contenuti DRM {#drm-content-protection}

Il lettore Primetime supporta l&#39;integrazione DRM di Primetime come flussi di lavoro DRM personalizzati. Ciò significa che l’applicazione deve implementare i flussi di lavoro di autenticazione DRM prima di riprodurre il flusso.

Per abilitare questa funzione, TVSDK ti fornisce la gestione DRM per l’autenticazione. L’implementazione di riferimento fornisce un esempio dei seguenti flussi di lavoro:

* Come caricare e riprodurre flussi HLS con protezione dei contenuti di Access, ottimizzato per bassi tassi di errore e avvio rapido.
* Come caricare e riprodurre flussi HLS con la protezione dei contenuti AES128.
* Come caricare e riprodurre flussi HLS con protezione dei contenuti PHLS, ottimizzato per bassi tassi di errore e avvio rapido.

Tutti i contenuti protetti da DRM vengono gestiti automaticamente dalle librerie DRM integrate nel TVSDK. Tuttavia, puoi esporre la gestione degli errori, l’ottimizzazione dell’individualizzazione del dispositivo e l’acquisizione della licenza utilizzando i callback API TVSDK.

## Aggiungi la protezione del contenuto al lettore {#section_F1FC4322C35C4FE8A3B47FDC0A74221B}

È possibile aggiungere la protezione del contenuto al lettore creando un gestore di riproduzione o utilizzando il manager factory.

Per creare un gestore della protezione dei contenuti:

* Inizializzare il sistema DRM.

   L&#39;esempio di codice seguente mostra la chiamata di `loadDRMServices` nella funzione dell&#39;applicazione `onCreate()` per garantire che l&#39;inizializzazione necessaria per il sistema DRM venga avviata prima dell&#39;avvio della riproduzione.

   ```java
   @Override 
    public void onCreate() { 
        super.onCreate();  
        DrmManager.loadDRMServices(getApplicationContext()); 
    }
   ```

* Caricare le licenze DRM.

   L&#39;esempio di codice seguente mostra il caricamento di `VideoItems` al termine del caricamento dell&#39;elenco di contenuti. In questo modo le licenze DRM verranno acquisite dal server licenze e memorizzate nella cache locale, in modo che, all&#39;avvio della riproduzione, il contenuto venga caricato con un ritardo minimo.

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
   >È possibile impostare le licenze DRM Precache su ON nell&#39;interfaccia utente Impostazioni per prenotare le licenze DRM durante il caricamento del contenuto. Tuttavia, è consigliabile precaricare un elemento specifico invece di prememorizzare tutte le licenze nel catalogo.
   >
   >![](assets/precache-drm-licenses.jpg)

* Per utilizzare `ManagerFactory` per implementare la gestione degli errori DRM, assicurati che la seguente riga di codice sia nel file [!DNL PlayerFragment.java]:

   ```java
   drmManager = ManagerFactory.getDrmManager(config, mediaPlayer);
   ```

**Documentazione API correlata**

* [Classe DrmManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/DrmManager.html)
* [DrmManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/DrmManager.DrmManagerEventListener.html)