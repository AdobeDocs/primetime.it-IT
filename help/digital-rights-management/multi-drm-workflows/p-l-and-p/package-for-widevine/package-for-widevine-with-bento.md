---
description: Utilizziamo sia il Packager Bento4 che il Packager offline Adobe per creare contenuti DASH crittografati. Bento4 accetta come input contenuto mp4 non crittografato.
title: Creare pacchetti di contenuti con Bento4
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# Creazione di pacchetti di contenuti per Widevine e PlayReady {#package-for-widevine}

Utilizziamo sia il Packager Bento4 che il Packager offline Adobe per creare contenuti DASH crittografati. Bento4 accetta come input contenuto mp4 non crittografato.

## Creare pacchetti di contenuti con Bento4{#package-your-content-with-bento}

Il packager Bento4 prevede che l&#39;input mp4 sia pre-frammentato. La distribuzione Bento4 Packager include uno strumento per questo.

**Chiamata Bento4**

Le chiamate Bento4 Packager tipiche sono simili agli esempi seguenti:

```
./mp4dash
-f
--use-segment-list
--use-segment-timeline
--subtitles
--encryption-key=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8cd09fc0747c7c5ac215b3b
--widevine
--widevine-header=provider:intertrust#content_id:2a "CC_300_640x360.mp4"
-o "CC_300_640x360_DASH"
```

```
./mp4dash
-f
--use-segment-list
--use-segment-timeline
--subtitles
--encryption-key=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8cd09fc0747c7c5ac215b3b
--playready
--playready-header=\"LA_URL:http://pr.test.expressplay.com/playready/RightsManager.asmx\"
```

L&#39;esempio seguente combina gli schemi PlayReady e Widevine. In questo caso particolare, l&#39;autore del pacchetto sta aggiungendo al contenuto DASH di output sia i dati di inizializzazione della protezione dei contenuti Widevine che quelli della protezione dei contenuti PlayReady.

```
/mp4dash
-f
--use-segment-list
--use-segment-timeline
--subtitles
--encryption-key=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8cd09fc0747c7c5ac215b3b
--playready
--playready-header=\"LA_URL:http://pr.test.expressplay.com/playready/RightsManager.asmx\"
--widevine
--widevine-header=provider:intertrust#content_id:2a "CC_300_640x360.mp4"
-o "CC_300_640x360_DASH"
```

dove

Il valore per `--encryption-key` il contrassegno è nel modulo `<base16 encoded key id>:<base16 encoded encryption key>`.

Il `--widevine-header=provider:intertrust#content_id:2a` Questo flag indica al packager di includere la casella pssh nel manifesto, che TVSDK attualmente richiede per la riproduzione.

Il valore per `-playready-header` è per l&#39;acquisizione con licenza PlayReady.

## Creare un pacchetto dei contenuti con Adobe Offline Packager {#package-your-content-with-adobe-offline-packager}

Adobe Offline Packager prende come input il contenuto mp4 non crittografato.

**Adobe chiamante Offline Packager**

Una tipica chiamata a Adobe Offline Packager è simile alla chiamata seguente:

```
java -jar OfflinePackager.jar -conf_path Content_PR_WV.xml -in_path "Jaigo.mp4"
-out_path "Jaigo_DASH"
-key_file_path "Jaigo_DASH/_info/key.B64.random"
-widevine_key_id c595f214d84dc7ecf31a8ebf1b7ddda5
-widevine_provider intertrust
-playready_LA_URL
http://pr.test.expressplay.com/playready/RightsManager.asmx
-playready_keyid c595f214d84dc7ecf31a8ebf1b7ddda5
-content_id c595f214d84dc7ecf31a8ebf1b7ddda5
```

In questo caso particolare, l&#39;utilità di creazione pacchetti offline sta aggiungendo sia dati di protezione dei contenuti Widevine che dati di inizializzazione della protezione dei contenuti PlayReady al contenuto DASH di output. Il valore di `-key_file_path` è per una chiave con codifica base64. Il valore di `-playready_LA_URL` è per l&#39;acquisizione con licenza PlayReady.

L&#39;argomento conf_path punta al file di configurazione che conterrà quanto segue:

```
<config>
<frag_dur>4</frag_dur>
<target_dur>6</target_dur>
<encrypt_audio>false</encrypt_audio>
</config>
```

Poiché alcuni dispositivi Android, principalmente Amazon Fire TV, non supportano la decrittografia audio, la crittografia audio è opzionale.
