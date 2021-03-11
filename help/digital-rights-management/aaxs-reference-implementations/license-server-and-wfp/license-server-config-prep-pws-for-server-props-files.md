---
title: Preparazione delle password per i file delle proprietà del server
description: Preparazione delle password per i file delle proprietà del server
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# Preparazione delle password per i file delle proprietà del server {#preparing-passwords-for-the-server-properties-files}

Per garantire la sicurezza della password della credenziale, viene fornito uno strumento per crittografare la password prima di essere inserita nel file [!DNL flashaccess-refimpl.properties] o [!DNL flashaccess-refimpl-packager.properties].

Per eseguire lo strumento utilizzando lo script ANT fornito:

* Vai a *`<Reference Implementation Server Path>`* [!DNL \refimpl]

* Assicurati che la proprietà `sdkdir` in [!DNL build-refimpl.xml] punti alla directory contenente l&#39;SDK di Adobe Access
* Esegui il comando seguente utilizzando ANT:

   ```
       ant -f build-refimpl.xml
   ```

* Quando richiesto, digitare la password della credenziale

Per eseguire lo strumento utilizzando Java:

* Vai a *`<Reference Implementation Server Path>`*\ [!DNL scrambler]

* Dal prompt dei comandi, immetti il comando:

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

L&#39;utilità restituisce la password crittografata, che è necessario copiare nel file .properties .

>[!NOTE]
>
>Le password codificate utilizzando l&#39;utilità di scorrimento delle password fornita con l&#39;implementazione di riferimento non funzioneranno con Adobe Access Server per lo streaming protetto.
