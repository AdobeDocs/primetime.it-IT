---
title: Utilizzo della riga di comando
description: Utilizzo della riga di comando
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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

* `signaturefile` specifica il percorso del file signatures.xml dell&#39;applicazione AIR, che si trova nelle applicazioni [!DNL META-INF] directory

* `signingcert` specifica il certificato utilizzato per firmare l’applicazione AIR

>[!NOTE]
>
>Per determinare l’ID dell’editore di un’applicazione iOS, utilizza `-s` e specifica il certificato utilizzato per firmare l’applicazione iOS. ***Adobe Primetime è richiesto per creare applicazioni iOS in grado di riprodurre contenuti protetti da Access***.
