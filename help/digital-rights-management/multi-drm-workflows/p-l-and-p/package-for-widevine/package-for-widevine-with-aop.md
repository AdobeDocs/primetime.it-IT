---
description: Adobe Offline Packager prende come input il contenuto mp4 non crittografato.
title: Creare un pacchetto dei contenuti con Adobe Offline Packager
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Creare un pacchetto dei contenuti con Adobe Offline Packager{#package-your-content-with-adobe-offline-packager}

Adobe Offline Packager prende come input il contenuto mp4 non crittografato.

**Adobe chiamante Offline Packager**

Una tipica chiamata a Adobe Offline Packager è simile alla chiamata seguente:

    java -jar OfflinePackager.jar -conf_path Content_PR_WV.xml -in_path &quot;Jaigo.mp4&quot;
    -out_path &quot;Jaigo_DASH&quot;
    -key_file_path &quot;Jaigo_DASH/_info/key.B64.random&quot;
    -widevine_key_id c595f214d84dc7ecf31a8ebf1b7ddda5
    -intertrust widevine_provider
    -playready_LA_URL
    http://pr.test.expressplay.com/playready/RightsManager.asmx
    -playready_keyid c595f214d84dc7ecf31a8ebf1b7ddda5
    -content_id c595f214d84dc7ecf31a8ebf1b7ddda5

In questo caso particolare, l&#39;utilità di creazione pacchetti offline sta aggiungendo sia dati di protezione dei contenuti Widevine che dati di inizializzazione della protezione dei contenuti PlayReady al contenuto DASH di output. Il valore di `-key_file_path` è per una chiave con codifica base64. Il valore di `-playready_LA_URL` è per l&#39;acquisizione con licenza PlayReady.

L&#39;argomento conf_path punta al file di configurazione che conterrà quanto segue:

    &lt;config>
    &lt;frag_dur>4&lt;/frag_dur>
    &lt;target_dur>6&lt;/target_dur>
    &lt;encrypt_audio>false&lt;/encrypt_audio>
    &lt;/config>

Poiché alcuni dispositivi Android, principalmente Amazon Fire TV, non supportano la decrittografia audio, la crittografia audio è opzionale.
