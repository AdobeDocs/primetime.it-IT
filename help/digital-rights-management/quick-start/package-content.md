---
seo-title: Contenuto crittografato pacchetto
title: Contenuto crittografato pacchetto
uuid: 1e271167-107d-41df-8a7c-3075cb3acc0c
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Contenuto crittografato pacchetto{#package-encrypted-content}

1. Copiare la `<Primetime DRM DVD>\Reference Implementation\Command Line Tools\` directory nel file system locale.
1. Nella `Command Line Tools\` cartella locale, aggiornate il `flashaccesstools.properties` file in modo che funzioni con il server.

   È necessario modificare almeno le seguenti proprietà:

   * `encrypt.keys.asymmetric.certfile=[license-server-certificate.cer]`: Percorso del certificato del server licenze (in genere termina con [!DNL .cer], [!DNL .der] o [!DNL .pem]).

   * `encrypt.license.serverurl=[license-server-url]`: L’URL del server licenze, ad esempio:    `https://<License Server Hostname>:8080/flashaccessserver/sampletenant`.

   * `encrypt.license.servercert=[transport-certificate.cer]`: Percorso del certificato di trasporto (in genere termina con [!DNL .cer], [!DNL .der]o [!DNL .pem]).

   * `encrypt.sign.certfile=[packager-credentials.pfx]`: Il percorso del certificato Packager (termina con [!DNL .pfx]).

   * `encrypt.sign.certpass=[password]`: La password per il certificato Packager.
   >[!NOTE]
   >
   >Assicurati di non rimandare la password.

1. Creare un criterio.

   Nella `Command Line Tools\` cartella locale, eseguite il comando seguente:

   ```
   java -jar libs/AdobePolicyManager.jar new examplepolicy.pol -n examplepolicy -x
   ```

   Questo comando crea un file di criteri denominato [!DNL examplepolicy.pol] che utilizza l&#39;autenticazione anonima del server licenze (l&#39; `-x` opzione).
1. Copiate il file video MP4, FLV o F4V da cifrare nella `Command Line Tools\` cartella locale.
1. Create pacchetti per il contenuto.

   Supponiamo che il file video sorgente sia [!DNL sample.mp4]. Nella `Command Line Tools\` cartella locale, eseguite il comando seguente:

   ```
   java -jar libs/AdobePackager.jar sample.mp4 sample_encrypted.mp4 -p examplepolicy.pol
   ```

   >[!NOTE]
   >
   >Se desiderate creare pacchetti di contenuti HLS, HDS o DASH, dovete utilizzare un altro strumento Packager, ad esempio [Adobe Primetime Offline Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf).

1. Copiare gli artefatti del file crittografato (in questo caso [!DNL sample_encrypted.mp4] e [!DNL sample_encrypted.mp4.metadata]) in `<Your Content Server - Tomcat Install Dir>\webapps\ROOT`.

A questo punto avete completato la fase di imballaggio del processo.

>[!NOTE]
>
>Per informazioni dettagliate sugli strumenti della riga di comando per la creazione di pacchetti di contenuti, la creazione di criteri e altro ancora, consultate Strumenti [della riga di comando DRM di](../drm-reference-implementations/command-line-tools/command-line-tools-overview.md)Adobe Primetime.
