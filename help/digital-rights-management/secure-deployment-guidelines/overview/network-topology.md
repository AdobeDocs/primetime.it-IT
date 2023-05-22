---
title: Panoramica della topologia di rete
description: Panoramica della topologia di rete
copied-description: true
exl-id: a4737ea3-407a-48fd-ae3e-4df56a4c1812
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# Panoramica {#network-topology-overview}

Dopo aver distribuito correttamente Adobe Primetime DRM, è necessario mantenere la sicurezza del server di produzione di Primetime DRM.

>[!NOTE]
>
>DRM di Primetime era noto in precedenza come accesso di Adobe e prima ancora come Flash Access.

È possibile utilizzare una *proxy inverso* per garantire la disponibilità di diversi set di URL per le applicazioni Web DRM Primetime per utenti esterni e interni. *Inverti proxy* è più sicuro di consentire agli utenti di connettersi direttamente al server applicazioni su cui viene eseguito Primetime DRM e questa configurazione esegue tutte le richieste HTTP per il server applicazioni che esegue Primetime DRM. Gli utenti possono accedere solo al proxy inverso e tentare solo le connessioni URL supportate dal proxy inverso.

<!--<a id="fig_8083A8C794B646CD87985EC891B60663"></a>-->

![](assets/AdobeAccess_4_SecureDeployment.png)
