---
title: Caricamento sicuro degli annunci tramite HTTPS
description: Caricamento sicuro degli annunci tramite HTTPS
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---

# Caricamento sicuro degli annunci tramite HTTPS{#secure-ad-loading-over-https}

Adobe Primetime può richiedere server di annunci di terze parti tramite https anche se il lettore è ospitato su http. Solo le chiamate ad-server vengono aggiornate a https che il client cerca durante la fase di Auditude dell’Ad resolver.

>[!NOTE]
>
>Questa funzione non è supportata per il Flash.

Utilizza quanto segue per abilitare il caricamento sicuro degli annunci. Per impostazione predefinita, non è attivato.

```
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
auditudeSettings.forceHttpsConfiguration.adServerCalls = true;
```
