---
description: Utilizziamo sia il packager Bento4 che il packager Adobe offline per creare contenuto DASH crittografato. Bento4 prende come input contenuto mp4 non crittografato.
seo-description: Utilizziamo sia il packager Bento4 che il packager Adobe offline per creare contenuto DASH crittografato. Bento4 prende come input contenuto mp4 non crittografato.
seo-title: Pacchetto dei contenuti con Bento4
title: Pacchetto dei contenuti con Bento4
uuid: 88323a4e-d0b5-4a41-acec-7126d3e0c90b
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c

---


# Creazione di pacchetti di contenuti per Widevine e PlayReady {#package-for-widevine}

Utilizziamo sia il packager Bento4 che il packager Adobe offline per creare contenuto DASH crittografato. Bento4 prende come input contenuto mp4 non crittografato.

## Pacchetto dei contenuti con Bento4{#package-your-content-with-bento}

Il packager Bento4 prevede la pre-frammentazione dell&#39;input mp4. La distribuzione del packager Bento4 include uno strumento per questo.

**Chiamata Bento4**

Le tipiche chiamate per il packager Bento4 sono simili a quelle di seguito:

    ./mp4dash
    -f
    —use-segment-list
    —use-segment-timeline
    —sottotitoli
    —key-key=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8cd09cd fc0747c7c5ac215b3b
    —widevine
    —widevine-header=provider:intertrust#content_id:2a &quot;CC_300_640x360.mp4&quot;
    -o &quot;CC_300_640x360 ASH&quot;
>
    ./mp4dash
    -f
    —use-segment-list
    —use-segment-timeline
    —sottotitoli
    —key-key=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8cd09cd fc0747c7c5ac215b3b
    —playready
    —playready-header=\&quot;LA_URL:http://pr.test.expressplay.com/playready/RightsManager.asmx\&quot;

L&#39;esempio seguente combina gli schemi PlayReady e Widevine. In questo caso particolare, il packager sta aggiungendo sia la protezione del contenuto Widevine che i dati di inizializzazione della protezione del contenuto PlayReady al contenuto DASH di output.

    /mp4dash
    -f
    —use-segment-list
    —use-segment-timeline
    —sottotitoli
    —key-key=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8cd09cd fc0747c7c5ac215b3b
    —playready
    —playready-header=\&quot;LA_URL:http://pr.test.expressplay.com/playready/RightsManager.asmx\&quot;
    —widevine
    —widevine-header=provider:intertrust#content_id:2a &quot;CC_300_640x360.mp4&quot;
    
    
    -o_300_640x360_DASH&quot;dove

Il valore del `--encryption-key` flag è nel modulo `<base16 encoded key id>:<base16 encoded encryption key>`.

Il `--widevine-header=provider:intertrust#content_id:2a` flag indica al packager di includere la casella pssh nel manifesto, che TVSDK richiede attualmente per la riproduzione.
Il valore per `-playready-header` è per l&#39;acquisizione della licenza PlayReady.

## Creare pacchetti di contenuti con Adobe Offline Packager {#package-your-content-with-adobe-offline-packager}

Adobe Offline Packager acquisisce come contenuto mp4 non crittografato di input.

**Chiamata di Adobe Offline Packager**

Una tipica chiamata adobe offline packager avrà l&#39;aspetto della chiamata di seguito:

    java -jar OfflinePackager.jar -conf_path Content_PR_WV.xml -in_path &quot;Jaigo.mp4&quot;
    -out_path &quot;Jaigo_DASH&quot;
    -key_file_path &quot;Jaigo_DASH/_info/key.B64.random&quot;
    -widevine_key_id c595f214d84dc7ecf3 1a8ebf1b7ddda5
    -widevine_provider intertrust
    -playready_LA_
    URLhttp://pr.test.expressplay.com/playready/RightsManager.asmx
    -playready_keyid c595f214d84dc7ecf31a8ebf1b7dda5
    -content_id c595f211 4d84dc7ecf31a8ebf1b7ddda5

In questo caso particolare, il packager offline aggiunge sia la protezione del contenuto Widevine che i dati di inizializzazione della protezione del contenuto PlayReady al contenuto DASH di output. Il valore di `-key_file_path` è per una chiave con codifica base64. Il valore di `-playready_LA_URL` è per l&#39;acquisizione della licenza PlayReady.

L&#39;argomento conf_path punta al file di configurazione che contiene quanto segue:

    &lt;config>
    &lt;frag_dur>4&lt;/frag_dur>
    &lt;target_dur>6&lt;/target_dur>
    &lt;encrypt_audio>false&lt;/encrypt_audio>
    &lt;/config>

Perché alcuni dispositivi Android — principalmente Amazon Fire TV — non supportano la decrittazione audio, la crittografia audio è facoltativa.