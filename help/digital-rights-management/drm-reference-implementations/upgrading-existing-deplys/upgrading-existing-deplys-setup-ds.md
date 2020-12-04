---
description: 'null'
seo-description: 'null'
seo-title: Configurare un server di dominio
title: Configurare un server di dominio
uuid: bf85305e-9a00-4bc0-ba36-c870979456e4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---


# Configurare un server di dominio{#set-up-a-domain-server}

Per configurare un server di dominio su un&#39;installazione del server di licenze esistente:

1. Nella directory [!DNL tomcat/lib], aprire il file [!DNL flashaccess-refimpl.properties].
1. In `Domain CA certificate`, completare il certificato Domain CA.

   Questo certificato viene quindi utilizzato per accettare i token di dominio.
1. Sotto l&#39;opzione `Domain CA credential`, completare i dettagli `Domain CA credential certificate (PFX)`.

   Questo certificato viene quindi utilizzato per la firma di certificati di dominio e token.
1. Specificare il valore per `DomainServerlURL`.

   Se questo valore è impostato su `NULL`, l&#39;autenticazione del dominio potrebbe avere esito positivo. Tuttavia, durante l&#39;adesione al dominio, potrebbe verificarsi un errore di join domain.
