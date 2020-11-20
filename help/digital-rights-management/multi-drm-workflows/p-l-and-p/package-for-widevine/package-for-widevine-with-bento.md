---
description: Utilizziamo sia il packager Bento4 che il packager offline del Adobe  per creare contenuto DASH crittografato. Bento4 prende come input contenuto mp4 non crittografato.
seo-description: Utilizziamo sia il packager Bento4 che il packager offline del Adobe  per creare contenuto DASH crittografato. Bento4 prende come input contenuto mp4 non crittografato.
seo-title: Pacchetto dei contenuti con Bento4
title: Pacchetto dei contenuti con Bento4
uuid: 88323a4e-d0b5-4a41-acec-7126d3e0c90b
translation-type: tm+mt
source-git-commit: 75702ea2a524d7b38bb9ac83cb094c8482b1098f
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# Creazione di pacchetti di contenuti per Widevine e PlayReady {#package-for-widevine}

Utilizziamo sia il packager Bento4 che il packager offline del Adobe  per creare contenuto DASH crittografato. Bento4 prende come input contenuto mp4 non crittografato.

## Pacchetto dei contenuti con Bento4{#package-your-content-with-bento}

Il packager Bento4 prevede la pre-frammentazione dell&#39;input mp4. La distribuzione del packager Bento4 include uno strumento per questo.

**Chiamata Bento4**

Le tipiche chiamate per il packager Bento4 sono simili a quelle di seguito:

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

L&#39;esempio seguente combina gli schemi PlayReady e Widevine. In questo caso particolare, il packager sta aggiungendo sia la protezione del contenuto Widevine che i dati di inizializzazione della protezione del contenuto PlayReady al contenuto DASH di output.

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

Il valore del `--encryption-key` flag è nel modulo `<base16 encoded key id>:<base16 encoded encryption key>`.

Il `--widevine-header=provider:intertrust#content_id:2a` flag indica al packager di includere la casella pssh nel manifesto, che TVSDK richiede attualmente per la riproduzione.

Il valore per `-playready-header` è per l&#39;acquisizione della licenza PlayReady.

## Creare pacchetti con  Adobe Offline Packager {#package-your-content-with-adobe-offline-packager}

 Adobe Offline Packager accetta come input contenuto mp4 non crittografato.

**Chiamata  Adobe Offline Packager**

Una tipica chiamata adobe offline packager avrà l&#39;aspetto della chiamata di seguito:

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

In questo caso particolare, il packager offline aggiunge sia la protezione del contenuto Widevine che i dati di inizializzazione della protezione del contenuto PlayReady al contenuto DASH di output. Il valore di `-key_file_path` è per una chiave con codifica base64. Il valore di `-playready_LA_URL` è per l&#39;acquisizione della licenza PlayReady.

L&#39;argomento conf_path punta al file di configurazione che contiene quanto segue:

```
<config>
<frag_dur>4</frag_dur>
<target_dur>6</target_dur>
<encrypt_audio>false</encrypt_audio>
</config>
```

Perché alcuni dispositivi Android — principalmente  Amazon Fire TV — non supportano la decrittazione audio, la crittografia audio è facoltativa.
