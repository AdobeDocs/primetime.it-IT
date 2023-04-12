---
title: Trasferimento delle informazioni sul client (dispositivo, connessione e applicazione)
description: Trasferimento delle informazioni sul client (dispositivo, connessione e applicazione)
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1681'
ht-degree: 0%

---


# Trasferimento delle informazioni sul client (dispositivo, connessione e applicazione) {#pass-client-info}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.


## Ambito {#pass-client-info-scope}

Questo documento aggrega i dettagli e le cartelle di cookie per il passaggio di informazioni client (dispositivo, connessione e applicazione) da un’applicazione Programmer alle API REST o agli SDK di autenticazione Adobe Primetime.

I vantaggi della fornitura di informazioni ai clienti sono i seguenti:

* Possibilità di abilitare l&#39;autenticazione di base (HBA) nel caso di alcuni tipi di dispositivi e MVPD che supportano HBA.
* La possibilità di applicare correttamente i TTL nel caso di alcuni tipi di dispositivi (ad esempio, configurare TTL più lunghi per le sessioni di autenticazione su dispositivi collegati alla TV).
* Possibilità di aggregare correttamente le metriche aziendali in rapporti suddivisi per tipi di dispositivi utilizzando il monitoraggio del servizio di adesione (ESM).
* Sblocca la possibilità di applicare correttamente varie regole di business (ad esempio, degradazione) su tipi di dispositivi specifici.

## Panoramica {#pass-client-info-overview}

Le informazioni sul cliente consistono in:

* **Dispositivo** informazioni sugli attributi hardware e software del dispositivo da cui l&#39;utente sta tentando di utilizzare il contenuto del programmatore.
* **Connessione** informazioni sugli attributi di connessione del dispositivo da cui l&#39;utente si connette ai servizi e/o ai servizi di programmazione di Adobe Primetime Authentication (ad esempio, implementazioni server-to-server).
* **Applicazione** informazioni sull&#39;applicazione registrata da cui l&#39;utente sta tentando di utilizzare il contenuto del programmatore.

Le informazioni client sono un oggetto JSON generato con chiavi presentate nella tabella seguente.

>[!NOTE]
>
>I seguenti **chiavi** sono **obbligatorio** da inviare nell&#39;oggetto JSON informazioni client: **model**, **osName**.
>
>Le seguenti chiavi hanno **limitato** valori: `primaryHardwareType`, `osName`, `osFamily`, `browserName`, `browserVendor`, `connectionSecure`.

