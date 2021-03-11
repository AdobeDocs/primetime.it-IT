---
description: Utilizziamo sia il packager Bento4 che il packager offline Adobe per creare contenuti DASH crittografati. Bento4 prende come input contenuto mp4 non crittografato.
title: Pacchetto dei contenuti con Bento4
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---


# Contenuto del pacchetto per Widevine e PlayReady {#package-for-widevine}

Utilizziamo sia il packager Bento4 che il packager offline Adobe per creare contenuti DASH crittografati. Bento4 prende come input contenuto mp4 non crittografato.

## Crea un pacchetto con i contenuti con Bento4{#package-your-content-with-bento}

Il packager Bento4 prevede che l&#39;input mp4 sia pre-frammentato. La distribuzione del packager Bento4 include uno strumento per questo.

**Chiamata a Bento4**

Le chiamate tipiche del packager Bento4 sono simili agli esempi seguenti:

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

L&#39;esempio seguente combina gli schemi PlayReady e Widevine. In questo caso particolare il packager sta aggiungendo sia la protezione del contenuto Widevine che i dati di inizializzazione della protezione del contenuto PlayReady al contenuto DASH di output.

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

Il valore del flag `--encryption-key` si trova nel modulo `<base16 encoded key id>:<base16 encoded encryption key>`.

Il flag `--widevine-header=provider:intertrust#content_id:2a` indica al gestore di pacchetti di includere la casella pssh nel manifesto, che TVSDK attualmente richiede per la riproduzione.

Il valore di `-playready-header` è per l&#39;acquisizione della licenza PlayReady.

## Pacchetto del contenuto con Adobe Offline Packager {#package-your-content-with-adobe-offline-packager}

Adobe Offline Packager prende come input contenuto mp4 non crittografato.

**Chiamata di Adobe Offline Packager**

Una tipica chiamata di adobe offline packager assomiglia alla chiamata di seguito:

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

In questo caso particolare il packager offline sta aggiungendo sia i dati di inizializzazione della protezione del contenuto Widevine che quelli della protezione del contenuto PlayReady al contenuto DASH di output. Il valore di `-key_file_path` è per una chiave con codifica base64. Il valore di `-playready_LA_URL` è per l&#39;acquisizione della licenza PlayReady.

L&#39;argomento conf_path punta al file di configurazione che contiene quanto segue:

```
<config>
<frag_dur>4</frag_dur>
<target_dur>6</target_dur>
<encrypt_audio>false</encrypt_audio>
</config>
```

Poiché alcuni dispositivi Android, principalmente Amazon Fire TV, non supportano la decrittografia audio, la crittografia audio è facoltativa.
