---
description: Per il browser TVSDK è necessario tenere presenti alcune considerazioni di sicurezza.
title: Considerazioni sulla sicurezza
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# Considerazioni sulla sicurezza{#security-considerations}

Per il browser TVSDK è necessario tenere presenti alcune considerazioni di sicurezza.

* **Flash Player Adobe**

   * Il Flash Player non consente l&#39;accesso ai dati che risiedono al di fuori del dominio da cui ha avuto origine il SWF.

     Per consentire l&#39;accesso, ospitare un file di criteri per più domini con le autorizzazioni appropriate nella directory principale del server che ospita i dati. Nella modalità di fallback del Flash nel browser TVSDK (versione 23 e successive del Flash Player), è necessario il token di autorizzazione per il dominio. Per generare il token, contatta il rappresentante del tuo Adobe.

* **JavaScript**

   * JavaScript segue lo stesso criterio di origine e impedisce l’accesso alle risorse oltre i limiti del dominio.

     Per consentire l’accesso a queste risorse, l’intestazione CORS (Access-Control-Allow-Origin) deve essere impostata sulle risorse in hosting su origini diverse dal lettore. Facoltativamente, se il contenuto viene specificato utilizzando intervalli di byte, la richiesta delle opzioni di pre-volo CORS deve indicare che queste richieste sono consentite dall’origine.

* **Browser e contenuti misti**

   * I browser richiedono che il contenuto crittografato AES-128 sia ospitato su un’origine sicura (ad esempio, HTTPS).

     Poiché la maggior parte dei browser non consente l’utilizzo di contenuti misti, consigliamo che il lettore, il contenuto e le risorse associate, come i file Key/WebVTT, siano ospitati su un’origine sicura.

     >[!IMPORTANT]
     >
     >A partire dalla versione 2.4.5, se il lettore è ospitato su HTTPS, il TVSDK del browser converte le chiamate HTTP in HTTPS quando si utilizza la tecnologia MSE.
