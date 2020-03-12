---
description: Per iniziare a utilizzare Primetime DRM Cloud, basato su ExpressPlay, devi configurare account Adobe Cert ed ExpressPlay con l'aiuto del tuo rappresentante Adobe.
seo-description: Per iniziare a utilizzare Primetime DRM Cloud, basato su ExpressPlay, devi configurare account Adobe Cert ed ExpressPlay con l'aiuto del tuo rappresentante Adobe.
seo-title: Get Provisioning (account, ecc.)
title: Get Provisioning (account, ecc.)
uuid: 51b95676-2121-4d8b-8756-9fd097185a13
translation-type: tm+mt
source-git-commit: 9792aff8586c46aabb5bfb70864cfe98c28e602d

---


# Get Provisioning (account, ecc.) {#get-provisioned-accounts-etc}

Per iniziare a utilizzare Primetime DRM Cloud, basato su ExpressPlay, devi configurare account Adobe Cert ed ExpressPlay con l&#39;aiuto del tuo rappresentante Adobe.

1. Contattate il rappresentante Adobe e richiedete gli account Adobe Cert e ExpressPlay necessari per implementare Multi-DRM con TVSDK.

       Fornite al vostro rappresentante Adobe l&#39;indirizzo e-mail che utilizzerete come punto di contatto. Adobe crea quindi due account:
   
   * ***Account*** portale certificati - (<span></span>https://certportal.primetime.adobe.com): Il team *di gestione delle registrazioni dei certificati DRM di* Adobe Access/Primetime invia un messaggio e-mail agli indirizzi forniti. L&#39;e-mail include l&#39;URL del portale Adobe Cert, insieme a un collegamento alla documentazione di iscrizione ai certificati di Adobe (i documenti più recenti sono disponibili qui: Guida [all&#39;iscrizione ai](../../../digital-rights-management/certificate-enrollment-guide/about-certs.md)certificati).

   * ***ExpressPlay Account*** - Adobe invia un messaggio e-mail contenente un collegamento che consente di registrarsi per l&#39;account ExpressPlay Admin.

1. Effettuate l&#39;accesso al portale Adobe Cert utilizzando il vostro Adobe ID (utilizzate lo stesso indirizzo e-mail che avete fornito al vostro rappresentante Adobe). Se non disponete ancora di un Adobe ID, potete crearne uno rapidamente seguendo il collegamento *Ottieni un Adobe ID* dal portale del certificato:

   <!--<a id="fig_mst_gtj_wv"></a>-->

   ![](assets/cert_portal_sign-in-page-web.png)

1. Nel portale Adobe Cert, richiedi un certificato di *prova* .

   Per la versione di prova Multi-DRM, un singolo certificato di prova coprirà tutti gli aspetti seguenti della protezione dei contenuti: imballaggio, licenze e trasporto. È necessario fornire il proprio [CSR](../../../digital-rights-management/certificate-enrollment-guide/request-certs/gen-cert-signing-req.md) per richiedere un certificato:
   <!--<a id="fig_op1_xwj_wv"></a>-->

   ![](assets/cert_portal_trial_request-web.png)

   Adobe invierà un messaggio e-mail che indica l’accettazione o il rifiuto della richiesta del certificato. Potete visualizzare lo stato delle richieste di certificati nella scheda Cronologia ** richieste nel portale certificati:
   <!--<a id="fig_gkl_myj_wv"></a>-->

   ![](assets/cert_portal_request_history-web.png)

1. Crea il tuo account ExpressPlay Admin.

   Seguite il collegamento a ExpressPlay fornito da Adobe. Viene aperta la pagina *Crea un account* in ExpressPlay. Compila le informazioni richieste e invia il modulo. Riceverete un messaggio e-mail da `operations@expressplay.com` contenente un collegamento di attivazione valido per una settimana. Dopo l&#39;attivazione, configura il servizio ExpressPlay:
   <!--<a id="fig_cjl_ztk_wv"></a>-->

   ![](assets/expressplay_create_service-web.png)

   Dopo aver creato il servizio, ti verrà presentata la tua pagina Admin. Insieme ad alcuni campi di tracciamento dell&#39;attività, vedrete gli autenticatori *dei* clienti Produzione e Test (chiavi API) e gli URL dei servizi Produzione e Test:

   <!--<a id="fig_c5h_xdl_wv"></a>-->

   ![](assets/expressplay_admin_dashboard_2-web.png) ![](assets/expressplay_admin_dashboard-web.png)

1. Se utilizzate FairPlay, sono necessari ulteriori passaggi (sul sito sviluppatori Apple) per ottenere la configurazione con ExpressPlay. Per istruzioni, consultate [Abilitare il servizio ExpressPlay per FairPlay](../../multi-drm-workflows/p-l-and-p/fairplay-workflow.md#enable-expressplay-service-for-fairplay) .
