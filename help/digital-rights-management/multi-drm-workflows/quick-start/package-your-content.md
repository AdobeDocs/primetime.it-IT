---
description: Il packaging dei contenuti è il processo di preparazione dei contenuti video per la riproduzione sul web. Il packaging include la trasformazione di video non elaborati in file manifest e, facoltativamente, la cifratura del contenuto utilizzando diverse soluzioni DRM per diversi dispositivi e browser.
title: Creare pacchetti per i contenuti
exl-id: d6f922d6-afec-4314-a01e-b951c1f8a7e8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---

# Creare pacchetti per i contenuti {#package-your-content}

Il packaging dei contenuti è il processo di preparazione dei contenuti video per la riproduzione sul web. Il packaging include la trasformazione di video non elaborati in file manifest e, facoltativamente, la cifratura del contenuto utilizzando diverse soluzioni DRM per diversi dispositivi e browser.

Per preparare il contenuto, è possibile utilizzare Adobe Offline Packager o altri strumenti come Bento4 Packager di ExpressPlay. I package preparano il video per la riproduzione (ad esempio, frammentando il file originale e inserendolo in un manifesto) e lo proteggono con la soluzione DRM scelta (PlayReady, Widevine, FairPlay, Access, ecc.):

* [Packager offline Adobe](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf)
* [Pacchetti ExpressPlay](https://www.expressplay.com/developer/packaging-tools/)

<!--<a id="fig_jbn_fw5_xw"></a>-->

![](assets/pkg_lic_play_web.png)

1. Creare un pacchetto o ottenere in altro modo il contenuto da utilizzare per testare la configurazione.

   Uno dei punti cruciali da ricordare per la creazione del pacchetto è che l’ID chiave (ID contenuto) utilizzato in questa fase di creazione del pacchetto è lo stesso che devi fornire nella successiva richiesta del token di licenza. L&#39;ID chiave è l&#39;unico elemento che identifica il codice CEK (che può essere memorizzato nel proprio database di gestione delle chiavi o memorizzato utilizzando [Servizio di archiviazione delle chiavi di ExpressPlay](https://www.expressplay.com/developer/key-storage/).

   >[!NOTE]
   >
   >Per chi ha familiarità con l’accesso agli Adobi, si tratta di una differenza importante nel funzionamento delle diverse soluzioni. In Access, la chiave di licenza viene incorporata nei metadati DRM e trasmessa avanti e indietro con il contenuto protetto. Nei sistemi Multi-DRM qui descritti, la Licenza effettiva non viene passata, ma memorizzata in modo sicuro ed ottenuta tramite l&#39;ID chiave.

<!--<a id="example_52AF76B730174B79B6088280FCDF126D"></a>-->

Di seguito è riportato un esempio di creazione di pacchetti utilizzando Adobe Offline Packager per Widevine. Il Packager utilizza un file di configurazione (ad esempio, [!DNL widevine.xml]), che si presenta così:

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

* `in_path` - Questa voce punta alla posizione del video sorgente sul vostro confezionatore locale.
* `out_type` - Questa voce descrive il tipo di output del pacchetto, in questo caso DASH (per la protezione Widevine su HTML5).
* `out_path` : la posizione sul computer locale in cui desideri spostare l’output.
* `drm_sys` - La soluzione DRM per la quale si sta effettuando il packaging. Questo sarà o `widevine`, `fairplay`, o `playready`.

* `frag_dur` e `target_dur` sono voci di durata specifiche per DASH relative alla riproduzione di video.

* `key_file_path` : si tratta della posizione del file di licenza sul computer di creazione pacchetti che funge da chiave di crittografia del contenuto (CEK). È una stringa esadecimale a 16 byte con codifica Base-64.
* `widevine_content_id` - Questo è Widevine &quot;boilerplate&quot;; è sempre `2a`. (Non confondere questo con il `widevine_key_id`.)

* `widevine_provider` - Per i nostri scopi, imposta sempre questo su `intertrust`.

* `widevine_key_id` - Identificatore della licenza specificata nell&#39; `key_file_path` voce. In altre parole, questo identifica la chiave utilizzata per crittografare il contenuto. Questo ID è una stringa HEX a 16 byte che crei tu stesso.

Come indicato nella [Documentazione di Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf), &quot;Come best practice, crea un file di configurazione contenente le opzioni comuni che desideri utilizzare per generare gli output. Quindi, crea l’output fornendo opzioni specifiche come argomento della riga di comando.&quot; In questo caso, il file di configurazione è abbastanza completo e puoi creare l’output nel modo seguente:

```
java -jar OfflinePackager.jar -conf_path widevine.xml -out_path test_dash/ 
```

>[!NOTE]
>
>I parametri della riga di comando hanno la precedenza sui parametri del file di configurazione. In questo esempio, tutto ciò che è necessario si trova nel file di configurazione, ma è stato sostituito il percorso di output specificato nel file di configurazione con `-out_path test_dash/`.