|  | Chiave | Limitato | Descrizione | Valori possibili |
|---|---|---|---|---|
|  | primaryHardwareType | # Sì | Il tipo di hardware principale del dispositivo. | # I valori sono limitati: Telecamera DataCollectionTerminal Desktop EmbeddedNetworkModule eReader GiochiConsole GeolocalizzazioneTracker Occhiali MediaPlayer MobilePhone PaymentTerminal PluginModem SetTopBox TV Tablet WirelessHotspot Wristwatch sconosciuto |
| #mandatory | model | No | Nome del modello del dispositivo. | ad esempio iPhone, SM-G930V, AppleTV, ecc. |
|  | version | No | Versione del dispositivo. | ad esempio 2.0.1, ecc. |
|  | produttore | No | Società/organizzazione di produzione del dispositivo. | Ad esempio Samsung, LG, ZTE, Huawei, Motorola, Apple, ecc. |
|  | fornitore | No | Società/organizzazione di vendita del dispositivo. | Ad esempio, Apple, Samsung, LG, Google, ecc. |
| #mandatory | osName | # Sì | Nome del sistema operativo del dispositivo. | # I valori sono limitati: Android Chrome OS Linux Mac OS X OpenBSD Roku OS Windows iOS tvOS webOS |
|  | osFamily | Sì | Nome del gruppo del sistema operativo del dispositivo. | # I valori sono limitati: Android BSD Linux PlayStation OS Roku OS Symbian Tizen Windows iOS macOS tvOS webOS |
|  | osVendor | No | Fornitore del sistema operativo del dispositivo. | Amazon Apple Google LG Microsoft Mozilla Nintendo Nokia Roku Samsung Progetto Tizen di Sony |
|  | osVersion | No | Versione del sistema operativo del dispositivo. | Ad esempio 10.2, 9.0.1, ecc. |
|  | browserName | # Sì | Nome del browser. | # I valori sono limitati: Browser Android Chrome Edge Firefox Internet Explorer Opera Safari SeaMonkey Browser Symbian |
|  | browserVendor | # Sì | Azienda/organizzazione di costruzione del browser. | # I valori sono limitati: Amazon Apple Google Microsoft Motorola Mozilla Netscape Nintendo Nokia Samsung Sony Ericsson |
|  | browserVersion | No | Versione del browser del dispositivo. | ad esempio 60.0.3112 |
|  | userAgent | No | L&#39;agente utente del dispositivo. | ad esempio Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_3) AppleWebKit/602.4.8 (KHTML, come Gecko) Versione/10.0.3 Safari/602.4.8 |
|  | displayWidth | No | Larghezza dello schermo fisico del dispositivo. |  |
|  | displayHeight | No | Altezza dello schermo fisico del dispositivo. |  |
|  | displayPpi | No | La densità dei pixel dello schermo fisico del dispositivo. | ad esempio 294 |
|  | diagonaleScreenSize | No | Dimensione diagonale dello schermo fisico del dispositivo in pollici. | ad esempio 5.5, 10.1 |
|  | connectionIp | No | IP del dispositivo utilizzato per l’invio di richieste HTTP. | ad esempio 8.8.4.4 |
|  | connectionPort | No | La porta del dispositivo utilizzata per l’invio di richieste HTTP. | ad esempio 53124 |
|  | connectionType | No | Tipo di connessione di rete. | ad esempio WiFi, LAN, 3G, 4G, 5G |
|  | connectionSecure | # Sì | Stato di protezione della connessione di rete. | # I valori sono limitati: true - nel caso di una rete sicura false - nel caso di un hotspot pubblico |
|  | applicationId | No | Identificatore univoco dell&#39;applicazione. | ad esempio CNN |

## Riferimenti API {#api-ref}

Questa sezione presenta l’API responsabile della gestione delle informazioni client quando si utilizzano le API REST o gli SDK di autenticazione Adobe Primetime.

### API REST {#rest-api}

I servizi di autenticazione Adobe Primetime supportano la ricezione delle informazioni sul client nei seguenti modi:

* Come **intestazione: &quot;X-Device-Info&quot;**
* Come **parametro query: &quot;device_info&quot;**
* Come **parametro post: &quot;device_info&quot;**

>[!IMPORTANT]
>
>In tutti e tre gli scenari, il payload dell’intestazione o del parametro deve essere **Codifica Base64 e codifica URL**.

**SDK**

#### SDK JavaScript {#js-sdk}

L&#39;SDK JavaScript di AccessEnabler crea per impostazione predefinita un oggetto JSON di informazioni sul client, che verrà passato ai servizi di autenticazione di Adobe Primetime, a meno che non venga sostituito.

L&#39;SDK JavaScript di AccessEnabler supporta **ignorare** la chiave &quot;applicationId&quot; dall’oggetto JSON di informazioni sul client tramite [setRequestor](/help/authentication/javascript-sdk-api-reference.md#setrequestor(inRequestorID,endpoints,options))s *applicationId* parametro options .

>[!CAUTION]
>
>La `applicationId` Il valore del parametro deve essere un valore String di testo normale.
>Nel caso in cui l&#39;applicazione Programmer decida di passare l&#39;applicationId, il resto delle chiavi di informazioni client sarà ancora calcolato dall&#39;SDK JavaScript di AccessEnabler.

#### SDK iOS/tvOS {#ios-tvos-sdk}

L&#39;SDK iOS/tvOS di AccessEnabler crea per impostazione predefinita un oggetto JSON di informazioni sul client, che verrà passato ai servizi di autenticazione di Adobe Primetime, a meno che non venga sostituito.

L&#39;SDK di AccessEnabler per iOS/tvOS supporta **sovrascrivere l&#39;insieme** informazioni sul client oggetto JSON tramite [setOptions](/help/authentication/iostvos-sdk-api-reference.md#setoptions)Parametro device_info di .

