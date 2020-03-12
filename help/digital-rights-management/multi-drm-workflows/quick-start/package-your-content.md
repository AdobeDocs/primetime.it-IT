---
description: La creazione di pacchetti di contenuti è il processo di preparazione dei contenuti video per la riproduzione sul Web. La creazione di pacchetti include la trasformazione di video non elaborati in file manifest e, facoltativamente, la cifratura del contenuto utilizzando diverse soluzioni DRM per dispositivi e browser diversi.
seo-description: La creazione di pacchetti di contenuti è il processo di preparazione dei contenuti video per la riproduzione sul Web. La creazione di pacchetti include la trasformazione di video non elaborati in file manifest e, facoltativamente, la cifratura del contenuto utilizzando diverse soluzioni DRM per dispositivi e browser diversi.
seo-title: Creazione di pacchetti di contenuti
title: Creazione di pacchetti di contenuti
uuid: b9bc6104-a1ea-4ea0-a0a4-af8a606e5d47
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Creazione di pacchetti di contenuti {#package-your-content}

La creazione di pacchetti di contenuti è il processo di preparazione dei contenuti video per la riproduzione sul Web. La creazione di pacchetti include la trasformazione di video non elaborati in file manifest e, facoltativamente, la cifratura del contenuto utilizzando diverse soluzioni DRM per dispositivi e browser diversi.

Per preparare i contenuti, potete utilizzare Adobe Offline Packager o altri strumenti come il packager ExpressPlay Bento4. I Packager preparano il video per la riproduzione (ad esempio, frammentando il file originale e inserendolo in un manifesto) e proteggono il video con la soluzione DRM scelta (PlayReady, Widevine, FairPlay, Access, ecc.):

* [Adobe Offline Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf)
* [Pacchetti ExpressPlay](https://www.expressplay.com/developer/packaging-tools/)

<!--<a id="fig_jbn_fw5_xw"></a>-->

![](assets/pkg_lic_play_web.png)

1. Creare pacchetti o ottenere altro contenuto da utilizzare per il test della configurazione.

   Uno dei punti cruciali da ricordare per la creazione del pacchetto è che l&#39;ID chiave (ID contenuto) utilizzato in questa fase del pacchetto è lo stesso che dovete fornire nella richiesta successiva di token di licenza. L&#39;ID chiave è l&#39;unico elemento che identifica il CEK (che può essere memorizzato nel database di gestione delle chiavi, o memorizzato utilizzando il servizio [di archiviazione chiavi di](https://www.expressplay.com/developer/key-storage/)ExpressPlay).

   >[!NOTE]
   >
   >Per coloro che hanno familiarità con Adobe Access, questa è una differenza importante nel modo in cui le diverse soluzioni funzionano. In Access, il codice di licenza è incorporato nei metadati DRM e viene trasmesso avanti e indietro con il contenuto protetto. Nei sistemi Multi-DRM qui descritti, la licenza effettiva non viene passata, ma memorizzata in modo sicuro e ottenuta tramite l&#39;ID chiave.

<!--<a id="example_52AF76B730174B79B6088280FCDF126D"></a>-->

Di seguito è riportato un esempio di pacchetto che utilizza Adobe Offline Packager per Widevine. Il Packager utilizza un file di configurazione (ad esempio, [!DNL widevine.xml]) simile al seguente:

```
<config> 
<in_path>sample.mp4</in_path> 
<out_type>dash</out_type> 
<out_path>dash2</out_path> 
<drm/> 
<drm_sys>widevine</drm_sys> 
<frag_dur>4</frag_dur> 
<target_dur>6</target_dur> 
<key_file_path>keyfile.bin</key_file_path> 
<widevine_content_id>2a</widevine_content_id> 
<widevine_provider>intertrust</widevine_provider> 
<widevine_key_id>7debe705d938c76bfd886f077b8fa5f7</widevine_key_id> 
</config>
```

* `in_path` - Questa voce indica la posizione del video sorgente sul computer locale di imballaggio.
* `out_type` - Questa voce descrive il tipo di output del pacchetto, in questo caso DASH (per la protezione Widevine su HTML5).
* `out_path` - La posizione sul computer locale in cui si desidera che l&#39;output venga eseguito.
* `drm_sys` - La soluzione DRM per la quale state creando un pacchetto. Sarà `widevine`, `fairplay`o `playready`.

* `frag_dur` e `target_dur` sono voci di durata specifiche per DASH relative alla riproduzione video.

* `key_file_path` - Si tratta della posizione del file di licenza nel computer in uso che funge da chiave di crittografia del contenuto (CEK). Si tratta di una stringa esadecimale con codifica Base-64 a 16 byte.
* `widevine_content_id` - Questa è Widevine &quot;boilerplate&quot;; è sempre `2a`. (Non confondete con il `widevine_key_id`.)

* `widevine_provider` - Per i nostri scopi, imposta sempre questo a `intertrust`.

* `widevine_key_id` - Identificatore per la licenza specificata nella `key_file_path` voce. In altre parole, identifica la chiave utilizzata per cifrare il contenuto. Si tratta di una stringa HEX a 16 byte che potete creare voi stessi.

Come indicato nella documentazione [di](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf)Packager, &quot;Come procedura ottimale, create un file di configurazione che contenga le opzioni comuni che desiderate utilizzare per generare gli output. Quindi, create l&#39;output fornendo opzioni specifiche come argomento della riga di comando.&quot; In questo caso, il nostro file di configurazione è abbastanza completo, in modo da poter creare l&#39;output come segue:

```
java -jar OfflinePackager.jar -conf_path widevine.xml -out_path test_dash/ 
```

>[!NOTE]
>
>I parametri della riga di comando hanno la precedenza rispetto ai parametri del file di configurazione. In questo esempio, tutto ciò che è necessario è contenuto nel file di configurazione, ma abbiamo sostituito il percorso di output specificato nel file di configurazione con `-out_path test_dash/`.

