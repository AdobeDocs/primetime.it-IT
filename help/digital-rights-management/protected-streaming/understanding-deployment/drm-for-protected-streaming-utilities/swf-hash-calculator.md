---
description: L'utility SWF Hash Calculator calcola il digest di un'applicazione SWF che si trova in un file.
title: Calcolatore hash SWF
exl-id: 245254fe-2fcb-41e8-94bd-0cbc8b39b2b5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '65'
ht-degree: 0%

---

# Calcolatore hash SWF{#swf-hash-calculator}

L&#39;utility SWF Hash Calculator calcola il digest di un&#39;applicazione SWF che si trova in un file.

Per eseguire l&#39;acceleratore, digitare:

```
Hasher.bat 
<i class="+ topic ph hi-d="" i "="">
  filename.swf
</i class="+ topic>
```

o

```
java -jar libs/flashaccess-hasher.jar 
<i class="+ topic ph hi-d="" i "="">
  filename.swf
</i class="+ topic>
```

L&#39;utility visualizza il seguente messaggio:

```
SWF Hash: 
<i class="+ topic ph hi-d="" i "="">
  hash-of-swf
</i class="+ topic>
```

Puoi utilizzare questo valore per specificare il digest SWF in [!DNL flashaccess-tenant.xml].
