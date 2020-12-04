---
description: Potete  le vostre app iOS utilizzando  strumento di Adobe  strumenti.
seo-description: Potete  le vostre app iOS utilizzando  strumento di Adobe  strumenti.
seo-title: ' Elenco consentiti dell''applicazione iOS'
title: ' Elenco consentiti dell''applicazione iOS'
uuid: bc558f5f-d4e6-4c1c-81eb-f8bd61c63016
translation-type: tm+mt
source-git-commit: eb9f0a2f6d2118b953c711dfdc0402d1d923b016
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 0%

---


#  Elenco consentiti dell&#39;applicazione iOS {#allowlist-your-ios-application}

Potete  le vostre app iOS utilizzando  strumento di Adobe  strumenti.

Generalmente, quando completi un’applicazione TVSDK, puoi utilizzare  strumenti della riga di comando Adobe Primetime DRM per  elenco consentiti dell’app.

>[!TIP]
>
>Potete inoltre utilizzare questi strumenti per creare criteri DRM e cifrare il contenuto.

L&#39;elenco delle app garantisce che il contenuto protetto possa essere riprodotto solo nel lettore video. Tuttavia, per consentire l&#39;elenco di un&#39;applicazione iOS è necessario completare una procedura speciale che funzioni con i criteri di invio dell&#39;applicazione Apple.

Prima di inviare un&#39;app iOS, dovete firmarla e pubblicarla su Apple.

>[!NOTE]
>
>Apple striscia la firma dello sviluppatore e la firma nuovamente con il proprio certificato.

A causa della nuova firma, le informazioni di elenco consentite generate prima dell&#39;invio all&#39;Apple App Store non sono utilizzabili.

Per utilizzare questo criterio di invio,  Adobe ha creato uno strumento `machotools` che imprime un&#39;impronta digitale all&#39;applicazione iOS per creare un valore digest, firmare questo valore e inserire questo valore nell&#39;applicazione iOS. Dopo aver eseguito l&#39;impronta digitale dell&#39;app iOS, potete inviare l&#39;app ad Apple App Store. Quando un utente esegue l&#39;app dall&#39;App Store, Primetime DRM esegue un calcolo runtime dell&#39;impronta digitale dell&#39;applicazione e lo conferma con il valore digest precedentemente immesso nell&#39;applicazione. Se l&#39;impronta digitale corrisponde, l&#39;app viene confermata come consentita nell&#39;elenco e il contenuto protetto può essere riprodotto.

Lo strumento  Adobe `machotools` è incluso nell&#39;SDK iOS TVSDK, in [!DNL [...]/tools/DRM].

Per utilizzare `machotools`:

1. Genera una coppia di chiavi.

   Per utilizzare un&#39;utilità come OpenSSL, aprite una finestra di comando e immettete quanto segue:

   ```shell
   openssl genrsa -des3 -out selfsigncert-ios.key 1024
   ```

1. Quando richiesto, immettete una password per proteggere la chiave privata.

   Le password devono contenere almeno 12 caratteri e i caratteri devono includere sia caratteri ASCII maiuscoli che minuscoli.
1. Per utilizzare OpenSSL per generare una password complessa, aprite una finestra di comando e immettete quanto segue:

   ```shell
   openssl rand -base64 8
   ```

1. Generare una richiesta di firma dei certificati (CSR).

   Per utilizzare OpenSSL per generare un CSR, aprite una finestra di comando e immettete quanto segue:

   ```shell
   openssl req -new -key selfsigncert-ios.key -out selfsigncert-ios.csr -batch
   ```

1. Firmare il certificato e immettere qualsiasi durata.

   L’esempio seguente riporta una scadenza di 20 anni:

   ```shell
   openssl x509 -req -days 7300 -in selfsigncert-ios.csr  
     -signkey selfsigncert-ios.key -out selfsigncert-ios.crt
   ```

1. Convertite il certificato autofirmato in un file PKCS#12:

   ```shell
   openssl pkcs12 -export -out selfsigncert-ios.pfx  
     -inkey selfsigncert-ios.key -in selfsigncert-ios.crt
   ```

   Potete utilizzare il certificato autofirmato per firmare l&#39;app iOS.

1. Aggiornare la posizione del file PFX e la password.
1. Prima di creare l&#39;applicazione in Xcode, andare su **[!UICONTROL Build Phases]** > **[!UICONTROL Run Script]** e aggiungere il comando seguente allo script di esecuzione:

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

1. Create un nuovo criterio DRM o aggiornate il criterio esistente per includere il valore hash ID editore restituito.
1. Utilizzando [!DNL AdobePolicyManager.jar], create un nuovo criterio DRM (aggiornate il criterio esistente) per includere il valore hash ID editore restituito, un ID app facoltativo e gli attributi versione min e max nel file [!DNL flashaccess-tools.properties] incluso.

   ```shell
   java -jar libs/AdobePolicyManager.jar new app_allowlist.pol
   ```

1. Create un pacchetto del contenuto utilizzando la nuova policy DRM e confermate la riproduzione del contenuto incluso nell&#39;elenco nella vostra app iOS.
