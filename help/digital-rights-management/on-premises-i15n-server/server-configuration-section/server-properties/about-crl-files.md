---
title: Informazioni sui file CRL
description: Informazioni sui file CRL
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '305'
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

Di seguito sono riportati i CRL ospitati esternamente utilizzati solo dai server licenze:

* URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl>]
* File: [!DNL http___crl2.adobe.com_Adobe_FlashAccessIndividualizationCA.crl]
* Validità: Buono per circa 3 mesi dalla creazione

* URL: [!DNL <ht<span></span>tps://individualization-crl.primetime.adobe.com/FlashAccessIndividualizationCA.crl>]
* File: [!DNL http___individualization-crl.primetime.adobe.com_FlashAccessIndividualizationCA.crl]
* Validità: Buono per circa 3 mesi dalla creazione

* URL: [!DNL <ht<span></span>tps://individualization-crl.s3-website-us-east-1.amazonaws.com/FlashAccessIndividualizationCA.crl]
* File: [!DNL http___individualization-crl.s3-website-us-east-1.amazonaws.com_FlashAccessIndividualizationCA.crl]
* Validità: Buono per circa 3 mesi dalla creazione

Oltre ai suddetti CRL, è necessario creare e mantenere un CRL aggiuntivo. Si tratta dell&#39;Individualization CA CRL, come specificato nella sezione [Create Individualization CA CRL](../../../on-premises-i15n-server/server-configuration-section/server-properties/create-i15n-ca-crl.md) del presente documento.

È previsto l’aggiornamento dei CRL 45 giorni prima della scadenza. In questo modo è possibile disporre di tempo sufficiente per acquisire e installare i nuovi CRL generati da Internet. È necessario assicurarsi di aggiornare i file CRL prima che siano scaduti.
