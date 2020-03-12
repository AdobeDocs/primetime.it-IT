---
description: 'null'
seo-description: 'null'
seo-title: Proteggere il caricamento di annunci tramite HTTPS
title: Proteggere il caricamento di annunci tramite HTTPS
uuid: 10657f59-cfbf-4c75-9249-fc154952bc51
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Proteggere il caricamento di annunci tramite HTTPS{#secure-ad-loading-over-https}

Adobe Primetime può richiedere server di annunci di terze parti tramite https anche se il lettore è ospitato su http. Solo le chiamate ad-server vengono aggiornate a https che il client cerca durante la fase del risolutore di Auditude Ad.

>[!NOTE]
>
>Questa funzione non è supportata per Flash.

Utilizzate quanto segue per abilitare il caricamento sicuro degli annunci. Per impostazione predefinita non è attivato.

```
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
auditudeSettings.forceHttpsConfiguration.adServerCalls = true;
```
