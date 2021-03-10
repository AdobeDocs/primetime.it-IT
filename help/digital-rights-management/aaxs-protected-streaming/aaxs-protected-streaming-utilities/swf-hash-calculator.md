---
title: Calcolatore hash SWF
description: Calcolatore hash SWF
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '52'
ht-degree: 0%

---


# Calcolatore hash SWF{#swf-hash-calculator}

L&#39;utilità di calcolo hash SWF ha calcolato il digest di un&#39;applicazione SWF che si trova in un file. Per eseguire l&#39;applicazione, esegui il comando:

```
Hasher.bat filename.swf
```

o il comando:

```
java -jar libs/flashaccess-hasher.jar filename.swf
```

L&#39;utilità genera il seguente messaggio:

```
SWF Hash: hash-of-swf
```

Questo valore può essere utilizzato per specificare il digest SWF in [!DNL flashaccess-tenant.xml].
