---
description: Puoi generare token Expressplay per il contenuto crittografato inviando richieste di token al server token Expressplay appropriato.
title: Token esplicativi
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 0%

---


# Token espliciti {#expressplay-tokens}

Puoi generare token Expressplay per il contenuto crittografato inviando richieste di token al server token Expressplay appropriato.

Un esempio è il seguente URL:

```
https://wv-gen.service.expressplay.com/hms/wv/
token?customerAuthenticator=<your expressplay customer authenticator>
&kid=fd1a706ac2b36002888f6d4a414333c3
&contentKey=5438b719bf47a2f5678237477db2f9e6
&securityLevel=1
&hdcpOutputControl=0
```

L&#39;ID di archiviazione della chiave di crittografia del contenuto o CEKSID assegnato al parametro `kid` e la chiave di crittografia del contenuto o CEK fornita al parametro `contentKey` devono corrispondere all&#39;ID di archiviazione della chiave di crittografia del contenuto e alla chiave di crittografia del contenuto utilizzata per il package. Il testo seguente è un esempio della risposta del server token:

```
https://wv.service.expressplay.com/hms/wv/rights/
?ExpressPlayToken=AQAAABIDKbgAAABQbt68jktab0YRY-r9mo6VP
 VqDDvkHq78x4V9_AyBUTtcNFHw5JtNKlKrMt-4HBdJ3Fopr7fqFSBp
 SJ4o-d8teAkUZUtW3Od5V-SHsCLnAlbFW84K71h2xNUiMAvRcUFBG3bjxMQ
```

È possibile

* utilizza l’URL restituito e utilizza la query come URL del server licenze, oppure
* elimina la query dall’URL e passa il token ExpressPlayToken separatamente come intestazione HTTP POST