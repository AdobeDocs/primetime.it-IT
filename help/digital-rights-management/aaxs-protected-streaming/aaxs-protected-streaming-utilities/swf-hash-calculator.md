---
title: Calcolatore hash SWF
description: Calcolatore hash SWF
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
