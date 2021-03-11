---
description: È possibile utilizzare le funzioni del Digital Rights Management Primetime (DRM) per fornire un accesso sicuro ai contenuti video. In alternativa, è possibile utilizzare soluzioni DRM di terze parti come alternativa alla soluzione integrata di Adobe.
title: DRM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---


# DRM Widevine {#widevine-drm}

È possibile utilizzare le funzioni del Digital Rights Management Primetime (DRM) per fornire un accesso sicuro ai contenuti video. In alternativa, è possibile utilizzare soluzioni DRM di terze parti come alternativa alla soluzione integrata di Adobe.

Contatta il tuo rappresentante di Adobe per informazioni aggiornate sulla disponibilità di soluzioni DRM di terze parti.

<!--<a id="section_1385440013EF4A9AA45B6AC98919E662"></a>-->

È possibile utilizzare il DRM nativo Widevine Android con flussi CMAF HLS.

>[!NOTE]
>
> Lo schema CTR di Widevine CENC richiede la versione minima di Android 4.4 (API Level 19).
>
> Lo schema CBCS di Widevine richiede la versione minima di Android 7.1 (API Level 25).

## Imposta i dettagli del server licenze {#license-server-details}

Chiama la seguente `com.adobe.mediacore.drm.DRMManager` API prima di caricare la risorsa MediaPlayer:

```java
public static void setProtectionData(
String drm,
String licenseServerURL,
Map<String, String> requestProperties)
```

### Argomenti {#arguments-license-server}

* `drm` -  `"com.widevine.alpha"` per Widevine.

* `licenseServerURL` - L&#39;URL del server licenze Widevine che riceve richieste di licenza.

* `requestProperties` - Contiene intestazioni aggiuntive da includere nella richiesta di licenza in uscita.

Ad esempio, quando utilizzi il contenuto incluso nel pacchetto per Expressplay DRM, utilizza il codice seguente prima di riprodurre:

```java
DRMManager.setProtectionData(
  "com.widevine.alpha",  
  "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken= 
<i>token</i>",  
  null);
```

## Fornire un callback personalizzato {#custom-callback}

Chiama la seguente `com.adobe.mediacore.drm.DRMManager` API prima di caricare la risorsa MediaPlayer.

```java
public static void setMediaDrmCallback(
MediaDrmCallback callback)
```

### Argomenti {#arguments-custom-callback}

* `callback` - implementazione personalizzata di MediaDrmCallback da utilizzare invece del valore predefinito  `com.adobe.mediacore.drm.WidevineMediaDrmCallback`.

Per informazioni dettagliate, consulta la [documentazione API TVSDK 3.11 per Android](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.11/index.html).

## Recupera PSSH Box della risorsa MediaPlayer caricata corrente {#pssh-box-mediaplayer-resoource}

Chiama la seguente `com.adobe.mediacore.drm.DRMManager` API, preferibilmente nell’implementazione di callback personalizzata.

```java
public static byte[] getPSSH()
```

API restituisce la casella di intestazione specifica del sistema di protezione associata alla risorsa multimediale Widevine caricata.

È disponibile una casella valida per un breve periodo di tempo (tra la creazione dell’istanza DRM e il caricamento delle chiavi). `MediaDrmCallback callback executeKeyRequest()` può essere utilizzato per personalizzare il recupero delle chiavi di licenza.

>[!NOTE]
>
> `getPSSH()` L’API è supportata solo con l’istanza di un singolo lettore. Per ricevere la casella corretta, è necessario che più lettori o la funzione di attivazione immediata inizializzino in modo seriale.
