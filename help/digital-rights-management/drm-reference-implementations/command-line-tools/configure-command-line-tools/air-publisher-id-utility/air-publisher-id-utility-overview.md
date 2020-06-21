---
seo-title: Panoramica
title: Panoramica
uuid: f45c6b58-53c5-41e0-be3d-590231dd214a
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# AIR Publisher ID {#air-publisher-id-utility}

Quando create un file AIR, ADT (AIR Developer Tool) genera automaticamente un ID Publisher. L&#39;utility AIR Publisher ID ( [!DNL AdobePublisherIDUtility.jar]) calcola l&#39;ID Publisher per un&#39;applicazione AIR.

L&#39;ID editore è univoco per il certificato utilizzato per creare un file AIR. Se riutilizzate lo stesso certificato per più applicazioni AIR, tutte le applicazioni AIR hanno lo stesso ID editore. Una versione AIR che ha esito positivo alla release 1.5.2 non aggiunge l&#39;ID editore generato a un file. Di conseguenza, se intendete utilizzare un elenco di applicazioni AIR allow, utilizzate questo strumento per determinare l&#39;ID editore.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>L&#39;ID editore utilizzato per AIR consente l&#39;imposizione degli elenchi non è lo stesso ID editore specificato dall&#39;editore nel [!DNL application.xml] file dell&#39;applicazione.

## Utilizzo della riga di comando dell&#39;utility ID di AIR Publisher {#air-publisher-id-utility-command-line-usage}

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
   * `signaturefile`* specifica il percorso del [!DNL signatures.xml] file dell&#39;applicazione AIR, che si trova nella directory delle applicazioni [!DNL META-INF]

* `signingcert` specifica il certificato utilizzato per firmare un&#39;applicazione AIR

>[!NOTE]
>
>Per determinare l&#39;ID editore per un&#39;applicazione Android, dovete utilizzare l&#39; `-s` opzione per specificare il certificato utilizzato per firmare il pacchetto dell&#39;applicazione Android (APK). Primetime DRM è richiesto per creare applicazioni Android in grado di riprodurre contenuto protetto da DRM di Primetime.