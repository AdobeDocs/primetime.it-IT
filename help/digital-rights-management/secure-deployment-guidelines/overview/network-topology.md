---
seo-title: Panoramica della topologia di rete
title: Panoramica della topologia di rete
uuid: b8b072dc-8dc0-46ba-bb01-1e9b58af2681
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Panoramica {#network-topology-overview}

Dopo aver implementato correttamente Adobe Primetime DRM, è necessario mantenere la sicurezza del server di produzione DRM Primetime.

>[!NOTE]
>
>Primetime DRM era precedentemente noto come Adobe Access e prima di tale era Flash Access.

Potete utilizzare un proxy ** inverso per garantire che diversi set di URL per le applicazioni Web DRM di Primetime siano disponibili per gli utenti interni ed esterni. *Il proxy* inverso è più sicuro che consentire agli utenti di connettersi direttamente al server applicazione su cui viene eseguito Primetime DRM e questa configurazione esegue tutte le richieste HTTP per il server applicazione che esegue Primetime DRM. Gli utenti possono accedere solo al proxy inverso e possono tentare solo le connessioni URL supportate dal proxy inverso.

<!--<a id="fig_8083A8C794B646CD87985EC891B60663"></a>-->

![](assets/AdobeAccess_4_SecureDeployment.png)