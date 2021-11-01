---
title: Informazioni sui file CRL
description: Informazioni sui file CRL
copied-description: true
exl-id: 126a323d-9433-4a1e-a617-2d3bbf717cce
source-git-commit: 6a00df9c061da43f6efa49d927873db629568597
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# Informazioni sui file CRL {#about-crl-files}

Per funzionare correttamente, i server Individualization e License devono disporre di diversi file dell’elenco di revoca dei certificati (CRL) memorizzati nella cache su disco sul server dell’applicazione in esecuzione (ad esempio, Tomcat). I nuovi file CRL devono essere scaricati e memorizzati nella cache su disco su base regolare. Se il periodo di validità dei file CRL sul disco è lasciato scadere, Individualization Server rifiuterà di individuare i client e il License Server rifiuterà di rilasciare licenze.

I CRL memorizzati nella cache su disco devono avere nomi di file che corrispondono agli URL corrispondenti. I caratteri speciali quali i due punti &#39;:&#39; e le barre &#39;/&#39; sono convertiti in caratteri di sottolineatura &#39;_&#39; nei nomi dei file.

Di seguito è riportato un elenco di CRL ospitati esternamente utilizzati sia dai server di Individualization che da quelli di Licenza:

* **CRL intermedio:**

   * URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl>]
   * File: [!DNL http___crl2.adobe.com_Adobe_FlashAccessIntermediateCA.crl]
   * Validità: Buono per circa 12 mesi dalla creazione

* **CRL principale:**

   * URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessRootCA.crl>]
   * File: [!DNL http___crl2.adobe.com_Adobe_FlashAccessRootCA.crl]
   * Validità: Buono per circa 5 anni dalla creazione

* **Ultimo CRL:**

   * URL: [!DNL <ht<span></span>tps://crl3.adobe.com/AdobeSystemsIncorporatedFlashAccessRuntime/LatestCRL.crl>]
   * File: [!DNL http___crl3.adobe.com_AdobeSystemsIncorporatedFlashAccessRuntime_LatestCRL.crl]
   * Validità: Buono per circa 3 mesi dalla creazione

Per informazioni sui CRL ospitati esternamente che possono essere utilizzati dai server di licenza, contattare il supporto Adobe.

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

Oltre ai CRL ospitati esternamente, puoi creare e gestire un CRL aggiuntivo. Si tratta del CRL di Individualization CA, come specificato nel [Creare un CRL di CA per l&#39;individuazione](../../../on-premises-i15n-server/server-configuration-section/server-properties/create-i15n-ca-crl.md) sezione di questo documento.

È previsto l’aggiornamento dei CRL 45 giorni prima della scadenza. In questo modo è possibile disporre di tempo sufficiente per acquisire e installare i nuovi CRL generati da Internet. È necessario assicurarsi di aggiornare i file CRL prima che siano scaduti.