>[!CAUTION]
>
>La *device_info* il valore del parametro deve essere un **Codifica Base64** *NSString* valore.
>
>Nel caso in cui l&#39;applicazione del programmatore decida di passare il *device_info*, tutte le chiavi di informazioni client calcolate dall&#39;SDK iOS/tvOS di AccessEnabler avranno la priorità. Pertanto, è molto importante calcolare e trasmettere i valori per il maggior numero possibile di chiavi. Per ulteriori dettagli sull’implementazione, consulta la sezione [Panoramica](#pass-client-info-overview) la tabella e [Guida di riferimento rapido per iOS/tvOS](#ios-tvos).

#### SDK per Android/FireOS {#and-fire-os-sdk}

La `AccessEnabler` L&#39;SDK per Android/FireOS crea per impostazione predefinita un oggetto JSON di informazioni sul client, che verrà passato ai servizi di autenticazione di Adobe Primetime, a meno che non venga ignorato.

La `AccessEnabler` L&#39;SDK per Android/FireOS supporta **sovrascrivere l&#39;insieme** informazioni sul client oggetto JSON tramite [setOptions](/help/authentication/android-sdk-api-reference.md#setOptions)&#39;s/[setOptions](/help/authentication/amazon-fireos-native-client-api-reference.md#fire_setOption)s `device_info` parametro .

>[!NOTE]
>
>La `device_info` il valore del parametro deve essere un **Codifica Base64** Valore stringa.

>[!IMPORTANT]
>
>Nel caso in cui l&#39;applicazione del programmatore decida di passare il `device_info`, quindi tutte le chiavi di informazioni client calcolate dal `AccessEnabler` L’SDK per Android/FireOS verrà ignorato. Pertanto, è molto importante calcolare e trasmettere i valori per il maggior numero possibile di chiavi. Per ulteriori dettagli sull’implementazione, consulta la sezione [Panoramica](#pass-client-info-overview) la tabella e [Android](#android) e [FireOS](#fire-tv) libro di cucina.

## Cookie {#cookbooks}

In questa sezione viene presentato un cookie per la creazione di oggetti JSON per le informazioni sul client nel caso di diversi tipi di dispositivi.

>[!IMPORTANT]
>
>Le chiavi contrassegnate con  **!** sono obbligatori da inviare.

### Android {#android}

Le informazioni sul dispositivo possono essere costruite nel modo seguente:

|  | Chiave | Origine | Valore (esempio) |
|---|---------------|-----------------------------|---------------|
| ! | model | Build.MODEL | GT-I9505 |
|  | fornitore | Build.BRAND | samsung |
|  | produttore | Build.MANUFACTURER | samsung |
| ! | version | Build.DEVICE | battito |
|  | displayWidth | DisplayMetrics.widthPixels | 600 |
|  | displayHeight | DisplayMetrics.heightPixels | 800 |
| ! | osName | hardcoded | Android |
| ! | osVersion | Build.VERSION.RELEASE | 5.0.1 |

Le informazioni di connessione possono essere costruite nel modo seguente:

|  | Chiave | Origine | Valore (esempio) |
|---|---|---|---|
| ! | connectionType | `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>` `getSystemService(Context.CONNECTIVITY_SERVICE).getActiveNetworkInfo().getType()` | `"WIFI","BLUETOOTH","MOBILE","ETHERNET","VPN","DUMMY","MOBILE_DUN","WIMAX","notAccessible"` |
|  | connectionSecure |  |  |

Le informazioni sull&#39;applicazione possono essere costruite nel modo seguente:

|  | Chiave | Origine | Valore (esempio) |
|---|---------------|-----------|--------------|
|  | applicationId | hardcoded | CNN |

>[!IMPORTANT]
Le informazioni sulla periferica, sulla connessione e sull&#39;applicazione devono essere aggiunte allo stesso oggetto JSON. Successivamente, l&#39;oggetto risultante deve essere **Codifica Base64**. Inoltre, nel caso delle API REST di autenticazione di Adobe Primetime, il valore deve essere **URL codificato**.

**Codice di esempio**

