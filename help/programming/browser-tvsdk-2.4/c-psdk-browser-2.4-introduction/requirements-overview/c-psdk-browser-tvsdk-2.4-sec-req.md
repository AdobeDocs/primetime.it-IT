---
description: Esistono alcune considerazioni di sicurezza da tenere presenti per l'SDK per browser.
seo-description: Esistono alcune considerazioni di sicurezza da tenere presenti per l'SDK per browser.
seo-title: Considerazioni sulla sicurezza
title: Considerazioni sulla sicurezza
uuid: 78edf2b0-363c-4ab6-b588-ab4748ee6096
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---


# Considerazioni sulla sicurezza{#security-considerations}

Esistono alcune considerazioni di sicurezza da tenere presenti per l&#39;SDK per browser.

* **Flash Player Adobe**

   * Il Flash Player non consente l&#39;accesso ai dati che risiedono al di fuori del dominio da cui è stato originato il file SWF.

      Per consentire l&#39;accesso, ospitare un file di criteri per i domini con le autorizzazioni appropriate nella directory principale del server in cui sono ospitati i dati. In modalità Fallback di Flash in Browser TVSDK (versione di Flash Player 23 e successiva), è necessario il token di autorizzazione per il dominio. Per generare il token, contattate il rappresentante del Adobe .

* **JavaScript**

   * JavaScript segue lo stesso criterio di origine e impedisce l&#39;accesso alle risorse attraverso i limiti del dominio.

      Per consentire l’accesso a queste risorse, l’intestazione Access-Control-Allow-Origin (CORS) deve essere impostata sulle risorse ospitate su origini diverse dal lettore. Facoltativamente, se il contenuto viene specificato utilizzando intervalli di byte, la richiesta di opzioni di verifica preliminare CORS deve indicare che queste richieste sono consentite dall&#39;origine.

* **Browser e contenuti misti**

   * I browser richiedono che il contenuto crittografato AES-128 sia ospitato su un&#39;origine protetta (ad esempio, HTTPS).

      Poiché la maggior parte dei browser non consente contenuti misti, è consigliabile che il lettore, il contenuto e le risorse associate, come i file Key/ WebVTT, siano ospitati anche su Origine protetta.

      >[!IMPORTANT]
      >
      >A partire dalla versione 2.4.5, se il lettore è ospitato su HTTPS, Browser TVSDK converte le chiamate HTTP in HTTPS quando si utilizza la tecnologia MSE.

