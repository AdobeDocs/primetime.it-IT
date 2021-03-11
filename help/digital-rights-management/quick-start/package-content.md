---
title: Contenuto crittografato del pacchetto
description: Contenuto crittografato del pacchetto
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---


# Contenuto crittografato del pacchetto{#package-encrypted-content}

1. Copia la directory `<Primetime DRM DVD>\Reference Implementation\Command Line Tools\` nel file system locale.
1. Nella cartella `Command Line Tools\` locale, aggiorna il file `flashaccesstools.properties` in modo che funzioni con il server.

   È necessario modificare almeno le seguenti proprietà:

   * `encrypt.keys.asymmetric.certfile=[license-server-certificate.cer]`: Percorso del certificato del server licenze (in genere termina con  [!DNL .cer],  [!DNL .der] o  [!DNL .pem]).

   * `encrypt.license.serverurl=[license-server-url]`: URL del server licenze, ad esempio:     `https://<License Server Hostname>:8080/flashaccessserver/sampletenant`.

   * `encrypt.license.servercert=[transport-certificate.cer]`: Il percorso del certificato di trasporto (in genere termina con  [!DNL .cer],  [!DNL .der] o  [!DNL .pem]).

   * `encrypt.sign.certfile=[packager-credentials.pfx]`: Percorso del certificato Packager (termina con  [!DNL .pfx]).

   * `encrypt.sign.certpass=[password]`: Password del certificato Packager.
   >[!NOTE]
   >
   >Assicurati di non usare la password come schermata.

1. Crea un criterio.

   Nella cartella `Command Line Tools\` locale, esegui il seguente comando:

   ```
   java -jar libs/AdobePolicyManager.jar new examplepolicy.pol -n examplepolicy -x
   ```

   Questo comando crea un file di criteri denominato [!DNL examplepolicy.pol] che utilizza l&#39;autenticazione anonima del server licenze (opzione `-x`).
1. Copiare il file video MP4, FLV o F4V che si desidera crittografare nella cartella locale `Command Line Tools\`.
1. Crea un pacchetto per il contenuto.

   Supponiamo che il file video sorgente sia [!DNL sample.mp4]. Nella cartella `Command Line Tools\` locale, esegui il seguente comando:

   ```
   java -jar libs/AdobePackager.jar sample.mp4 sample_encrypted.mp4 -p examplepolicy.pol
   ```

   >[!NOTE]
   >
   >Se desideri creare un pacchetto per i contenuti HLS, HDS o DASH, devi utilizzare uno strumento di pacchetto diverso, ad esempio [Adobe Primetime Offline Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf).

1. Copia gli artefatti del file crittografato (in questo caso [!DNL sample_encrypted.mp4] e [!DNL sample_encrypted.mp4.metadata]) in `<Your Content Server - Tomcat Install Dir>\webapps\ROOT`.

A questo punto avete completato la fase di imballaggio del processo.

>[!NOTE]
>
>Per informazioni più dettagliate sugli strumenti della riga di comando per creare pacchetti di contenuti, creare criteri e altro ancora, consulta [Strumenti della riga di comando Adobe Primetime DRM](../drm-reference-implementations/command-line-tools/command-line-tools-overview.md).
