---
description: Potete inserire in una whitelist le app iOS utilizzando lo strumento di strumenti di analisi di Adobe.
seo-description: Potete inserire in una whitelist le app iOS utilizzando lo strumento di strumenti di analisi di Adobe.
seo-title: Whitelist dell’applicazione iOS
title: Whitelist dell’applicazione iOS
uuid: 52ce1dd7-5f10-418e-9916-cec60eae874e
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Whitelist dell’applicazione iOS{#whitelist-your-ios-application}

Potete inserire in una whitelist le app iOS utilizzando lo strumento di strumenti di analisi di Adobe.

Generalmente, quando completi un’applicazione TVSDK, puoi utilizzare gli strumenti della riga di comando DRM di Adobe Primetime per inserire in una whitelist l’app.

>[!TIP]
>
>Potete inoltre utilizzare questi strumenti per creare criteri DRM e cifrare il contenuto.

La whitelist dell&#39;app garantisce che il contenuto protetto possa essere riprodotto solo nel lettore video. Tuttavia, per inserire in una whitelist un&#39;applicazione iOS è necessario completare una procedura speciale che funzioni con i criteri di invio dell&#39;applicazione Apple.

Prima di inviare un&#39;app iOS, dovete firmarla e pubblicarla su Apple.

>[!NOTE]
>
>Apple striscia la firma dello sviluppatore e la firma nuovamente con il proprio certificato.

A causa della nuova firma, le informazioni di whitelist generate prima dell&#39;invio all&#39;Apple App Store non sono utilizzabili.

Per utilizzare questo criterio di invio, Adobe ha creato uno `machotools` strumento che imprime un&#39;impronta digitale all&#39;applicazione iOS per creare un valore digest, firmare questo valore e iniettare questo valore nell&#39;applicazione iOS. Dopo aver eseguito l&#39;impronta digitale dell&#39;app iOS, potete inviare l&#39;app ad Apple App Store. Quando un utente esegue l&#39;app dall&#39;App Store, Primetime DRM esegue un calcolo runtime dell&#39;impronta digitale dell&#39;applicazione e lo conferma con il valore digest precedentemente immesso nell&#39;applicazione. Se l&#39;impronta digitale corrisponde, l&#39;app viene confermata come inserita nella white list e il contenuto protetto può essere riprodotto.

Lo strumento Adobe `machotools` è incluso nell’SDK iOS TVSDK, in [!DNL [...]/tools/DRM].

Per utilizzare `machotools`:

1. Genera una coppia di chiavi.

   Per utilizzare un&#39;utilità come OpenSSL, aprite una finestra di comando e immettete quanto segue:

   ```
   openssl genrsa -des3 -out selfsigncert-ios.key 1024
   ```

1. Quando richiesto, immettete una password per proteggere la chiave privata.

   Le password devono contenere almeno 12 caratteri e i caratteri devono includere sia caratteri ASCII maiuscoli che minuscoli.
1. Per utilizzare OpenSSL per generare una password complessa, aprite una finestra di comando e immettete quanto segue:

   ```
   openssl rand -base64 8
   ```

1. Generare una richiesta di firma dei certificati (CSR).

   Per utilizzare OpenSSL per generare un CSR, aprite una finestra di comando e immettete quanto segue:

   ```
   openssl req -new -key selfsigncert-ios.key -out selfsigncert-ios.csr -batch
   ```

1. Firmare il certificato e immettere qualsiasi durata.

   L’esempio seguente riporta una scadenza di 20 anni:

   ```
   openssl x509 -req -days 7300 -in selfsigncert-ios.csr  
     -signkey selfsigncert-ios.key -out selfsigncert-ios.crt
   ```

1. Convertite il certificato autofirmato in un file PKCS#12:

   ```
   openssl pkcs12 -export -out selfsigncert-ios.pfx  
     -inkey selfsigncert-ios.key -in selfsigncert-ios.crt
   ```

   Potete utilizzare il certificato autofirmato per firmare l&#39;app iOS.

1. Aggiornare la posizione del file PFX e la password.
1. Prima di creare l&#39;applicazione in Xcode, passare a **[!UICONTROL Build Phases]** > **[!UICONTROL Run Script]** e aggiungere il seguente comando allo script di esecuzione:

   ```
   mkdir -p "${PROJECT_DIR}/generatedRes" "${PROJECT_DIR}/machotools" sign  
     -in "${CODESIGNING_FOLDER_PATH}/${EXECUTABLE_NAME}"  
     -out "${PROJECT_DIR}/generatedRes/AAXSAppDigest.digest"  
     -pfx "${PROJECT_DIR}/selfsigncert-ios.pfx"  
     -pass PASSWORD
   ```

1. Esegui [!DNL machotools] per generare il valore hash dell&#39;ID editore dell&#39;app.

   ```
   ./machotools dumpMachoSignature -in ${PROJECT_DIR}/generatedRes/AAXSAppDigest.digest
   ```

1. Create un nuovo criterio DRM o aggiornate il criterio esistente per includere il valore hash ID editore restituito.
1. Utilizzando [!DNL AdobePolicyManager.jar], create un nuovo criterio DRM (aggiornate il criterio esistente) per includere nel [!DNL flashaccess-tools.properties] file incluso il valore hash ID editore restituito, un ID app facoltativo e gli attributi di versione min e max.

   ```
   java -jar libs/AdobePolicyManager.jar new app_whitelist.pol
   ```

1. Create un pacchetto del contenuto utilizzando la nuova policy DRM e confermate la riproduzione del contenuto inserito nella white list nell&#39;app iOS.

