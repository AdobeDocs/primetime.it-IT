---
title: Uso della riga di comando
description: Uso della riga di comando
copied-description: true
exl-id: 67056085-beb5-4f54-8962-369bc32d7907
source-git-commit: 79cab347d0daa01549fbf8a9b37bf0a91c14648e
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

* `signaturefile` specifica il percorso del file signatures.xml dell’applicazione AIR, che si trova nelle applicazioni [!DNL META-INF] directory

* `signingcert` specifica il certificato utilizzato per firmare l’applicazione AIR

>[!NOTE]
>
>Per determinare l&#39;ID editore per un&#39;applicazione iOS, utilizza l&#39; `-s` e specifica il certificato utilizzato per firmare l’applicazione iOS. ***Adobe Primetime è necessario per creare applicazioni iOS in grado di riprodurre contenuti protetti da Access***.
