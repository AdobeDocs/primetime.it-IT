---
title: Configurare un server di dominio
description: Configurare un server di dominio
copied-description: true
exl-id: b2589412-25e4-44c8-be11-8b2cfccbf7bb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
