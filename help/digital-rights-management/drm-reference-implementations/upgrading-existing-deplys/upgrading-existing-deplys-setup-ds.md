---
title: Configurare un server di dominio
description: Configurare un server di dominio
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 0%

---

# Configurare un server di dominio{#set-up-a-domain-server}

Per configurare un server di dominio in un&#39;installazione di un server licenze esistente:

1. In [!DNL tomcat/lib] , aprire la [!DNL flashaccess-refimpl.properties] file.
1. Sotto `Domain CA certificate` , completa il certificato CA del dominio.

   Questo certificato viene quindi utilizzato per accettare i token di dominio.
1. Sotto `Domain CA credential` , completa il `Domain CA credential certificate (PFX)` dettagli.

   Questo certificato viene quindi utilizzato per firmare certificati e token di dominio.
1. Specifica il valore per `DomainServerlURL`.

   Se questo valore è impostato su `NULL`, l&#39;autenticazione del dominio potrebbe avere esito positivo. Tuttavia, durante l’aggiunta al dominio, potrebbe verificarsi un errore di aggiunta al dominio.
