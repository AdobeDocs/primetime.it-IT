---
description: L'utility Password Scrambler crittografa una password per il server DRM di Adobe Primetime per i file di configurazione Protected Streaming.
title: Scrambler di password
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---


# Scrambler di password {#password-scrambler}

L&#39;utility Password Scrambler crittografa una password per il server DRM di Adobe Primetime per i file di configurazione Protected Streaming.

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

L&#39;utilità visualizza il seguente messaggio:

```
Encrypted password:  
<i class="+ topic ph hi-d="" i "="">
  scrambled-password 
</i class="+ topic>
```

Tutte le password specificate nei file [!DNL flashaccess-global.xml] e [!DNL flashaccess-tenant.xml] devono essere crittografate.

>[!NOTE]
>
>L&#39;utility Password Scrambler nel server DRM di Primetime per lo streaming protetto non è intercambiabile con lo scrambler fornito con il server delle licenze di implementazione di riferimento.