---
title: Configurare SSL sul server BEES
description: Configurare SSL sul server BEES
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---

# Configurare SSL sul server BEES {#configure-ssl-on-your-bees-server}

1. Fornisci il certificato SSL del server al tuo contatto Adobe che ha fornito questo software.

   Il certificato verrà aggiunto come attendibile all&#39;archivio attendibile di Primetime Cloud DRM.
1. Per abilitare l&#39;autenticazione client per la connessione SSL (disabilitata in questa versione):
   1. Aggiungi il `[!DNL clouddrm-transport.cer]` e `[!DNL AdobeFlashAccessIntermediateCA.cer]` certificati all&#39;archivio fonti attendibili utilizzati per l&#39;autenticazione client.
   1. Abilita l’autenticazione client nella configurazione SSL.
