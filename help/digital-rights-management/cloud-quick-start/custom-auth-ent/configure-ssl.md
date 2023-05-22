---
title: Configurare SSL sul server BEES
description: Configurare SSL sul server BEES
copied-description: true
exl-id: 6823a71c-3be6-4c07-a3e6-e16bd931deaf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
