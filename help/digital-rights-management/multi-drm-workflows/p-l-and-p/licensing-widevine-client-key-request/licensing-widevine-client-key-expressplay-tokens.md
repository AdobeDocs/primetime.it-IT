---
description: Potete generare token Expressplay per il contenuto crittografato inviando richieste di token al server di token Expressplay appropriato.
seo-description: Potete generare token Expressplay per il contenuto crittografato inviando richieste di token al server di token Expressplay appropriato.
seo-title: Token espliciti
title: Token espliciti
uuid: 6103e1b2-127d-4758-a589-15f0f3c73db1
translation-type: tm+mt
source-git-commit: d0ba1f98b16f6350ae842ca2ce1261bf49dd8a66
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# Token espliciti {#expressplay-tokens}

Potete generare token Expressplay per il contenuto crittografato inviando richieste di token al server di token Expressplay appropriato.

Un esempio è costituito dal seguente URL:

```
https://wv-gen.service.expressplay.com/hms/wv/
token?customerAuthenticator=<your expressplay customer authenticator>
&kid=fd1a706ac2b36002888f6d4a414333c3
&contentKey=5438b719bf47a2f5678237477db2f9e6
&securityLevel=1
&hdcpOutputControl=0
```

L&#39;ID di archiviazione o CEKSID della chiave di crittografia del contenuto fornito al parametro `kid` e la chiave di crittografia del contenuto o CEK data al parametro `contentKey` devono corrispondere all&#39;ID di memorizzazione della chiave di crittografia del contenuto e alla chiave di crittografia del contenuto utilizzata per la creazione del pacchetto. Il testo seguente è un esempio della risposta del server token:

```
https://wv.service.expressplay.com/hms/wv/rights/
?ExpressPlayToken=AQAAABIDKbgAAABQbt68jktab0YRY-r9mo6VP
 VqDDvkHq78x4V9_AyBUTtcNFHw5JtNKlKrMt-4HBdJ3Fopr7fqFSBp
 SJ4o-d8teAkUZUtW3Od5V-SHsCLnAlbFW84K71h2xNUiMAvRcUFBG3bjxMQ
```

È possibile

* utilizzare l&#39;URL restituito e la query come URL del server licenze, oppure
* estrarre la query dall’URL e trasmettere il token ExpressPlayToken separatamente come intestazione POST HTTP