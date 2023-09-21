---
title: Informazioni sui file CRL
description: Informazioni sui file CRL
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# Informazioni sui file CRL {#about-crl-files}

Per funzionare correttamente, i server di Personalizzazione e Licenza devono disporre di diversi file CRL (Certificate Revocation List) memorizzati su disco nel server applicazioni in esecuzione (ad esempio, Tomcat). I nuovi file CRL devono essere scaricati e memorizzati nella cache su disco regolarmente secondo la pianificazione. Se il periodo di validità dei file CRL su disco scade, il server di personalizzazione si rifiuterà di individuare i client e il server licenze si rifiuterà di rilasciare le licenze.

I CRL memorizzati nella cache del disco devono avere nomi di file corrispondenti agli URL corrispondenti. Nei nomi dei file, i caratteri speciali come i due punti &quot;:&quot; e le barre &quot;/&quot; vengono convertiti in caratteri di sottolineatura &quot;_&quot;.

Di seguito è riportato un elenco di CRL in hosting esterno utilizzati sia dai server di personalizzazione che dai server licenze:

* **CRL intermedio:**

   * URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl>]
   * File: [!DNL http___crl2.adobe.com_Adobe_FlashAccessIntermediateCA.crl]
   * Validità: valida per circa 12 mesi dalla creazione

* **CRL radice:**

   * URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessRootCA.crl>]
   * File: [!DNL http___crl2.adobe.com_Adobe_FlashAccessRootCA.crl]
   * Validità: valida per circa 5 anni dalla creazione

* **CRL più recente:**

   * URL: [!DNL <ht<span></span>tps://crl3.adobe.com/AdobeSystemsIncorporatedFlashAccessRuntime/LatestCRL.crl>]
   * File: [!DNL http___crl3.adobe.com_AdobeSystemsIncorporatedFlashAccessRuntime_LatestCRL.crl]
   * Validità: valida per circa 3 mesi dalla creazione

Per informazioni sui CRL ospitati esternamente che possono essere utilizzati dai server licenze, contatta il supporto Adobe.

<!---

Commenting out because of a security vulnerability reported in Jira PSIRT-20689. 

The following are externally hosted CRLs that are used only by the License Servers:

* URL: `https://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl`

* File: `http___crl2.adobe.com_Adobe_FlashAccessIndividualizationCA.crl`

* Validity: Good for approximately 3 months from creation

* URL: `https://individualization-crl.primetime.adobe.com/FlashAccessIndividualizationCA.crl`

* File: `http___individualization-crl.primetime.adobe.com_FlashAccessIndividualizationCA.crl`

* Validity: Good for approximately 3 months from creation

* URL: `https://individualization-crl.s3-website-us-east-1.amazonaws.com/FlashAccessIndividualizationCA.crl`

* File: `http___individualization-crl.s3-website-us-east-1.amazonaws.com_FlashAccessIndividualizationCA.crl`

* Validity: Good for approximately 3 months from creation

--->

Oltre ai CRL ospitati esternamente, puoi creare e gestire un CRL aggiuntivo. Questo è il CRL della CA di Personalizzazione, come specificato nella [Crea CRL CA di personalizzazione](../../../on-premises-i15n-server/server-configuration-section/server-properties/create-i15n-ca-crl.md) sezione del presente documento.

L’aggiornamento dei CRL è pianificato 45 giorni prima della scadenza. In questo modo avrai a disposizione il tempo necessario per acquisire e installare i CRL appena generati da Internet. Prima della scadenza, è necessario aggiornare i file CRL.
