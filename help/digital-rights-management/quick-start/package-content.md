---
title: Contenuto crittografato del pacchetto
description: Contenuto crittografato del pacchetto
copied-description: true
exl-id: e5792917-8172-48b0-8792-7a7e942596c5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# Contenuto crittografato del pacchetto{#package-encrypted-content}

1. Copia il `<Primetime DRM DVD>\Reference Implementation\Command Line Tools\` nel file system locale.
1. Nel tuo locale `Command Line Tools\` cartella, aggiorna la `flashaccesstools.properties` per lavorare con il server.

   È necessario modificare almeno le seguenti proprietà:

   * `encrypt.keys.asymmetric.certfile=[license-server-certificate.cer]`: percorso del certificato del server licenze (in genere termina con [!DNL .cer], [!DNL .der] o [!DNL .pem]).

   * `encrypt.license.serverurl=[license-server-url]`: URL del server licenze, ad esempio:    `https://<License Server Hostname>:8080/flashaccessserver/sampletenant`.

   * `encrypt.license.servercert=[transport-certificate.cer]`: percorso del certificato di trasporto (in genere termina con [!DNL .cer], [!DNL .der], o [!DNL .pem]).

   * `encrypt.sign.certfile=[packager-credentials.pfx]`: percorso del certificato Packager (termina con [!DNL .pfx]).

   * `encrypt.sign.certpass=[password]`: password per il certificato Packager.
   >[!NOTE]
   >
   >Assicurati di non usare la password.

1. Crea un criterio.

   Nel tuo locale `Command Line Tools\` cartella, esegui il comando seguente:

   ```
   java -jar libs/AdobePolicyManager.jar new examplepolicy.pol -n examplepolicy -x
   ```

   Con questo comando viene creato un file di criteri denominato [!DNL examplepolicy.pol] che utilizza l&#39;autenticazione anonima del server licenze (il `-x` opzionale).
1. Copiare il file video MP4, FLV o F4V che si desidera crittografare nel file locale `Command Line Tools\` cartella.
1. Creare un pacchetto dei contenuti.

   Supponiamo che il file video sorgente sia [!DNL sample.mp4]. Nel tuo locale `Command Line Tools\` cartella, esegui il comando seguente:

   ```
   java -jar libs/AdobePackager.jar sample.mp4 sample_encrypted.mp4 -p examplepolicy.pol
   ```

   >[!NOTE]
   >
   >Se si desidera creare un pacchetto di contenuti HLS, HDS o DASH, è necessario utilizzare uno strumento Packager diverso, ad esempio [Adobe Primetime Offline Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf).

1. Copiare gli artefatti del file crittografato (in questo caso [!DNL sample_encrypted.mp4] e [!DNL sample_encrypted.mp4.metadata]) a `<Your Content Server - Tomcat Install Dir>\webapps\ROOT`.

A questo punto hai completato la fase di packaging del processo.

>[!NOTE]
>
>Per informazioni più dettagliate sugli strumenti della riga di comando per la creazione di pacchetti di contenuto, la creazione di policy e altro ancora, consulta [Strumenti della riga di comando di Adobe Primetime DRM](../drm-reference-implementations/command-line-tools/command-line-tools-overview.md).
