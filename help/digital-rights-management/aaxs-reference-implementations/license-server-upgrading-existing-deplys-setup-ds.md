---
title: Configurare un server di dominio
description: Configurare un server di dominio
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# Configurare un server di dominio {#set-up-a-domain-server}

Per configurare il server di dominio in un&#39;installazione esistente del server licenze, eseguire le operazioni seguenti:

1. Apri [!DNL flashaccess-refimpl.properties] file in [!DNL tomcat/lib].

1. Sotto `Domain CA certificate` , compilare i dettagli del certificato CA del dominio. Questo certificato verrà utilizzato per accettare i token di dominio.
1. Sotto `Domain CA credential` , compila il `Domain CA credential certificate (PFX)` dettagli. Questo certificato verrà utilizzato per la firma di certificati di dominio e token.

1. Specifica il valore per `DomainServerlURL`. Se il valore è NULL, l&#39;autenticazione del dominio potrebbe avere esito positivo. Tuttavia, durante l’aggiunta al dominio si verifica un errore di aggiunta al dominio.
