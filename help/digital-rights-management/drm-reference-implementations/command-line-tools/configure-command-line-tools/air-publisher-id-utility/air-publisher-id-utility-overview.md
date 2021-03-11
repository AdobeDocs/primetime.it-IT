---
title: Panoramica
description: Panoramica
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---


# Utility ID di AIR Publisher {#air-publisher-id-utility}

Quando si crea un file AIR, AIR Developer Tool (ADT) genera automaticamente un ID editore. L&#39;utility AIR Publisher ID ( [!DNL AdobePublisherIDUtility.jar]) calcola l&#39;ID editore per un&#39;applicazione AIR.

L’ID editore è univoco per il certificato utilizzato per creare un file AIR. Se riutilizzi lo stesso certificato per più applicazioni AIR, tutte le applicazioni AIR avranno lo stesso ID editore. Una versione di AIR successiva alla versione 1.5.2 non aggiunge l’ID editore generato a un file . Pertanto, se prevedi di utilizzare un elenco consentiti di applicazione AIR, utilizza questo strumento per determinare l&#39;ID editore.

>[!NOTE]
>
>L&#39;ID dell&#39;editore utilizzato per l&#39;applicazione dell&#39;elenco consentiti AIR non è lo stesso ID dell&#39;editore specificato dall&#39;autore dell&#39;applicazione nel file [!DNL application.xml] dell&#39;applicazione.

## Uso della riga di comando dell&#39;utilità ID editore di AIR {#air-publisher-id-utility-command-line-usage}

```
java -jar AdobePublisherIDUtility.jar 
<i class="+ topic ph hi-d="" i "="">
 <i class="+ topic ph hi-d="" i "="">
  signaturefile 
  java -jar AdobePublisherIDUtility.jar -s 
  <i class="+ topic ph hi-d="" i "="">
    signingcert
  </i class="+ topic>
 </i class="+ topic>
</i class="+ topic>
```

* 
   * `signaturefile`* specifica un percorso del  [!DNL signatures.xml] file dell&#39;applicazione AIR, situato nella  [!DNL META-INF] directory delle applicazioni

* `signingcert` specifica il certificato utilizzato per firmare un&#39;applicazione AIR

>[!NOTE]
>
>Per determinare l&#39;ID editore per un&#39;applicazione Android, devi utilizzare l&#39;opzione `-s` per specificare il certificato utilizzato per firmare il pacchetto dell&#39;applicazione Android (APK). Primetime DRM è necessario per creare applicazioni Android che possono riprodurre contenuti protetti da DRM di Primetime.