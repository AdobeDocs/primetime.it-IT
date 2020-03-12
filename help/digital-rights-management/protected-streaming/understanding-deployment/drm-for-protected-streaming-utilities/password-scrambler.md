---
description: L'utility Password Scrambler crittografa una password per i file di configurazione Adobe Primetime DRM Server for Protected Streaming.
seo-description: L'utility Password Scrambler crittografa una password per i file di configurazione Adobe Primetime DRM Server for Protected Streaming.
seo-title: Scrambler password
title: Scrambler password
uuid: 56df0f49-f3fd-464d-b4ba-25e1b497158a
translation-type: tm+mt
source-git-commit: 105dedcfe47a5f454a067e66a95827e638290742

---


# Scrambler password {#password-scrambler}

L&#39;utility Password Scrambler crittografa una password per i file di configurazione Adobe Primetime DRM Server for Protected Streaming.

Per eseguire lo scorrimento, digitare:

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

L&#39;utilità visualizza il messaggio seguente:

```
Encrypted password:  
<i class="+ topic ph hi-d="" i "="">
  scrambled-password 
</i class="+ topic>
```

Tutte le password specificate nei [!DNL flashaccess-global.xml] file e [!DNL flashaccess-tenant.xml] devono essere crittografate.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>L&#39;utility Password Scrambler nel server DRM di Primetime per lo streaming protetto non è intercambiabile con lo scanner fornito con il server delle licenze di implementazione di riferimento.