---
title: Calcolatore hash SWF
description: Calcolatore hash SWF
copied-description: true
exl-id: 651b31bc-47b5-4388-aa00-27d3bd59da30
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '52'
ht-degree: 0%

---

# Calcolatore hash SWF{#swf-hash-calculator}

L&#39;utility SWF Hash Calculator ha calcolato il digest di un&#39;applicazione SWF presente in un file. Per eseguire il comando hasher, esegui il comando:

```
Hasher.bat filename.swf
```

oppure il comando:

```
java -jar libs/flashaccess-hasher.jar filename.swf
```

L&#39;utility genera il seguente messaggio:

```
SWF Hash: hash-of-swf
```

Questo valore può essere utilizzato per specificare il digest SWF in [!DNL flashaccess-tenant.xml].
