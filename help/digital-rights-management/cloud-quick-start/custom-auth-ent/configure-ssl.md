---
title: Configurare SSL sul server API
description: Configurare SSL sul server API
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---


# Configurare SSL sul server BEES {#configure-ssl-on-your-bees-server}

1. Fornisci il certificato SSL del server al contatto Adobe che ha fornito questo software.

   Il certificato verrà aggiunto come certificato attendibile all’archivio attendibilità DRM di Primetime Cloud.
1. Per abilitare l’autenticazione client per la connessione SSL (disabilitata in questa versione):
   1. Aggiungi i certificati `[!DNL clouddrm-transport.cer]` e `[!DNL AdobeFlashAccessIntermediateCA.cer]` all&#39;archivio dei trust utilizzato per l&#39;autenticazione client.
   1. Abilita l’autenticazione client nella configurazione SSL.
