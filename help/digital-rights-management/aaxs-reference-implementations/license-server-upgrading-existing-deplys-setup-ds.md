---
seo-title: Configurare un server di dominio
title: Configurare un server di dominio
uuid: b262ea86-f465-4ed1-b278-122d4dafc881
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---


# Configurare un server di dominio {#set-up-a-domain-server}

Per configurare il server di dominio su un&#39;installazione del server di licenze esistente, eseguire le operazioni seguenti:

1. Aprire il file [!DNL flashaccess-refimpl.properties] in [!DNL tomcat/lib].

1. Sotto l&#39;opzione `Domain CA certificate`, compilare i dettagli del certificato CA del dominio. Questo certificato verrà utilizzato per accettare i token di dominio.
1. Sotto l&#39;opzione `Domain CA credential`, inserite i dettagli `Domain CA credential certificate (PFX)`. Questo certificato verrà utilizzato per la firma dei certificati di dominio e dei token.

1. Specificare il valore per `DomainServerlURL`. Se questo valore è NULL, l&#39;autenticazione del dominio potrebbe avere esito positivo. Tuttavia, durante l&#39;adesione al dominio, si verificherà un errore di join domain.

