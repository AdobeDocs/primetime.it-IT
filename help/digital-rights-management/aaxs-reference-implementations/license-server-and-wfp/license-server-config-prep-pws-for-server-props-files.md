---
seo-title: Preparazione delle password per i file delle proprietà del server
title: Preparazione delle password per i file delle proprietà del server
uuid: 2d876eb0-b1a5-4c30-ae96-0a22f6a03910
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Preparazione delle password per i file delle proprietà del server {#preparing-passwords-for-the-server-properties-files}

Per garantire la sicurezza della password della credenziale, viene fornito uno strumento per cifrare la password prima di inserirla nel [!DNL flashaccess-refimpl.properties] file o [!DNL flashaccess-refimpl-packager.properties] .

Per eseguire lo strumento utilizzando lo script ANT fornito:

* Vai a *`<Reference Implementation Server Path>`*[!DNL \refimpl]

* Assicurati che la `sdkdir` proprietà sia indicata in [!DNL build-refimpl.xml] punti alla directory contenente l’SDK di Adobe Access
* Eseguite il comando seguente utilizzando ANT:

   ```
       ant -f build-refimpl.xml
   ```

* Quando richiesto, digitare la password della credenziale

Per eseguire lo strumento utilizzando Java:

* Vai a *`<Reference Implementation Server Path>`*\ [!DNL scrambler]

* Dal prompt dei comandi, immettere il comando:

* In Windows:

   ```
   java -classpath path_to_adobe-flashaccess-sdk.jar;.  
   com.adobe.flashaccess.refimpl.util.ScrambleUtil your_pfx_password
   ```

* In Linux:

   ```
       java -classpath path_to_adobe-flashaccess-sdk.jar;.  
       com.adobe.flashaccess.refimpl.util.ScrambleUtil your_pfx_password
   ```

L&#39;utilità genera la password crittografata, che è necessario copiare nel file .properties.

>[!NOTE]
>
>Le password codificate tramite l&#39;utilità di scorrimento password fornita con l&#39;implementazione del riferimento non funzioneranno con Adobe Access Server per lo streaming protetto.
