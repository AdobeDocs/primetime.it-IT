---
description: L'utilità di calcolo hash SWF calcola il digest di un'applicazione SWF che si trova in un file.
title: Calcolatore hash SWF
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '65'
ht-degree: 0%

---


# Calcolatore hash SWF{#swf-hash-calculator}

L&#39;utilità di calcolo hash SWF calcola il digest di un&#39;applicazione SWF che si trova in un file.

Per eseguire il carattere di hasher, digita:

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

L&#39;utilità visualizza il seguente messaggio:

```
SWF Hash: 
<i class="+ topic ph hi-d="" i "="">
  hash-of-swf
</i class="+ topic>
```

È possibile utilizzare questo valore per specificare il digest SWF in [!DNL flashaccess-tenant.xml].
