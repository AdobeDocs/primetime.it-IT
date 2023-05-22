---
title: Configurare un server di dominio
description: Configurare un server di dominio
copied-description: true
exl-id: eeb0d39d-58a4-4414-9123-2cf1b27b73de
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
