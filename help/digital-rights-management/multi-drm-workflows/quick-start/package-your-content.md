---
description: Il contenuto di imballaggio è il processo di preparazione del contenuto video per la riproduzione sul web. Il pacchetto include la trasformazione di video non elaborati in file manifest e la crittografia del contenuto utilizzando facoltativamente diverse soluzioni DRM per dispositivi e browser diversi.
title: Crea un pacchetto con i contenuti
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---


# Crea un pacchetto per i contenuti {#package-your-content}

Il contenuto di imballaggio è il processo di preparazione del contenuto video per la riproduzione sul web. Il pacchetto include la trasformazione di video non elaborati in file manifest e la crittografia del contenuto utilizzando facoltativamente diverse soluzioni DRM per dispositivi e browser diversi.

Per preparare il contenuto, è possibile utilizzare Adobe Offline Packager o altri strumenti come il packager Bento4 di ExpressPlay. I pacchetti preparano il video per la riproduzione (ad esempio, la frammentazione del file originale e la sua messa in un manifesto) e lo proteggono con la soluzione DRM scelta (PlayReady, Widevine, FairPlay, Access, ecc.):

* [Pacchetto offline Adobe](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf)
* [Pacchetti ExpressPlay](https://www.expressplay.com/developer/packaging-tools/)

<!--<a id="fig_jbn_fw5_xw"></a>-->

![](assets/pkg_lic_play_web.png)

1. Crea un pacchetto o ottenere in altro modo il contenuto da utilizzare per testare la configurazione.

   Uno dei punti cruciali da ricordare per il packaging è che l&#39;ID chiave (ID contenuto) che utilizzi in questo passaggio del pacchetto è lo stesso che devi fornire nella successiva richiesta del token di licenza. L&#39;ID chiave è l&#39;unico elemento che identifica il CEK (che può essere memorizzato nel database di gestione delle chiavi in uso o memorizzato utilizzando [Servizio di archiviazione chiavi ExpressPlay](https://www.expressplay.com/developer/key-storage/).

   >[!NOTE]
   >
   >Per coloro che hanno familiarità con Adobe Access, questa è una differenza importante nel funzionamento delle diverse soluzioni. In Access, il codice di licenza è incorporato nei metadati DRM e trasmesso avanti e indietro con il contenuto protetto. Nei sistemi Multi-DRM qui descritti, la Licenza effettiva non viene passata, ma memorizzata in modo sicuro e ottenuta tramite l’ID chiave.

<!--<a id="example_52AF76B730174B79B6088280FCDF126D"></a>-->

Ecco un esempio di imballaggio che utilizza Adobe Offline Packager per Widevine. Il Packager utilizza un file di configurazione (ad esempio, [!DNL widevine.xml]) simile al seguente:

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

* `in_path` - Questa voce indica la posizione del video di origine sulla macchina da imballaggio locale.
* `out_type` - Questa voce descrive il tipo di output imballato, in questo caso DASH (per la protezione Widevine su HTML5).
* `out_path` - La posizione sul computer locale in cui si desidera che l&#39;output venga trasmesso.
* `drm_sys` - La soluzione DRM per la quale stai effettuando il packaging. Sarà `widevine`, `fairplay` o `playready`.

* `frag_dur` e  `target_dur` sono voci di durata specifiche DASH relative alla riproduzione video.

* `key_file_path` - Questo è il percorso del file di licenza sul computer di imballaggio che funge da chiave di crittografia del contenuto (CEK). Si tratta di una stringa esadecimale con codifica Base-64 a 16 byte.
* `widevine_content_id` - Questa è Widevine &quot;calderplate&quot;; lo è sempre  `2a`. (Non confonderlo con il simbolo `widevine_key_id`.)

* `widevine_provider` - Per i nostri scopi, imposta sempre questo a  `intertrust`.

* `widevine_key_id` - Identificatore della licenza specificata nella  `key_file_path` voce. In altre parole, identifica la chiave utilizzata per crittografare il contenuto. Questo ID è una stringa HEX a 16 byte che crei te stesso.

Come indicato nella [Documentazione di Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf), &quot;Come best practice, crea un file di configurazione che contiene le opzioni comuni che desideri utilizzare per generare gli output. Quindi, crea l&#39;output fornendo opzioni specifiche come argomento della riga di comando.&quot; In questo caso, il nostro file di configurazione è abbastanza completo, in modo da poter creare l&#39;output come segue:

```
java -jar OfflinePackager.jar -conf_path widevine.xml -out_path test_dash/ 
```

>[!NOTE]
>
>I parametri della riga di comando hanno la precedenza sui parametri del file di configurazione. In questo esempio, tutto ciò che è necessario è nel file di configurazione, ma abbiamo sostituito il percorso di output specificato nel file di configurazione con `-out_path test_dash/`.

