---
title: Panoramica
description: Panoramica
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# Utility AIR Publisher ID {#air-publisher-id-utility}

Quando si crea un file AIR, AIR Developer Tool (ADT) genera automaticamente un ID di pubblicazione. Utility AIR Publisher ID ( [!DNL AdobePublisherIDUtility.jar]) calcola l&#39;ID dell&#39;editore per un&#39;applicazione AIR.

L’ID dell’editore è univoco rispetto al certificato utilizzato per creare un file AIR. Se riutilizzi lo stesso certificato per più applicazioni AIR, tutte le applicazioni AIR hanno lo stesso ID editore. Una versione di AIR successiva alla versione 1.5.2 non aggiunge l’ID dell’editore generato a un file. Pertanto, se prevedi di utilizzare un elenco consentiti dell’applicazione AIR, utilizza questo strumento per determinare l’ID dell’editore.

>[!NOTE]
>
>L&#39;ID del server di pubblicazione utilizzato per l&#39;applicazione dell&#39;elenco consentiti AIR non corrisponde all&#39;ID del server di pubblicazione specificato dal server di pubblicazione dell&#39;applicazione nel [!DNL application.xml] file.

## Utilizzo della riga di comando dell&#39;utilità AIR Publisher ID {#air-publisher-id-utility-command-line-usage}

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

* `signaturefile` specifica un percorso per l&#39;applicazione AIR [!DNL signatures.xml] file, nelle applicazioni [!DNL META-INF] directory

* `signingcert` specifica il certificato utilizzato per firmare un’applicazione AIR

>[!NOTE]
>
>Per determinare l&#39;ID dell&#39;editore di un&#39;applicazione Android, è necessario utilizzare `-s` per specificare il certificato utilizzato per firmare il pacchetto dell’applicazione Android (APK). Per creare applicazioni Android in grado di riprodurre contenuti protetti da Primetime DRM è necessario utilizzare Primetime DRM.
