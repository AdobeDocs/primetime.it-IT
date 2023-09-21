---
title: Scrambler password
description: Scrambler password
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 0%

---

# Scrambler password {#password-scrambler}

L&#39;utilità Scrambler password crittografa una password in modo che possa essere utilizzata nei file di configurazione di Adobe Access Server for Protected Streaming. Per eseguire lo scrambler, eseguire il comando:

```
Scrambler.bat password 
```

oppure il comando:

```
java -jar libs/flashaccess-scrambler.jar password  
```

L&#39;utility restituisce il seguente messaggio:

```
Encrypted password: scrambled-password 
```

Tutte le password specificate in flashaccess-global.xml e flashaccess-tenant.xml devono essere crittografate.

>[!NOTE]
>
>L&#39;utilità Scrambler password in Adobe Access Server for Protected Streaming non è intercambiabile con lo scrambler fornito con Reference Implementation License Server.
