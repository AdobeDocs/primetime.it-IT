---
description: Per iniziare a utilizzare Primetime DRM Cloud, con tecnologia ExpressPlay, devi configurare gli account Adobe Cert ed ExpressPlay con l’aiuto del tuo rappresentante Adobe.
title: Effettua il provisioning (account, ecc.)
exl-id: 2543d997-3495-4545-9395-072c07431aba
source-git-commit: a0917e128862184ce18050792c2ee2ac265050d2
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---

# Effettua il provisioning (account, ecc.) {#get-provisioned-accounts-etc}

Per iniziare a utilizzare Primetime DRM Cloud, con tecnologia ExpressPlay, devi configurare gli account Adobe Cert ed ExpressPlay con l’aiuto del tuo rappresentante Adobe.

1. Contatta il tuo rappresentante di Adobe e richiedi gli account Adobe Cert ed ExpressPlay necessari per implementare Multi-DRM con TVSDK.

   Fornisci al rappresentante del tuo Adobe l’indirizzo e-mail che userai come punto di contatto. Adobe crea quindi due account:

   * ***Account portale certificati*** - ( https://certportal.primetime.adobe.com) : *Team di gestione registrazione certificati Adobe Access/Primetime DRM* invia un’e-mail agli indirizzi che hai fornito. L’e-mail include l’URL del portale del certificato di Adobe, insieme a un collegamento alla documentazione di registrazione del certificato di Adobe (i documenti più recenti sono disponibili qui: [Guida alla registrazione dei certificati](../../../digital-rights-management/certificate-enrollment-guide/about-certs.md)).

   * ***Account ExpressPlay*** - Adobe invia un&#39;e-mail contenente un collegamento da utilizzare per la registrazione all&#39;account amministratore ExpressPlay.

1. Accedi al portale del certificato di Adobe utilizzando il tuo Adobe ID (utilizza lo stesso indirizzo e-mail fornito al tuo rappresentante Adobe). Se non disponi ancora di un Adobe ID, puoi crearne rapidamente uno seguendo la *Ottieni un Adobe ID* collegamento dal portale certificati:

   <!--<a id="fig_mst_gtj_wv"></a>-->

   ![](assets/cert_portal_sign-in-page-web.png)

1. Nel portale del certificato di Adobe, richiedi un *Versione di prova* cert.

   Per la prova Multi-DRM, un unico certificato di prova coprirà tutti questi aspetti della protezione dei contenuti: imballaggio, licenze e trasporto. Dovrai fornire il tuo [CSR](../../../digital-rights-management/certificate-enrollment-guide/request-certs/gen-cert-signing-req.md) per richiedere un certificato:
   <!--<a id="fig_op1_xwj_wv"></a>-->

   ![](assets/cert_portal_trial_request-web.png)

   Adobe ti invierà un’e-mail che indica se la richiesta di certificato è stata accettata o rifiutata. Puoi visualizzare lo stato delle richieste di certificato in *Cronologia richieste* scheda nel portale certificati:
   <!--<a id="fig_gkl_myj_wv"></a>-->

   ![](assets/cert_portal_request_history-web.png)

1. Crea il tuo account Amministratore ExpressPlay.

   Segui il collegamento a ExpressPlay fornito nell&#39;Adobe. Verrà aperto il *Creare un account* su ExpressPlay. Compila le informazioni richieste e invia il modulo. Riceverai un’e-mail da `operations@expressplay.com` contenente un collegamento di attivazione valido per una settimana. Dopo l&#39;attivazione, configurare il servizio ExpressPlay:
   <!--<a id="fig_cjl_ztk_wv"></a>-->

   ![](assets/expressplay_create_service-web.png)

   Dopo aver creato il servizio, viene visualizzata una pagina Amministratore personalizzata. Insieme ad alcuni campi di tracciamento delle attività, visualizzerai i tuoi Produzione e Test *autenticatori cliente* (chiavi API) e gli URL del servizio di produzione e test:

   <!--<a id="fig_c5h_xdl_wv"></a>-->

   ![](assets/expressplay_admin_dashboard_2-web.png) ![](assets/expressplay_admin_dashboard-web.png)

1. Se utilizzi FairPlay, sono necessari ulteriori passaggi (sul sito per sviluppatori di Apple) per completare la configurazione con ExpressPlay. Consulta [Abilitare il servizio ExpressPlay per FairPlay](../../multi-drm-workflows/p-l-and-p/fairplay-workflow.md#enable-expressplay-service-for-fairplay) per istruzioni.