```JAVA
private JSONObject computeClientInformation() {
     String LOGGING_TAG = "DefineClass.class";
  
     JSONObject clientInformation = new JSONObject();

     String connectionType;

     try {
          ConnectivityManager cm = (ConnectivityManager) getContext().getSystemService(CONNECTIVITY_SERVICE);
          NetworkInfo activeNetwork = cm.getActiveNetworkInfo();

          if (activeNetwork != null && activeNetwork.isConnectedOrConnecting()) {
              switch (activeNetwork.getType()) {
                    case ConnectivityManager.TYPE_WIFI: {
                        connectionType = "WIFI";
                        break;
                    }
                    case ConnectivityManager.TYPE_BLUETOOTH: {
                        connectionType = "BLUETOOTH";
                        break;
                    }
                    case ConnectivityManager.TYPE_MOBILE: {
                        connectionType = "MOBILE";
                        break;
                    }
                    case ConnectivityManager.TYPE_ETHERNET: {
                        connectionType = "ETHERNET";
                        break;
                    }
                    case ConnectivityManager.TYPE_VPN: {
                        connectionType = "VPN";
                        break;
                    }
                    case ConnectivityManager.TYPE_DUMMY: {
                        connectionType = "DUMMY";
                        break;
                    }
                    case ConnectivityManager.TYPE_MOBILE_DUN: {
                        connectionType = "MOBILE_DUN";
                        break;
                    }
                    case ConnectivityManager.TYPE_WIMAX: {
                        connectionType = "WIMAX";
                        break;
                    }
                    default:
                       connectionType = ConnectivityManager.EXTRA_OTHER_NETWORK_INFO;
              }
          } else {
                connectionType = ConnectivityManager.EXTRA_NO_CONNECTIVITY;
          }
     } catch (Exception e) {
          connectionType = "notAccessible";
     }

     try {
          clientInformation.put("model",Build.MODEL);
          clientInformation.put("vendor", Build.BRAND);
          clientInformation.put("manufacturer",Build.MANUFACTURER);
          clientInformation.put("version",Build.DEVICE);
          clientInformation.put("osName","Android");
          clientInformation.put("osVersion",Build.VERSION.RELEASE);
          clientInformation.put("connectionType",connectionType);
          clientInformation.put("applicationId","CNN");
     } catch (JSONException e) {
          Log.e(LOGGING_TAG, e.getMessage());
     }

     return Base64.encodeToString(clientInformation.toString().getBytes(), Base64.NO_WRAP);
}
```

