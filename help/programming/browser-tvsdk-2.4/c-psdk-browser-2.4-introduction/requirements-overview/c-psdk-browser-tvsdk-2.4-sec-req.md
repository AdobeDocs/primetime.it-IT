---
description: È necessario tenere presenti alcune considerazioni sulla sicurezza per il browser TVSDK.
title: Considerazioni sulla sicurezza
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---


# Considerazioni sulla sicurezza{#security-considerations}

È necessario tenere presenti alcune considerazioni sulla sicurezza per il browser TVSDK.

* **Flash Player Adobe**

   * Il Flash Player non consente l&#39;accesso ai dati che si trovano al di fuori del dominio da cui è stato creato il file SWF.

      Per consentire l’accesso, ospita un file di criteri tra domini con le autorizzazioni appropriate nella directory principale del server che ospita i dati. Nella modalità di fallback del Flash nel browser TVSDK (versione del Flash Player 23 e successive), è necessario il token di autorizzazione per il dominio. Per generare il token, contatta il tuo rappresentante di Adobe.

* **JavaScript**

   * JavaScript segue lo stesso criterio di origine e impedisce l’accesso alle risorse oltre i limiti del dominio.

      Per consentire l’accesso a queste risorse, l’intestazione Access-Control-Allow-Origin (CORS) deve essere impostata sulle risorse ospitate su origini diverse dal lettore. Facoltativamente, se il contenuto viene specificato utilizzando intervalli di byte, la richiesta di opzioni di pre-flight CORS deve indicare che queste richieste sono consentite dall&#39;origine.

* **Browser e contenuti misti**

   * I browser richiedono che il contenuto crittografato AES-128 sia ospitato su un’origine protetta (ad esempio, HTTPS).

      Poiché la maggior parte dei browser non consente contenuti misti, si consiglia di ospitare il lettore, il contenuto e le risorse associate, come i file Key/WebVTT, anche su Origin protetta.

      >[!IMPORTANT]
      >
      >A partire dalla versione 2.4.5, se il lettore è ospitato su HTTPS, il browser TVSDK converte le chiamate HTTP in HTTPS quando si utilizza la tecnologia MSE.

