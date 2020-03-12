---
seo-title: Scrambler password
title: Scrambler password
uuid: e488babc-cd50-41b9-acb8-490e8e42e8bc
translation-type: tm+mt
source-git-commit: 47b2ed65ff0ea4f54a210cf7627ed535782296b9

---


# Scrambler password {#password-scrambler}

L&#39;utility Password Scrambler crittografa una password in modo che possa essere utilizzata nei file di configurazione Adobe Access Server per lo streaming protetto. Per eseguire lo scorrimento, eseguite il comando:

```
Scrambler.bat password 
```

o il comando:

```
java -jar libs/flashaccess-scrambler.jar password  
```

L&#39;utilità genera il seguente messaggio:

```
Encrypted password: scrambled-password 
```

Tutte le password specificate in flashaccess-global.xml e flashaccess-tenant.xml devono essere crittografate.

>[!NOTE]
>
>L&#39;utility Password Scrambler in Adobe Access Server for Protected Streaming non è intercambiabile con lo scanner fornito con il server delle licenze di implementazione di riferimento.

