---
title: Panoramica
description: Panoramica
copied-description: true
exl-id: 07f2ef0b-c6aa-4574-a3ae-18685a090cf2
source-git-commit: a1fc67b708f3d5821532d3827639adbadf15f6b4
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# Utility AIR Publisher ID {#air-publisher-id-utility}

Quando si crea un file AIR, AIR Developer Tool (ADT) genera automaticamente un ID editore. Utility AIR Publisher ID ( [!DNL AdobePublisherIDUtility.jar]) calcola l&#39;ID editore per un&#39;applicazione AIR.

L&#39;ID editore è univoco per il certificato utilizzato per creare un file AIR. Se riutilizzi lo stesso certificato per più applicazioni AIR, tutte le applicazioni AIR avranno lo stesso ID editore. Una versione di AIR successiva alla versione 1.5.2 non aggiunge l’ID editore generato a un file . Pertanto, se si intende utilizzare un elenco consentiti di applicazione AIR, utilizzare questo strumento per determinare l&#39;ID editore.

>[!NOTE]
>
>L&#39;ID editore utilizzato per l&#39;applicazione di AIR elenco consentiti non è lo stesso ID editore specificato dall&#39;editore dell&#39;applicazione nel [!DNL application.xml] file.

## Utilizzo della riga di comando dell&#39;utilità di pubblicazione AIR ID {#air-publisher-id-utility-command-line-usage}

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

* `signaturefile` specifica un percorso dell&#39;applicazione AIR [!DNL signatures.xml] file, situato nelle applicazioni [!DNL META-INF] directory

* `signingcert` specifica il certificato utilizzato per firmare un&#39;applicazione AIR

>[!NOTE]
>
>Per determinare l&#39;ID editore per un&#39;applicazione Android, è necessario utilizzare il `-s` per specificare il certificato utilizzato per firmare il pacchetto dell&#39;applicazione Android (APK). Primetime DRM è necessario per creare applicazioni Android che possono riprodurre contenuti protetti da DRM di Primetime.
