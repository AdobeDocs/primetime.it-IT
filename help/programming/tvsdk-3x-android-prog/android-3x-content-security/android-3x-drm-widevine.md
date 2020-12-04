---
description: Potete utilizzare le funzioni del sistema Digital Rights Management Primetime (DRM) per fornire un accesso sicuro ai contenuti video. In alternativa, potete utilizzare soluzioni DRM di terze parti come alternativa  soluzione integrata  Adobe.
seo-description: Potete utilizzare le funzioni del sistema Digital Rights Management Primetime (DRM) per fornire un accesso sicuro ai contenuti video. In alternativa, potete utilizzare soluzioni DRM di terze parti come alternativa  soluzione integrata  Adobe.
seo-title: DRM Widevine
title: DRM Widevine
uuid: 3a5fd786-4319-4e92-83b6-0f5328df6a44
translation-type: tm+mt
source-git-commit: 0271af21b74e80455ddb2c53571cd75f3a0f56ba
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---


# DRM Widevine {#widevine-drm}

Potete utilizzare le funzioni del sistema Digital Rights Management Primetime (DRM) per fornire un accesso sicuro ai contenuti video. In alternativa, potete utilizzare soluzioni DRM di terze parti come alternativa  soluzione integrata  Adobe.

Per informazioni aggiornate sulla disponibilità di soluzioni DRM di terze parti, contattate il rappresentante del Adobe .

<!--<a id="section_1385440013EF4A9AA45B6AC98919E662"></a>-->

Potete utilizzare il DRM Widevine nativo Android con flussi CMAF HLS.

>[!NOTE]
>
> Lo schema CTR CENC di Widevine richiede la versione minima di Android 4.4 (API Level 19).
>
> Widevine CBCS Scheme richiede la versione minima di Android 7.1 (API Level 25).

## Impostare i dettagli del server licenze {#license-server-details}

Chiama la seguente `com.adobe.mediacore.drm.DRMManager` API prima di caricare la risorsa MediaPlayer:

```java
public static void setProtectionData(
String drm,
String licenseServerURL,
Map<String, String> requestProperties)
```

### Argomenti {#arguments-license-server}

* `drm` -  `"com.widevine.alpha"` per Widevine.

* `licenseServerURL` - L&#39;URL del server licenze Widevine che riceve le richieste di licenza.

* `requestProperties` - Contiene intestazioni aggiuntive da includere nella richiesta di licenza in uscita.

Ad esempio, quando utilizzate contenuto incluso in un pacchetto per Express DRM, utilizzate il seguente codice prima di riprodurre:

```java
DRMManager.setProtectionData(
  "com.widevine.alpha",  
  "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken= 
<i>token</i>",  
  null);
```

## Fornire una callback personalizzata {#custom-callback}

Chiama la seguente `com.adobe.mediacore.drm.DRMManager` API prima di caricare la risorsa MediaPlayer.

```java
public static void setMediaDrmCallback(
MediaDrmCallback callback)
```

### Argomenti {#arguments-custom-callback}

* `callback` - implementazione personalizzata di MediaDrmCallback da utilizzare invece del valore predefinito  `com.adobe.mediacore.drm.WidevineMediaDrmCallback`.

Per informazioni dettagliate, consultate [Documentazione API TVSDK 3.11 per Android](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.11/index.html).

## Recupera casella PSSH della risorsa MediaPlayer caricata corrente {#pssh-box-mediaplayer-resoource}

Chiama la seguente `com.adobe.mediacore.drm.DRMManager` API, preferibilmente nell&#39;implementazione di callback personalizzata.

```java
public static byte[] getPSSH()
```

L&#39;API restituisce la Casella di intestazione specifica del sistema di protezione associata alla risorsa multimediale Widevine caricata.

È disponibile una casella valida per un periodo di breve durata (tra la creazione dell&#39;istanza DRM e il caricamento delle chiavi). `MediaDrmCallback callback executeKeyRequest()` può essere utilizzato per personalizzare il recupero delle chiavi di licenza.

>[!NOTE]
>
> `getPSSH()` L&#39;API è supportata solo con un&#39;istanza di lettore singolo. Più lettori o la funzione Attivato istantaneo deve essere inizializzata in serie per ricevere la casella corretta.
