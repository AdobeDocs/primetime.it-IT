---
description: Puoi eseguire l’elenco consentiti delle app iOS utilizzando lo strumento Machotools di Adobe.
title: Elenco consentiti dell’applicazione iOS
exl-id: 3af75d9a-3b38-4d3c-9890-513a4abc1809
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# Elenco consentiti dell’applicazione iOS {#allowlist-your-ios-application}

Puoi eseguire l’elenco consentiti delle app iOS utilizzando lo strumento Machotools di Adobe.

In genere, quando si completa un&#39;applicazione TVSDK, è possibile utilizzare gli strumenti della riga di comando Adobe Primetime DRM per eseguire l&#39;elenco consentiti dell&#39;app.

>[!TIP]
>
>È inoltre possibile utilizzare questi strumenti per creare criteri DRM e crittografare i contenuti.

Consenti l’inserimento nell’app per garantire che i contenuti protetti possano essere riprodotti solo nel lettore video. Tuttavia, per inserire un’applicazione iOS nell’elenco Consentiti è necessario completare una procedura speciale che funziona con i criteri di invio delle applicazioni di Apple.

Prima di inviare un’app iOS, devi firmarla e pubblicarla in Apple.

>[!NOTE]
>
>Apple elimina la firma dello sviluppatore e firma nuovamente l’applicazione con il proprio certificato.

A causa della rifirma, le informazioni sull’elenco Consentiti generate prima dell’invio all’App Store di Apple non sono utilizzabili.

Per utilizzare questo criterio di invio, Adobe ha creato un `machotools` strumento che consente di rilevare le impronte digitali dell’applicazione iOS per creare un valore digest, firmare questo valore e inserirlo nell’applicazione iOS. Dopo aver inserito le impronte digitali nell’app iOS, puoi inviarla all’App Store di Apple. Quando un utente esegue l’app da App Store, Primetime DRM esegue un calcolo in fase di esecuzione dell’impronta digitale dell’applicazione e la conferma con il valore digest precedentemente inserito nell’applicazione. Se l’impronta digitale corrisponde, l’app viene confermata come inserita nell’elenco Consentiti e il contenuto protetto può essere riprodotto.

L’Adobe `machotools` è incluso nell&#39;SDK di iOS TVSDK, nel [!DNL [...]/tools/DRM].

Da utilizzare `machotools`:

1. Genera una coppia di chiavi.

   Per utilizzare una utility come OpenSSL, aprire una finestra di comando e immettere quanto segue:

   ```shell
   openssl genrsa -des3 -out selfsigncert-ios.key 1024
   ```

1. Quando richiesto, immettere una password per proteggere la chiave privata.

   Le password devono contenere almeno 12 caratteri e i caratteri devono includere una combinazione di caratteri ASCII maiuscoli e minuscoli e numeri.
1. Per utilizzare OpenSSL per generare una password sicura, aprire una finestra di comando e immettere quanto segue:

   ```shell
   openssl rand -base64 8
   ```

1. Genera una richiesta di firma del certificato (CSR, Certificate Signing Request).

   Per utilizzare OpenSSL per generare una CSR, aprire una finestra di comando e immettere quanto segue:

   ```shell
   openssl req -new -key selfsigncert-ios.key -out selfsigncert-ios.csr -batch
   ```

1. Firma autonomamente il certificato e immetti una durata.

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

   Puoi utilizzare il certificato autofirmato per firmare la tua app iOS.

1. Aggiornare il percorso del file PFX e la password.
1. Prima di creare l’applicazione in Xcode, passa a  **[!UICONTROL Build Phases]** > **[!UICONTROL Run Script]** e aggiungi il seguente comando allo script di esecuzione:

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

1. Creare un nuovo criterio DRM o aggiornare il criterio esistente per includere il valore hash dell&#39;ID editore restituito.
1. Utilizzo di [!DNL AdobePolicyManager.jar], crea un nuovo criterio DRM (aggiorna il criterio esistente) per includere il valore hash dell&#39;ID editore restituito, un ID app opzionale e gli attributi di versione min e max nel [!DNL flashaccess-tools.properties] file.

   ```shell
   java -jar libs/AdobePolicyManager.jar new app_allowlist.pol
   ```

1. Crea un pacchetto dei contenuti utilizzando la nuova policy DRM e conferma la riproduzione dei contenuti consentiti elencati nella tua app iOS.
