---
title: Panoramica della topologia di rete
description: Panoramica della topologia di rete
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---

# Panoramica della topologia di rete {#network-topology-overview}

Dopo aver distribuito correttamente Adobe Access, è importante mantenere la sicurezza dell’ambiente. In questa sezione vengono descritte le attività necessarie per garantire la protezione del server di produzione Adobe Access.

Utilizza un *proxy inverso* per garantire che diversi set di URL, ad Adobe le applicazioni web di Access, siano disponibili sia per gli utenti esterni che per quelli interni. Questa configurazione è più sicura di quella che consente agli utenti di connettersi direttamente al server applicazioni sul quale è in esecuzione Adobe Access. Il proxy inverso esegue tutte le richieste HTTP per il server applicazioni che esegue Adobe Access. Gli utenti dispongono solo dell&#39;accesso di rete al proxy inverso e possono tentare solo le connessioni URL supportate dal proxy inverso.

<!--<a id="fig-frx-dcg-44"></a>-->

![](assets/AdobeAccess_4_SecureDeployment_web.png)
