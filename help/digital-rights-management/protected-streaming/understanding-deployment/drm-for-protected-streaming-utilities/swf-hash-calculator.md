---
description: L'utility SWF Hash Calculator calcola il digest di un'applicazione SWF che si trova in un file.
title: Calcolatore hash SWF
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