>[!NOTE]
**Risorse:**
* classe pubblica [build](https://developer.android.com/reference/android/os/Build.html){target=_blank} nella documentazione per gli sviluppatori Java.


### FireTV {#fire-tv}

Le informazioni sul dispositivo possono essere costruite nel modo seguente:

|  | Chiave | Origine | Valore (ad esempio) |
|---|---------------|-----------------------------|--------------|
| ! | model | Build.MODEL | AFTM |
|  | fornitore | Build.BRAND | Amazon |
|  | produttore | Build.MANUFACTURER | Amazon |
| ! | version | Build.DEVICE | montoya |
|  | displayWidth | DisplayMetrics.widthPixels |  |
|  | displayHeight | DisplayMetrics.heightPixels |  |
| ! | osName | hardcoded | Android |
| ! | osVersion | Build.VERSION.RELEASE | 5.1.1 |

Le informazioni di connessione possono essere costruite nel modo seguente:

|  | Chiave | Origine | Valore (esempio) |
|---|------------------|--------|---------------|
| ! | connectionType |  |  |
|  | connectionSecure |  |  |

Le informazioni sull&#39;applicazione possono essere costruite nel modo seguente:

|  | Chiave | Origine | Valore (esempio) |
|---|---------------|-----------|--------------|
|  | applicationId | hardcoded | CNN |

>[!IMPORTANT]
Le informazioni sulla periferica, sulla connessione e sull&#39;applicazione devono essere aggiunte allo stesso oggetto JSON. Successivamente, l&#39;oggetto risultante deve essere **Codifica Base64**. Inoltre, nel caso delle API REST di autenticazione di Adobe Primetime, il valore deve essere **URL codificato**.

>[!NOTE]
**Risorse:**
* classe pubblica [Crea](https://developer.android.com/reference/android/os/Build.html){target=_blank} nella documentazione per gli sviluppatori Android.
* [Identificazione di dispositivi FireTV](https://developer.amazon.com/docs/fire-tv/identify-amazon-fire-tv-devices.html){target=_blank}


### iOS/tvOS {#ios-tvos}

Le informazioni sul dispositivo possono essere costruite nel modo seguente:

|  | Chiave | Origine | Valore (esempio) |
|---|---------------|------------------------|--------------|
| ! | model | uname.machine | iPhone |
|  | fornitore | hardcoded | Apple |
|  | produttore | hardcoded | Apple |
| ! | version | uname.machine | 8,1 |
|  | displayWidth | UIScreen.mainScreen | 320 |
|  | displayHeight | UIScreen.mainScreen | 568 |
| ! | osName | UIDevice.systemName | iOS |
| ! | osVersion | UIDevice.systemVersion | 10.2 |

Le informazioni di connessione possono essere costruite nel modo seguente:

|  | Chiave | Origine | Valore (esempio) |
|---|------------------|-------------------------------------------|--------------|
| ! | connectionType | [Reachability currentReachabilityStatus] |  |
|  | connectionSecure |  |  |


Le informazioni sull&#39;applicazione possono essere costruite nel modo seguente:

|  | Chiave | Origine | Valore (esempio) |
|---|---------------|-----------|--------------|
|  | applicationId | hardcoded | CNN |

>[!IMPORTANT]
Le informazioni sulla periferica, sulla connessione e sull&#39;applicazione devono essere aggiunte allo stesso oggetto JSON. Successivamente, l&#39;oggetto risultante deve essere codificato in Base64. Inoltre, nel caso delle API REST di autenticazione di Adobe Primetime, il valore deve essere codificato in URL.

**Codice di esempio**

```C
+ (NSString *)computeClientInformation {        
        struct utsname u;
        uname(&u);

        NSString *hardware = [NSString stringWithCString:u.machine encoding:NSUTF8StringEncoding];

        UIDevice *device = [UIDevice currentDevice];

        NSString *deviceType;

        switch (UI_USER_INTERFACE_IDIOM()) {
            case UIUserInterfaceIdiomPhone:
                deviceType = @"MobilePhone";
                break;
            case UIUserInterfaceIdiomPad:
                deviceType = @"Tablet";
                break;
            case UIUserInterfaceIdiomTV:
                deviceType = @"TV";
                break;
            default:
                deviceType = @"Unknown";
        }

        CGRect screenRect = [[UIScreen mainScreen] bounds];
        NSNumber *screenWidth = @((float) screenRect.size.width);
        NSNumber *screenHeight = @((float) screenRect.size.height);

        Reachability *reachability = [Reachability reachabilityForInternetConnection];
        [reachability startNotifier];

        NetworkStatus status = [reachability currentReachabilityStatus];

        NSString *connectionType;

        if (status == NotReachable) {
            connectionType = @"notConnected";
        } else if (status == ReachableViaWiFi) {
            connectionType = @"WiFi";
        } else if (status == ReachableViaWWAN) {
            connectionType = @"cellular";
        }

        NSMutableDictionary *clientInformation = [@{
                @"type": deviceType,
                @"model": device.model,
                @"vendor": @"Apple",
                @"manufacturer": @"Apple",
                @"version": [hardware stringByReplacingOccurrencesOfString:device.model withString:@""],
                @"osName": device.systemName,
                @"osVersion": device.systemVersion,
                @"displayWidth": screenWidth,
                @"displayHeight": screenHeight,
                @"connectionType": connectionType,
                @"applicationId": @"CNN" 
        } mutableCopy];

        NSError *error;
        NSData *jsonData = [NSJSONSerialization dataWithJSONObject:clientInformation options:NSJSONWritingPrettyPrinted error:&error];
        NSString *base64Encoded = [jsonData base64EncodedStringWithOptions:0];

        return base64Encoded;
}
```

>[!NOTE]
**Risorse:**
* [UIDevice](https://developer.apple.com/documentation/uikit/uidevice#//apple_ref/occ/cl/UIDevice){target=_blank}
* [uname](https://man7.org/linux/man-pages/man2/uname.2.html){target=_blank}
* [Informazioni sulla raggiungibilità](https://developer.apple.com/library/archive/samplecode/Reachability/Introduction/Intro.html){target=_blank}


### Roku {#roku}

Le informazioni sul dispositivo possono essere costruite nel modo seguente:

| Chiave | Origine | Valore (esempio) |  |
|-----|---------------|--------------------------------------------|-----------------|
| ! | model | hardcoded | &quot;Roku&quot; |
|  | fornitore | ifDeviceInfo.GetModelDetails().VendorName | &quot;Sharp&quot;, &quot;Roku&quot; |
|  | produttore | ifDeviceInfo.GetModelDetails().VendorName | &quot;Sharp&quot;, &quot;Roku&quot; |
| ! | version | ifDeviceInfo.GetModelDetails().ModelNumber | &quot;5303X&quot; |
|  | displayWidth | ifDeviceInfo.GetDisplaySize().w | 1920 |
|  | displayHeight | ifDeviceInfo.GetDisplaySize().h | 1080 |
| ! | osName | hardcoded | &quot;Roku&quot; |
| ! | osVersion | ifDeviceInfo.getVersion() |  |

Le informazioni di connessione possono essere costruite nel modo seguente:

|  | Chiave | Origine | Valore (esempio) |
|---|---|---|---|
| ! | connectionType | ifDeviceInfo.GetConnectionType() | &quot;WifiConnection&quot;, &quot;WiredConnection&quot; |
|  | connectionSecure | hardcoded | true se la connessione è cablata |

Le informazioni sull&#39;applicazione possono essere costruite nel modo seguente:

|  | Chiave | Origine | Valore (esempio) |
|---|---------------|-----------|--------------|
|  | applicationId | hardcoded | CNN |

>[!IMPORTANT]
Le informazioni sulla periferica, sulla connessione e sull&#39;applicazione devono essere aggiunte allo stesso oggetto JSON. Successivamente, l&#39;oggetto risultante deve essere **Codifica Base64**. Inoltre, nel caso delle API REST di autenticazione di Adobe Primetime, il valore deve essere codificato in URL.

>[!NOTE]
Per ulteriori informazioni, consulta [ifDeviceInfo](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md)

### XBOX 1/360 {#xbox}

Le informazioni sul dispositivo possono essere costruite nel modo seguente:

|  | Chiave | Origine | Valore (esempio) |
|---|---|---|---|
| ! | model | EasClientDeviceInformation.SystemProductName |  |
|  | fornitore | hardcoded | Microsoft |
|  | produttore | hardcoded | Microsoft |
| ! | version | EasClientDeviceInformation.SystemHardwareVersion |  |
|  | displayWidth | DisplayInformation.ScreenWidthInRawPixels | 1920 |
|  | displayHeight | DisplayInformation.ScreenHeightInRawPixels | 1080 |
| ! | osName | EasClientDeviceInformation.OperatingSystem |  |
| ! | osVersion | EasClientDeviceInformation.SystemFirmwareVersion |  |

Le informazioni di connessione possono essere costruite nel modo seguente:

|  | Chiave | Origine | Esempio |
|---|---|---|---|
| ! | connectionType |  |  |
|  | connectionSecure | TipoAutenticazioneRete | &quot;None&quot;, &quot;Wpa&quot; ecc |

Le informazioni sull&#39;applicazione possono essere costruite nel modo seguente:

| Chiave | Origine | Valore (esempio) |
|---|---|---|
| applicationId | hardcoded | CNN |

>[!IMPORTANT]
Le informazioni sulla periferica, sulla connessione e sull&#39;applicazione devono essere aggiunte allo stesso oggetto JSON. Successivamente, l&#39;oggetto risultante deve essere **Codifica Base64**. Inoltre, nel caso delle API REST di autenticazione di Adobe Primetime, il valore deve essere **URL codificato**.

**Risorse**

* [Classe EasClientDeviceInformation](https://docs.microsoft.com/en-us/uwp/api/windows.security.exchangeactivesyncprovisioning.easclientdeviceinformation?view=winrt-22000)
* [Classe DisplayInformation](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.display.displayinformation?view=winrt-22000)


