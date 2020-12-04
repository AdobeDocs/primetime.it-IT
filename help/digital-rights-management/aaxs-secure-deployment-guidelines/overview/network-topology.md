---
seo-title: Panoramica della topologia di rete
title: Panoramica della topologia di rete
uuid: 1558b7fa-dc0d-477c-8f1c-9c6f3718e1b0
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---


# Panoramica della topologia di rete {#network-topology-overview}

Dopo aver implementato con successo  Accesso al Adobe, è importante mantenere la sicurezza dell&#39;ambiente. In questa sezione vengono descritte le attività necessarie per mantenere la sicurezza del server di produzione  Access.

Utilizzate un *proxy inverso* per garantire che diversi set di URL per  applicazioni Web di accesso ai Adobi siano disponibili sia per gli utenti esterni che per quelli interni. Questa configurazione è più sicura che consentire agli utenti di connettersi direttamente al server dell&#39;applicazione su cui è in esecuzione  accesso al Adobe. Il proxy inverso esegue tutte le richieste HTTP per il server applicazione che esegue  Adobe Access. Gli utenti dispongono solo dell&#39;accesso di rete al proxy inverso e possono tentare solo le connessioni URL supportate dal proxy inverso.

<!--<a id="fig-frx-dcg-44"></a>-->

![](assets/AdobeAccess_4_SecureDeployment_web.png)

