---
title: Panoramica della topologia di rete
description: Panoramica della topologia di rete
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# Panoramica {#network-topology-overview}

Dopo aver implementato correttamente Adobe Primetime DRM, è necessario mantenere la sicurezza del server di produzione DRM di Primetime.

>[!NOTE]
>
>Primetime DRM era noto in precedenza come Adobe Access e prima di questo, Flash Access.

È possibile utilizzare un *reverse proxy* per garantire che diversi set di URL per le applicazioni web DRM di Primetime siano disponibili per gli utenti esterni e interni. *Il* proxy inverso è più sicuro che consentire agli utenti di connettersi direttamente al server dell&#39;applicazione su cui viene eseguito DRM di Primetime e questa configurazione esegue tutte le richieste HTTP per il server dell&#39;applicazione che esegue DRM di Primetime. Gli utenti possono accedere solo al proxy inverso e possono tentare solo le connessioni URL supportate dal proxy inverso.

<!--<a id="fig_8083A8C794B646CD87985EC891B60663"></a>-->

![](assets/AdobeAccess_4_SecureDeployment.png)