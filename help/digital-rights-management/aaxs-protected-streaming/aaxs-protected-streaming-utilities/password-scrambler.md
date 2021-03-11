---
title: Password Scrambler
description: Password Scrambler
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 0%

---


# Scrambler di password {#password-scrambler}

L&#39;utility Password Scrambler crittografa una password in modo che possa essere utilizzata in Adobe Access Server per i file di configurazione Protected Streaming. Per eseguire lo scrambler, esegui il comando:

```
Scrambler.bat password 
```

o il comando:

```
java -jar libs/flashaccess-scrambler.jar password  
```

L&#39;utilità invia il seguente messaggio:

```
Encrypted password: scrambled-password 
```

Tutte le password specificate in flashaccess-global.xml e flashaccess-tenant.xml devono essere crittografate.

>[!NOTE]
>
>L&#39;utility Password Scrambler in Adobe Access Server per lo streaming protetto non è intercambiabile con lo scanner fornito con il server licenze di implementazione di riferimento.

