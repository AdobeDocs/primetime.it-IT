---
title: Panoramica della topologia di rete
description: Panoramica della topologia di rete
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---


# Panoramica della topologia di rete {#network-topology-overview}

Dopo aver implementato correttamente Adobe Access, è importante mantenere la sicurezza dell’ambiente. Questa sezione descrive le attività necessarie per mantenere la sicurezza del server di produzione di Adobe Access.

Utilizza un *proxy inverso* per garantire che diversi set di URL per le applicazioni web di Adobe Access siano disponibili per gli utenti sia esterni che interni. Questa configurazione è più sicura che consente agli utenti di connettersi direttamente al server dell&#39;applicazione su cui è in esecuzione Adobe Access. Il proxy inverso esegue tutte le richieste HTTP per l&#39;application server che esegue Adobe Access. Gli utenti hanno solo accesso di rete al proxy inverso e possono tentare solo le connessioni URL supportate dal proxy inverso.

<!--<a id="fig-frx-dcg-44"></a>-->

![](assets/AdobeAccess_4_SecureDeployment_web.png)

