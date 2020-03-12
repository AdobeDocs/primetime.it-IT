---
seo-title: Informazioni sui file CRL
title: Informazioni sui file CRL
uuid: 672c3ca0-5c5d-4ec7-83b1-f0f8e34c8d09
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Informazioni sui file CRL {#about-crl-files}

Per funzionare correttamente, i server delle licenze e delle individualizzazioni devono avere diversi file elenco di revoca certificati (CRL) memorizzati nella cache su disco sul server delle applicazioni in esecuzione (ad esempio, Tomcat). I nuovi file CRL devono essere scaricati e memorizzati nella cache su disco su base regolare. Se il periodo di validità dei file CRL sul disco è scaduto, il server di individuazione si rifiuterà di individuare i client e il server licenze si rifiuterà di rilasciare licenze.

I CRL memorizzati nella cache su disco devono avere nomi di file corrispondenti agli URL corrispondenti. I caratteri speciali come i due punti &#39;:&#39; e &#39;/&#39; sono convertiti in caratteri di sottolineatura &#39;_&#39; nei nomi dei file.

Di seguito è riportato un elenco di CRL con hosting esternamente utilizzati sia dai server di licenze che da quelli di Individualizzazione:

* **CRL intermedio:**

   * URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl>]
   * File: [!DNL http___crl2.adobe.com_Adobe_FlashAccessIntermediateCA.crl]
   * Validità: Buona per circa 12 mesi dalla creazione

* **CRL principale:**

   * URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessRootCA.crl>]
   * File: [!DNL http___crl2.adobe.com_Adobe_FlashAccessRootCA.crl]
   * Validità: Buona per circa 5 anni dalla creazione

* **Ultimo CRL:**

   * URL: [!DNL <ht<span></span>tps://crl3.adobe.com/AdobeSystemsIncorporatedFlashAccessRuntime/LatestCRL.crl>]
   * File: [!DNL http___crl3.adobe.com_AdobeSystemsIncorporatedFlashAccessRuntime_LatestCRL.crl]
   * Validità: Buona per circa 3 mesi dalla creazione

Di seguito sono riportati i CRL con hosting esterno utilizzati solo dai server licenze:

* URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl>]
* File: [!DNL http___crl2.adobe.com_Adobe_FlashAccessIndividualizationCA.crl]
* Validità: Buona per circa 3 mesi dalla creazione

* URL: [!DNL <ht<span></span>tps://individualization-crl.primetime.adobe.com/FlashAccessIndividualizationCA.crl>]
* File: [!DNL http___individualization-crl.primetime.adobe.com_FlashAccessIndividualizationCA.crl]
* Validità: Buona per circa 3 mesi dalla creazione

* URL: [!DNL <ht<span></span>tps://individualization-crl.s3-website-us-east-1.amazonaws.com/FlashAccessIndividualizationCA.crl]>
* File: [!DNL http___individualization-crl.s3-website-us-east-1.amazonaws.com_FlashAccessIndividualizationCA.crl]
* Validità: Buona per circa 3 mesi dalla creazione

Oltre ai CRL di cui sopra, è necessario creare e mantenere un CRL aggiuntivo. Si tratta del CRL CA di Individualizzazione, come specificato nella sezione [Create Individualization CA CRL](../../../on-premises-i15n-server/server-configuration-section/server-properties/create-i15n-ca-crl.md) di questo documento.

È previsto l&#39;aggiornamento dei CRL 45 giorni prima della scadenza. Questo dovrebbe consentire di ottenere e installare CRL generati di recente da Internet. È necessario aggiornare i file CRL prima che siano scaduti.
