---
description: È possibile utilizzare le funzioni del Digital Rights Management Primetime (DRM) per fornire un accesso sicuro al contenuto video. In alternativa, è possibile utilizzare soluzioni DRM di terze parti in alternativa alla soluzione integrata di Adobe.
title: DRM widevine
exl-id: 44ab032e-e665-4b63-a08b-54e862894987
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# DRM widevine {#widevine-drm}

È possibile utilizzare le funzioni del Digital Rights Management Primetime (DRM) per fornire un accesso sicuro al contenuto video. In alternativa, è possibile utilizzare soluzioni DRM di terze parti in alternativa alla soluzione integrata di Adobe.

Per informazioni aggiornate sulla disponibilità di soluzioni DRM di terze parti, contattare il rappresentante di Adobe.

<!--<a id="section_1385440013EF4A9AA45B6AC98919E662"></a>-->

È possibile utilizzare il DRM widevine nativo Android con i flussi CMAF HLS.

>[!NOTE]
>
> Lo schema CTR CENC Widevine richiede almeno la versione Android 4.4 (API livello 19).
>
> Lo schema CBCS widevine richiede almeno la versione Android 7.1 (livello API 25).

## Imposta dettagli server licenze {#license-server-details}

Chiama quanto segue `com.adobe.mediacore.drm.DRMManager` API prima di caricare la risorsa MediaPlayer:

```java
public static void setProtectionData(
String drm,
String licenseServerURL,
Map<String, String> requestProperties)
```

### Argomenti {#arguments-license-server}

* `drm` - `"com.widevine.alpha"` per Widevine.

* `licenseServerURL` : URL del server licenze Widevine che riceve le richieste di licenza.

* `requestProperties` - Contiene intestazioni aggiuntive da includere nella richiesta di licenza in uscita.

Ad esempio, quando si utilizza contenuto incluso nel pacchetto per Expressplay DRM, utilizzare il codice seguente prima della riproduzione:

```java
DRMManager.setProtectionData(
  "com.widevine.alpha",  
  "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken= 
<i>token</i>",  
  null);
```

## Fornisci callback personalizzato {#custom-callback}

Chiama quanto segue `com.adobe.mediacore.drm.DRMManager` prima di caricare la risorsa MediaPlayer.

```java
public static void setMediaDrmCallback(
MediaDrmCallback callback)
```

### Argomenti {#arguments-custom-callback}

* `callback` : implementazione personalizzata di MediaDrmCallback da utilizzare al posto del valore predefinito `com.adobe.mediacore.drm.WidevineMediaDrmCallback`.

Per ulteriori informazioni, consulta [Documentazione API Android TVSDK 3.11](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.11/index.html).

## Recupera casella PSSH della risorsa MediaPlayer caricata corrente {#pssh-box-mediaplayer-resoource}

Chiama quanto segue `com.adobe.mediacore.drm.DRMManager` API, preferibilmente nell&#39;implementazione di callback personalizzata.

```java
public static byte[] getPSSH()
```

API restituisce la casella di intestazione specifica del sistema di protezione associata alla risorsa multimediale Widevine caricata.

È disponibile una casella valida per un breve periodo (tra la creazione dell’istanza DRM e il caricamento delle chiavi). `MediaDrmCallback callback executeKeyRequest()` può utilizzarlo per personalizzare il recupero delle chiavi di licenza.

>[!NOTE]
>
> `getPSSH()` L’API è supportata solo con un’istanza del lettore singolo. Più lettori o la funzione Instant On devono essere inizializzati in serie per ricevere la casella corretta.
