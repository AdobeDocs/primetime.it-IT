---
title: Configurare un server di dominio
description: Configurare un server di dominio
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---


# Configurare un server di dominio {#set-up-a-domain-server}

Per configurare il server di dominio in un&#39;installazione di un server licenze esistente, eseguire le operazioni seguenti:

1. Apri il file [!DNL flashaccess-refimpl.properties] in [!DNL tomcat/lib].

1. Sotto l&#39;opzione `Domain CA certificate`, compila i dettagli del certificato Domain CA. Questo certificato verrà utilizzato per accettare i token di dominio.
1. Sotto l’opzione `Domain CA credential` , compila i dettagli `Domain CA credential certificate (PFX)` . Questo certificato verrà utilizzato per la firma di certificati di dominio e token.

1. Specifica il valore per `DomainServerlURL`. Se questo valore è NULL, l&#39;autenticazione del dominio potrebbe avere esito positivo. Tuttavia, durante l’accesso al dominio, si verificherà un errore di join domain.

