---
title: Preparazione delle password per i file delle proprietà del server
description: Preparazione delle password per i file delle proprietà del server
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# Preparazione delle password per i file delle proprietà del server {#preparing-passwords-for-the-server-properties-files}

Per garantire la protezione della password della credenziale, viene fornito uno strumento per crittografare la password prima che venga immessa nel [!DNL flashaccess-refimpl.properties] o [!DNL flashaccess-refimpl-packager.properties] file.

Per eseguire lo strumento utilizzando lo script ANT fornito:

* Vai a *`<Reference Implementation Server Path>`* [!DNL \refimpl]

* Assicurati che `sdkdir` proprietà in [!DNL build-refimpl.xml] punta alla directory contenente l’SDK di accesso agli Adobi
* Esegui il comando seguente utilizzando ANT:

  ```
      ant -f build-refimpl.xml
  ```

* Quando richiesto, digitare la password delle credenziali

Per eseguire lo strumento utilizzando Java:

* Vai a *`<Reference Implementation Server Path>`*\ [!DNL scrambler]

* Dal prompt dei comandi immettere il comando:

* In Windows:

  ```
  java -classpath path_to_adobe-flashaccess-sdk.jar;.  
  com.adobe.flashaccess.refimpl.util.ScrambleUtil your_pfx_password
  ```

* Su Linux:

  ```
      java -classpath path_to_adobe-flashaccess-sdk.jar;.  
      com.adobe.flashaccess.refimpl.util.ScrambleUtil your_pfx_password
  ```

L&#39;utility restituisce la password crittografata, che è necessario copiare nel file .properties.

>[!NOTE]
>
>Le password codificate mediante l&#39;utilità di scrambling password fornita con l&#39;implementazione di riferimento non funzioneranno con Adobe Access Server for Protected Streaming.
