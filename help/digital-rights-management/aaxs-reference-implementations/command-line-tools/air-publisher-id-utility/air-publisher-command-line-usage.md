---
title: Uso della riga di comando
description: Uso della riga di comando
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---


# Uso della riga di comando {#command-line-usage}

Per eseguire lo strumento, utilizzare la sintassi seguente:

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

* `signaturefile` specifica il percorso del file signatures.xml dell’applicazione AIR, che si trova nella  [!DNL META-INF] directory delle applicazioni

* `signingcert` specifica il certificato utilizzato per firmare l’applicazione AIR

>[!NOTE]
>
>Per determinare l&#39;ID editore per un&#39;applicazione iOS, utilizza l&#39;opzione `-s` e specifica il certificato utilizzato per firmare l&#39;applicazione iOS. ***Adobe Primetime è necessario per creare applicazioni iOS in grado di riprodurre contenuti*** protetti da Access.

