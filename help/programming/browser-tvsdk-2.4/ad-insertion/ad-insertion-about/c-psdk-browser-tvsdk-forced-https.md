---
title: Caricamento sicuro degli annunci tramite HTTPS
description: Caricamento sicuro degli annunci tramite HTTPS
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---


# Caricamento annunci sicuro su HTTPS{#secure-ad-loading-over-https}

Adobe Primetime può richiedere server di annunci di terze parti su https anche se il lettore è ospitato su http. Solo le chiamate ad-server vengono aggiornate a https che il client cerca durante la fase del risolutore di annunci Auditude.

>[!NOTE]
>
>Questa funzionalità non è supportata ad Flash.

Utilizza quanto segue per abilitare il caricamento sicuro degli annunci. Non è abilitata per impostazione predefinita.

```
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
auditudeSettings.forceHttpsConfiguration.adServerCalls = true;
```
