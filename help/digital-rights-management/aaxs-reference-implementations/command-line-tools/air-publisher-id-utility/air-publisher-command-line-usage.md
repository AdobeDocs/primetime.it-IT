---
seo-title: Utilizzo della riga di comando
title: Utilizzo della riga di comando
uuid: 54b1e867-c6cc-4355-b8e6-a7ec910bd33d
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---


# Utilizzo della riga di comando {#command-line-usage}

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

* 
   * `signaturefile`* specifica il percorso del file signatures.xml dell&#39;applicazione AIR, che si trova nella  [!DNL META-INF] directory delle applicazioni

* `signingcert` specifica il certificato utilizzato per firmare l&#39;applicazione AIR

>[!NOTE]
>
>Per determinare l&#39;ID editore per un&#39;applicazione iOS, utilizzate l&#39;opzione `-s` e specificate il certificato utilizzato per firmare l&#39;applicazione iOS. ***Adobe Primetime è richiesto per creare applicazioni iOS in grado di riprodurre contenuto*** protetto da Access.

