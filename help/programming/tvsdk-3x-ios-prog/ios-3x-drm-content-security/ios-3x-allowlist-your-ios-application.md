---
description: Puoi elenco consentiti delle tue app iOS utilizzando lo strumento strumenti di Adobe.
title: Elenco consentiti dell'applicazione iOS
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---


# Elenco consentiti dell&#39;applicazione iOS {#allowlist-your-ios-application}

Puoi elenco consentiti delle tue app iOS utilizzando lo strumento strumenti di Adobe.

Generalmente, quando completi un&#39;applicazione TVSDK, puoi utilizzare gli strumenti della riga di comando Adobe Primetime DRM per elenco consentiti della tua app.

>[!TIP]
>
>Puoi inoltre utilizzare questi strumenti per creare policy DRM e crittografare il contenuto.

L’inserimento nell’elenco delle app garantisce che il contenuto protetto possa essere riprodotto solo nel lettore video. Tuttavia, l’inserimento nell’elenco Consentiti di un’applicazione iOS richiede di completare una procedura speciale che funziona con i criteri di invio dell’applicazione Apple.

Prima di inviare un&#39;app iOS, devi firmarla e pubblicarla su Apple.

>[!NOTE]
>
>Apple elimina la firma dello sviluppatore e firma nuovamente l’applicazione con il proprio certificato.

A causa della nuova firma, le informazioni sull’elenco Consentiti generate prima dell’invio all’Apple App Store non sono utilizzabili.

Per utilizzare questo criterio di invio, Adobe ha creato uno strumento `machotools` che imprime l’impronta digitale all’applicazione iOS per creare un valore digest, firmare tale valore e inserirlo nell’applicazione iOS. Dopo l&#39;impronta digitale dell&#39;app iOS, puoi inviare l&#39;app all&#39;Apple App Store. Quando un utente esegue l&#39;app dall&#39;App Store, Primetime DRM esegue un calcolo runtime dell&#39;impronta digitale dell&#39;applicazione e la conferma con il valore digest precedentemente inserito nell&#39;applicazione. Se l’impronta digitale corrisponde, l’app viene confermata come consentita nell’elenco Consentiti e il contenuto protetto può essere riprodotto.

Lo strumento Adobe `machotools` è incluso nell’SDK per iOS TVSDK, nel [!DNL [...Cartella ]/tools/DRM].

Per utilizzare `machotools`:

1. Genera una coppia di chiavi.

   Per utilizzare un&#39;utilità come OpenSSL, aprire una finestra di comando e immettere quanto segue:

   ```shell
   openssl genrsa -des3 -out selfsigncert-ios.key 1024
   ```

1. Quando richiesto, immetti una password per proteggere la chiave privata.

   Le password devono contenere almeno 12 caratteri e i caratteri devono includere una combinazione di caratteri ASCII maiuscoli e minuscoli.
1. Per utilizzare OpenSSL per generare una password complessa, aprire una finestra di comando e immettere quanto segue:

   ```shell
   openssl rand -base64 8
   ```

1. Generare una richiesta di firma del certificato (CSR, Certificate Signing Request).

   Per utilizzare OpenSSL per generare una CSR, apri una finestra di comando e immetti quanto segue:

   ```shell
   openssl req -new -key selfsigncert-ios.key -out selfsigncert-ios.csr -batch
   ```

1. Firma il certificato e immetti qualsiasi durata.

   L’esempio seguente fornisce una scadenza di 20 anni:

   ```shell
   openssl x509 -req -days 7300 -in selfsigncert-ios.csr  
     -signkey selfsigncert-ios.key -out selfsigncert-ios.crt
   ```

1. Converti il certificato autofirmato in un file PKCS#12:

   ```shell
   openssl pkcs12 -export -out selfsigncert-ios.pfx  
     -inkey selfsigncert-ios.key -in selfsigncert-ios.crt
   ```

   Puoi usare il certificato autofirmato per firmare l’app iOS.

1. Aggiorna la posizione del file PFX e la password.
1. Prima di creare l&#39;applicazione in Xcode, vai a **[!UICONTROL Build Phases]** > **[!UICONTROL Run Script]** e aggiungi il seguente comando al tuo script di esecuzione:

   ```shell
   mkdir -p "${PROJECT_DIR}/generatedRes" "${PROJECT_DIR}/machotools" sign  
     -in "${CODESIGNING_FOLDER_PATH}/${EXECUTABLE_NAME}"  
     -out "${PROJECT_DIR}/generatedRes/AAXSAppDigest.digest"  
     -pfx "${PROJECT_DIR}/selfsigncert-ios.pfx"  
     -pass PASSWORD
   ```

1. Esegui [!DNL machotools] per generare il valore hash dell&#39;ID editore dell&#39;app.

   ```shell
   ./machotools dumpMachoSignature -in ${PROJECT_DIR}/generatedRes/AAXSAppDigest.digest
   ```

1. Crea un nuovo criterio DRM o aggiorna il criterio esistente per includere il valore hash restituito dall&#39;ID editore.
1. Utilizzando [!DNL AdobePolicyManager.jar], crea un nuovo criterio DRM (aggiorna il criterio esistente) per includere il valore hash dell&#39;ID editore restituito, un ID app facoltativo e gli attributi di versione minima e massima nel file [!DNL flashaccess-tools.properties] incluso.

   ```shell
   java -jar libs/AdobePolicyManager.jar new app_allowlist.pol
   ```

1. Crea un pacchetto per il contenuto utilizzando il nuovo criterio DRM e conferma la riproduzione del contenuto inserito nell’elenco Consentiti nell’app iOS.
