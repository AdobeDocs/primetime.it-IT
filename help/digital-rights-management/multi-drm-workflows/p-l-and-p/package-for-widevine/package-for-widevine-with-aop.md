---
description: Adobe Offline Packager prende come input contenuto mp4 non crittografato.
title: Pacchetto del contenuto con Adobe Offline Packager
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# Pacchetto del contenuto con Adobe Offline Packager{#package-your-content-with-adobe-offline-packager}

Adobe Offline Packager prende come input contenuto mp4 non crittografato.

**Chiamata di Adobe Offline Packager**

Una tipica chiamata di adobe offline packager assomiglia alla chiamata di seguito:

    java -jar OfflinePackager.jar -conf_path Content_PR_WV.xml -in_path &quot;Jaigo.mp4&quot;
    -out_path &quot;Jaigo_DASH&quot;
    -key_file_path &quot;Jaigo_DASH/_info/key.B64.random&quot;
    -widevine_key_id c595f214d84dc7ecf3 1a8ebf1b7dda5
    -widevine_provider intertrust
    -playready_LA_
    URLhttp://pr.test.expressplay.com/playready/RightsManager.asmx
    -playready_keyid c595f214d84dc7ecf31a8ebf1b7dda5
    -content_id c595f211 4d84dc7ecf31a8ebf1b7dda5

In questo caso particolare il packager offline sta aggiungendo sia i dati di inizializzazione della protezione del contenuto Widevine che quelli della protezione del contenuto PlayReady al contenuto DASH di output. Il valore di `-key_file_path` è per una chiave con codifica base64. Il valore di `-playready_LA_URL` è per l&#39;acquisizione della licenza PlayReady.

L&#39;argomento conf_path punta al file di configurazione che contiene quanto segue:

    &lt;config>
    &lt;frag_dur>4&lt;/frag_dur>
    &lt;target_dur>6&lt;/target_dur>
    &lt;encrypt_audio>false&lt;/encrypt_audio>
    &lt;/config>

Poiché alcuni dispositivi Android, principalmente Amazon Fire TV, non supportano la decrittografia audio, la crittografia audio è facoltativa.
