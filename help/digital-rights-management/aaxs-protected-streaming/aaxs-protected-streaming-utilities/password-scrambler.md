---
seo-title: Scrambler password
title: Scrambler password
uuid: e488babc-cd50-41b9-acb8-490e8e42e8bc
translation-type: tm+mt
source-git-commit: 47b2ed65ff0ea4f54a210cf7627ed535782296b9
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 0%

---


# Scrambler password {#password-scrambler}

L&#39;utility Password Scrambler codifica una password in modo che possa essere utilizzata in Adobe Access Server per i file di configurazione per lo streaming protetto. Per eseguire lo scorrimento, eseguite il comando:

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
>L&#39;utility Password Scrambler di Adobe Access Server per lo streaming protetto non è intercambiabile con lo scanner fornito con il server delle licenze di implementazione di riferimento.

