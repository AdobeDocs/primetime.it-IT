---
description: ' Adobe Offline Packager accetta come input contenuto mp4 non crittografato.'
seo-description: ' Adobe Offline Packager accetta come input contenuto mp4 non crittografato.'
seo-title: Creare pacchetti con  Adobe Offline Packager
title: Creare pacchetti con  Adobe Offline Packager
uuid: d0676147-c20f-49ea-93a6-9c8dbbbba992
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# Creare pacchetti con  Adobe Offline Packager{#package-your-content-with-adobe-offline-packager}

 Adobe Offline Packager accetta come input contenuto mp4 non crittografato.

**Chiamata  Adobe Offline Packager**

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

In questo caso particolare, il packager offline aggiunge sia la protezione del contenuto Widevine che i dati di inizializzazione della protezione del contenuto PlayReady al contenuto DASH di output. Il valore di `-key_file_path` corrisponde a una chiave con codifica base64. Il valore di `-playready_LA_URL` è relativo all&#39;acquisizione della licenza PlayReady.

L&#39;argomento conf_path punta al file di configurazione che contiene quanto segue:

    &lt;config>
    &lt;frag_dur>4&lt;/frag_dur>
    &lt;target_dur>6 &lt;/target_dur>
    &lt;encrypt_audio>false&lt;/encrypt_audio>
    &lt;/config>

Perché alcuni dispositivi Android — principalmente  Amazon Fire TV — non supportano la decrittazione audio, la crittografia audio è facoltativa.
