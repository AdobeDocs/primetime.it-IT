---
description: Puoi generare token Expressplay per il contenuto crittografato inviando richieste di token al server token Expressplay appropriato.
title: Espressione dei token
exl-id: 38faba06-6737-4dec-ac97-27db3124b993
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 0%

---

# Espressione dei token {#expressplay-tokens}

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

L&#39;ID di archiviazione o CEKSID della chiave di crittografia del contenuto fornito al `kid` e la chiave di crittografia del contenuto o CEK assegnato al `contentKey` Il parametro deve corrispondere all&#39;ID di archiviazione della chiave di crittografia del contenuto e alla chiave di crittografia del contenuto utilizzate per la creazione del pacchetto. Il testo seguente è un esempio della risposta del server token:

```
https://wv.service.expressplay.com/hms/wv/rights/
?ExpressPlayToken=AQAAABIDKbgAAABQbt68jktab0YRY-r9mo6VP
 VqDDvkHq78x4V9_AyBUTtcNFHw5JtNKlKrMt-4HBdJ3Fopr7fqFSBp
 SJ4o-d8teAkUZUtW3Od5V-SHsCLnAlbFW84K71h2xNUiMAvRcUFBG3bjxMQ
```

È quindi possibile:

* utilizzare l&#39;URL restituito e la query come URL del server licenze oppure
* elimina la query dall’URL e passa ExpressPlayToken separatamente come intestazione HTTP POST
