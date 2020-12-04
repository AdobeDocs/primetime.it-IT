---
description: Per iniziare a utilizzare Primetime DRM Cloud, basato su ExpressPlay, devi configurare  account Cert e ExpressPlay del Adobe con l'aiuto del tuo rappresentante del Adobe .
seo-description: Per iniziare a utilizzare Primetime DRM Cloud, basato su ExpressPlay, devi configurare  account Cert e ExpressPlay del Adobe con l'aiuto del tuo rappresentante del Adobe .
seo-title: Get Provisioning (account, ecc.)
title: Get Provisioning (account, ecc.)
uuid: 51b95676-2121-4d8b-8756-9fd097185a13
translation-type: tm+mt
source-git-commit: 9792aff8586c46aabb5bfb70864cfe98c28e602d
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---


# Get Provisioning (account, ecc.) {#get-provisioned-accounts-etc}

Per iniziare a utilizzare Primetime DRM Cloud, basato su ExpressPlay, devi configurare  account Cert e ExpressPlay del Adobe con l&#39;aiuto del tuo rappresentante del Adobe .

1. Contattate il rappresentante del Adobe  e richiedete gli account  Adobe Cert e ExpressPlay necessari per implementare Multi-DRM con TVSDK.

       Fornite al rappresentante  Adobe l&#39;indirizzo e-mail che verrà utilizzato come punto di contatto.  Adobe crea quindi due account:
   
   * ***Account***  portale certificati - ( <span></span>https://certportal.primetime.adobe.com): Il  *Adobe Accesso /* Team di gestione delle registrazioni DRM di Primetime invia un&#39;e-mail agli indirizzi che hai fornito. L&#39;e-mail include l&#39;URL del portale di certificati di Adobe , insieme a un collegamento alla documentazione di iscrizione  certificati di Adobe (i documenti più recenti sono disponibili qui: [Guida all&#39;iscrizione ai certificati](../../../digital-rights-management/certificate-enrollment-guide/about-certs.md)).

   * ***ExpressPlay Account*** -  Adobe invia un&#39;e-mail contenente un collegamento che consente di registrarsi per l&#39;account ExpressPlay Admin.

1. Effettuate l&#39;accesso al portale del certificato del Adobe  utilizzando l&#39;Adobe ID  (utilizzate lo stesso indirizzo e-mail fornito al Adobe rappresentante del ). Se non disponete ancora di un Adobe ID , potete crearne rapidamente uno seguendo il collegamento *Ottieni un Adobe ID* dal portale del certificato:

   <!--<a id="fig_mst_gtj_wv"></a>-->

   ![](assets/cert_portal_sign-in-page-web.png)

1. Sul portale del certificato del Adobe , richiedete un certificato *di prova*.

   Per la versione di prova Multi-DRM, un singolo certificato di prova coprirà tutti gli aspetti seguenti della protezione dei contenuti: imballaggio, licenze e trasporto. Per richiedere un certificato è necessario fornire il proprio [CSR](../../../digital-rights-management/certificate-enrollment-guide/request-certs/gen-cert-signing-req.md):
   <!--<a id="fig_op1_xwj_wv"></a>-->

   ![](assets/cert_portal_trial_request-web.png)

    Adobe vi invierà un&#39;e-mail che indica l&#39;accettazione o il rifiuto della vostra richiesta di certificato. Potete visualizzare lo stato delle richieste di certificati nella scheda *Cronologia richieste* del portale certificati:
   <!--<a id="fig_gkl_myj_wv"></a>-->

   ![](assets/cert_portal_request_history-web.png)

1. Crea il tuo account ExpressPlay Admin.

   Seguite il collegamento a ExpressPlay fornito  Adobe. Viene aperta la pagina *Create an Account* in ExpressPlay. Compila le informazioni richieste e invia il modulo. Riceverai un&#39;e-mail da `operations@expressplay.com` contenente un collegamento di attivazione valido per una settimana. Dopo l&#39;attivazione, configura il servizio ExpressPlay:
   <!--<a id="fig_cjl_ztk_wv"></a>-->

   ![](assets/expressplay_create_service-web.png)

   Dopo aver creato il servizio, ti verrà presentata la tua pagina Admin. Insieme ad alcuni campi di tracciamento dell&#39;attività, vedrete gli *autenticatori cliente di produzione e test* (chiavi API) e gli URL del servizio di produzione e test:

   <!--<a id="fig_c5h_xdl_wv"></a>-->

   ![](assets/expressplay_admin_dashboard_2-web.png) ![](assets/expressplay_admin_dashboard-web.png)

1. Se utilizzate FairPlay, sono necessari ulteriori passaggi (sul sito sviluppatori Apple) per ottenere la configurazione con ExpressPlay. Per istruzioni, vedere [Abilita servizio ExpressPlay per FairPlay](../../multi-drm-workflows/p-l-and-p/fairplay-workflow.md#enable-expressplay-service-for-fairplay).
