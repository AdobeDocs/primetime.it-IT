---
title: Caricamento sicuro degli annunci tramite HTTPS
description: Caricamento sicuro degli annunci tramite HTTPS
copied-description: true
exl-id: d43418e9-631b-4344-a5b3-0a6154a325d4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---

# Caricamento sicuro degli annunci tramite HTTPS{#secure-ad-loading-over-https}

Adobe Primetime può richiedere server di annunci di terze parti tramite https anche se il lettore è ospitato su http. Solo le chiamate ad-server vengono aggiornate a https richieste dal client durante la fase di risoluzione degli annunci di Auditude.

>[!NOTE]
>
>Questa funzione non è supportata per il Flash.

Utilizza quanto segue per abilitare il caricamento sicuro degli annunci. Per impostazione predefinita, non è attivato.

```
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
auditudeSettings.forceHttpsConfiguration.adServerCalls = true;
```
