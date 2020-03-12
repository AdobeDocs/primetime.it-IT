---
seo-title: Configurare SSL sul server BEES
title: Configurare SSL sul server BEES
uuid: 041a106e-8b21-4018-815d-b7ea48c3de03
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# Configurare SSL sul server BEES {#configure-ssl-on-your-bees-server}

1. Fornite il certificato SSL del server al vostro contatto Adobe che ha fornito il software.

   Il certificato verrà aggiunto come certificato attendibile all&#39;archivio dei trust DRM di Primetime Cloud.
1. Per abilitare l&#39;autenticazione client per la connessione SSL (disabilitata in questa versione):
   1. Aggiungete i certificati `[!DNL clouddrm-transport.cer]` e `[!DNL AdobeFlashAccessIntermediateCA.cer]` gli store attendibili utilizzati per l&#39;autenticazione client.
   1. Abilitate l&#39;autenticazione client nella configurazione SSL.
