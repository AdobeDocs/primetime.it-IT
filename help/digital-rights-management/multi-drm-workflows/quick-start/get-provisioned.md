---
description: Per iniziare a utilizzare Primetime DRM Cloud con tecnologia ExpressPlay, devi configurare gli account Adobe Cert ed ExpressPlay con l’aiuto del tuo rappresentante Adobe.
title: Ottieni provisioning (account, ecc.)
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---


# Ottieni il provisioning (account, ecc.) {#get-provisioned-accounts-etc}

Per iniziare a utilizzare Primetime DRM Cloud con tecnologia ExpressPlay, devi configurare gli account Adobe Cert ed ExpressPlay con l’aiuto del tuo rappresentante Adobe.

1. Contatta il tuo rappresentante di Adobe e richiedi gli account Adobe Cert e ExpressPlay necessari per implementare Multi-DRM con TVSDK.

       Fornisci al tuo rappresentante di Adobe l&#39;indirizzo e-mail che userai come punto di contatto. Ad Adobe, vengono creati due account:
   
   * ***Account***  del portale certificati - ( <span></span>https://certportal.primetime.adobe.com) : I  *team di gestione delle registrazioni dei certificati DRM di Adobe Access / Primetime* inviano un’e-mail agli indirizzi che hai fornito. L’e-mail include l’URL del portale di creazione Adobe, insieme a un collegamento alla documentazione di registrazione dei certificati di Adobe (gli ultimi documenti sono disponibili qui: [Guida alla registrazione dei certificati](../../../digital-rights-management/certificate-enrollment-guide/about-certs.md)).

   * ***Account ExpressPlay*** : l’Adobe ti invia un’e-mail contenente un collegamento utilizzato per la registrazione al tuo account amministratore ExpressPlay.

1. Accedi al portale di creazione Adobe utilizzando il tuo Adobe ID (usa lo stesso indirizzo e-mail fornito al tuo rappresentante di Adobe). Se non hai ancora un Adobe ID, puoi crearne rapidamente uno seguendo il collegamento *Ottieni un Adobe ID* dal portale del cert:

   <!--<a id="fig_mst_gtj_wv"></a>-->

   ![](assets/cert_portal_sign-in-page-web.png)

1. Sul portale del certificato di Adobe, richiedi un certificato *Trial*.

   Per la versione di prova Multi-DRM, un singolo certificato di prova includerà tutti questi aspetti della protezione dei contenuti: imballaggio, licenze e trasporto. Per richiedere un certificato dovrai fornire la tua [CSR](../../../digital-rights-management/certificate-enrollment-guide/request-certs/gen-cert-signing-req.md):
   <!--<a id="fig_op1_xwj_wv"></a>-->

   ![](assets/cert_portal_trial_request-web.png)

   L’Adobe ti invierà un’e-mail che indica l’accettazione o il rifiuto della tua richiesta di certificato. Lo stato delle richieste di certificati è visibile nella scheda *Cronologia richieste* del portale del certificato:
   <!--<a id="fig_gkl_myj_wv"></a>-->

   ![](assets/cert_portal_request_history-web.png)

1. Crea il tuo account amministratore ExpressPlay.

   Segui il collegamento a ExpressPlay fornito dall’Adobe. Viene visualizzata la pagina *Crea un account* in ExpressPlay. Compila le informazioni richieste e invia il modulo. Riceverai un’e-mail da `operations@expressplay.com` contenente un collegamento di attivazione valido per una settimana. Dopo l&#39;attivazione, configura il servizio ExpressPlay:
   <!--<a id="fig_cjl_ztk_wv"></a>-->

   ![](assets/expressplay_create_service-web.png)

   Dopo aver creato il servizio, riceverai la tua pagina di amministrazione. Insieme ad alcuni campi di tracciamento delle attività, vedrai i tuoi *autenticatori cliente di produzione e test* (chiavi API) e gli URL del servizio di produzione e test:

   <!--<a id="fig_c5h_xdl_wv"></a>-->

   ![](assets/expressplay_admin_dashboard_2-web.png) ![](assets/expressplay_admin_dashboard-web.png)

1. Se utilizzi FairPlay, sono necessari ulteriori passaggi (sul sito per sviluppatori Apple) per la configurazione con ExpressPlay. Per istruzioni, consulta [Abilita servizio ExpressPlay per FairPlay](../../multi-drm-workflows/p-l-and-p/fairplay-workflow.md#enable-expressplay-service-for-fairplay) .
