---
description: L'utilità Scrambler password crittografa una password per i file di configurazione di Adobe Primetime DRM Server for Protected Streaming.
title: Scrambler password
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# Scrambler password {#password-scrambler}

L&#39;utilità Scrambler password crittografa una password per i file di configurazione di Adobe Primetime DRM Server for Protected Streaming.

Per eseguire lo scrambler, digitare:

```
Scrambler.bat  
<i class="+ topic ph hi-d="" i "="">
  password 
</i class="+ topic>
```

o

```
java -jar libs/flashaccess-scrambler.jar  
<i class="+ topic ph hi-d="" i "="">
  password  
</i class="+ topic>
```

L&#39;utility visualizza il seguente messaggio:

```
Encrypted password:  
<i class="+ topic ph hi-d="" i "="">
  scrambled-password 
</i class="+ topic>
```

Tutte le password specificate in [!DNL flashaccess-global.xml] e [!DNL flashaccess-tenant.xml] i file devono essere crittografati.

>[!NOTE]
>
>L&#39;utilità Scrambler password nel server DRM Primetime per lo streaming protetto non è intercambiabile con lo scrambler fornito con il server licenze di implementazione di riferimento.
