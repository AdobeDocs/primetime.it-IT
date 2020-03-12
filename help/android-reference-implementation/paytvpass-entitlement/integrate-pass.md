---
description: Personalizza l'implementazione di riferimento per integrare l'autenticazione Adobe Primetime nell'ambiente di produzione.
seo-description: Personalizza l'implementazione di riferimento per integrare l'autenticazione Adobe Primetime nell'ambiente di produzione.
seo-title: Integrare l'autenticazione Primetime
title: Integrare l'autenticazione Primetime
uuid: 34cdf1da-261e-462c-a194-4fcb439e5dfb
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Integrare l&#39;autenticazione Primetime {#integrate-primetime-authentication}

Personalizza l&#39;implementazione di riferimento per integrare l&#39;autenticazione Adobe Primetime nell&#39;ambiente di produzione.

L&#39;integrazione Implementazione di riferimento del servizio di autenticazione Primetime funziona out-of-the-box come dimostrazione. Tuttavia, per utilizzare l&#39;integrazione in un lettore pronto per la produzione, è necessario implementare le seguenti personalizzazioni:

1. Abilitare o disabilitare i flussi di adesione.

   Per poter essere abilitata, è `EntitlementManager` necessario prima inizializzare e ottenere un&#39;istanza dell&#39;SDK di autenticazione Primetime. Se `EntitlementManager` non inizializza questa libreria, il manager verrà disabilitato.
1. Attivate `EntitlementManger`, dalla classe applicazione principale:

   ```java
   // initialize the AccessEnabler library, required for Primetime PayTV Pass entitlement workflows 
   EntitlementManager.initializeAccessEnabler(this); // comment out this line to disable entitlement workflows
   ```

1. Utilizzate la `ManagerFactory` classe per ottenere un&#39;istanza del `EntitlementManager`.

   È sempre necessario utilizzare il `ManagerFactory` per ottenere un&#39;istanza del `EntitlementManager`, in quanto `ManagerFactory` mantiene una singola istanza di EntitlementManager per l&#39;applicazione. Non creare mai un&#39;istanza delle `EntitlementManager` classi o `EntitlementManagerOn` delle classi utilizzando i relativi costruttori.

   ```java
   EntitlementManager entitlementManager =  
   ManagerFactory.getEntitlementManager();
   ```

   Il `ManagerFactory` metodo restituisce un&#39;istanza di `EntitlementManagerOn`, con i flussi di adesione abilitati, se avete precedentemente chiamato `EntitlementManager.initializeAccessEnabler`. Se non effettuate la prima chiamata `EntitlementManager.initializeAccessEnabler`, il `ManagerFactory` visitatore restituirà un’istanza di `EntitlementManager`, con i flussi di adesione disattivati. 1. Configurare l&#39;ID del richiedente.

   L&#39;implementazione di riferimento viene preconfigurata con l&#39;ID del richiedente di test impostato su: &quot;REF&quot;. Potete utilizzare questo ID richiedente per testare l’applicazione. Quando sei pronto a utilizzare l&#39;ID richiedente fornito dal rappresentante di autenticazione Primetime, aggiorna il [!DNL res/values/strings.xml] file dell&#39;applicazione con il tuo ID richiedente.

   ```xml
   <!-- Programmer Requestor ID, change to ID provided by your Adobe  
        Primetime pay-TV pass representative --> 
   <string name="adobepass_requestor_id">REF</string> 
   
   <!-- Adobe Primetime pay-TV pass service provider endpoint for production 
        environment --> 
   <string name="adobepass_sp_url_production">sp.auth.adobe.com</string> 
   
   <!-- Adobe Primetime pay-TV pass service provider endpoint for staging  
        environment --> 
   <string name="adobepass_sp_url_staging">sp.auth-staging.adobe.com</string>
   ```

   Inoltre, potrebbe essere necessario modificare gli URL utilizzati dall&#39;applicazione per connettersi ai servizi di autenticazione Primetime. Questi includono gli URL del server di pre-produzione e dell&#39;autenticazione Primetime e un URL di un servizio di verifica token. Per ulteriori informazioni, contattate il rappresentante Adobe Primetime. 1. Firmate l&#39;ID del richiedente.

   Al fine di stabilire l&#39;identità del programmatore all&#39;interno del sistema di autenticazione Primetime, l&#39;ID richiedente del programmatore viene inviato al sistema di autenticazione Primetime. Come ulteriore livello di sicurezza, l&#39;ID richiedente deve essere firmato dal programmatore prima di inviarlo ad Adobe. Adobe consiglia di impostare un servizio per firmare l&#39;ID del richiedente su una rete affidabile.

   L&#39;implementazione di riferimento di Primetime dimostra come firmare l&#39;ID del richiedente, ma questo è solo a scopo dimostrativo. Adobe consiglia vivamente di non includere il certificato di firma e il codice del generatore di firme in `com.adobe.primetime.reference.crypto`un&#39;applicazione di produzione. È invece necessario spostarlo in un servizio di rete affidabile.

1. Configurare l&#39;ambiente server.

   Il servizio di autenticazione Primetime può essere eseguito in due ambienti separati:

   * Gestione temporanea - L&#39;ambiente di verifica viene utilizzato per il test dell&#39;applicazione.
   * Produzione - L&#39;ambiente di produzione viene utilizzato per le distribuzioni live dell&#39;applicazione.
   È possibile impostare gli URI sia per l&#39;ambiente di staging che per l&#39;ambiente di produzione utilizzando l&#39;applicazione, tuttavia è necessario impostare quale di questi viene utilizzato dall&#39;applicazione all&#39;interno del codice. Nella `com.adobe.primetime.reference.manager.EntitlementManger` classe, impostare la `environmentUri` variabile su `STAGING_URI` o `PRODUCTION_URI` a seconda dell&#39;ambiente del servizio di autenticazione Primetime in uso.

   >[!NOTE]
   >
   >L&#39;ID richiedente fornito (&quot;REF&quot;) deve essere utilizzato solo con l&#39;ambiente di pre-produzione.

   `com.adobe.primetime.reference.manager.EntitlementManager`:

   ```java
     // Adobe Primetime authentication service provider endpoint for production environment 
     PRODUCTION_URI = 
         application.getResources().getString(R.string.adobepass_sp_url_production); 
   
     // Adobe Primetime authentication service provider endpoint for staging environment 
     STAGING_URI = 
       application.getResources().getString(R.string.adobepass_sp_url_staging); 
   
     // Set to STAGING_URI when testing against the staging/test environment 
     // Set to PRODUCTION_URI when deploying the application for production use 
     String environmentUri = STAGING_URI; 
   
     // Adobe Primetime authentication service URI used by this application 
     PAYTV_PASS_URI = environmentUri + "/adobe-services"; 
   
     // Token Verification Service URL 
     TVS_URL = "https://" + environmentUri + "/tvs/v1/validate";
   ```

1. Personalizzate la griglia di selezione MVPD.

   Nella pagina di selezione del provider di contenuti viene visualizzata una tabella dei nove MVPD principali selezionati dall&#39;utente. L&#39;applicazione estrae i primi nove MVPD da un elenco ordinato all&#39;interno dell&#39;applicazione che corrisponde ai MVPD disponibili integrati con il programmatore nel sistema di autenticazione Primetime. L&#39;elenco ordinato dei file MVPD principali è basato sull&#39;ID MVPD all&#39;interno del sistema di autenticazione Primetime, non sul nome visualizzato MVPD. È importante verificare che gli ID MVPD nell&#39;elenco MVPD principale corrispondano agli ID MVPD integrati nell&#39;account del programmatore, in quanto in alcuni casi gli ID possono essere diversi tra le diverse integrazioni. Di seguito è riportato l&#39;elenco ordinato dei file MVPD principali che si trova nella classe `com.adobe.primetime.reference.ui.entitlement.MvpdPickerFragment`.

   ```java
   /* Array of MVPDs to display in a Grid of icons 
   When displaying a grid, only the MVPDs which intersect this array and the 
   ArrayList of all MVPDs are displayed. 
   The array contents are ordered by display preference as only a maximum of 
   MAX_DISPLAY_ICONS are displayed. 
   */ 
   private static final String[] PRIMARY_MVPDS = { 
   "Comcast_SSO",                         // Comcast XFINITY 
   "DTV",                                 // DirectTV 
   "Dish",                                // Dish 
   "TWC",                                 // Time Warner Cable 
   "Cox",                                 // Cox 
   "Charter_Direct",                      // Charter 
   "Verizon",                             // Verizon FiOS 
   "Cablevision",                         // Cablevision Optimum 
   "ATT",                                 // AT&T U-verse 
   "Brighthouse",                         // Brighthouse 
   "Suddenlink",                          // Suddenlink 
   "Mediacom",                            // Mediacom 
   "CableOne",                            // CableOne 
   "WOW",                                 // WOW! 
   "RCN",                                 // RCN 
   "auth_atlanticbb_net",                 // Atlantic Broadband 
   "auth_armstrongmywire_com",            // Armstrong 
   "knology_auth-gateway_net",            // KNOLOGY 
   "serviceelectric_auth-gateway_net",    // Service Electric Cablevision 
   "msauth_midco_net",                    // Midcontinent Communications 
   "auth_metrocast_net",                  // MetroCast 
   "www_websso_mybrctv_com",              // Blue Ridge Communications 
   };
   ```

   Nella tabella seguente è riportato un esempio di come viene utilizzato l&#39;elenco ordinato di MVPD principali. Nella prima colonna sono elencati i file MVPD integrati con il programmatore. La seconda colonna è l&#39;elenco (abbreviato) ordinato degli MVPD. La terza colonna è l&#39;elenco dei risultati utilizzato per visualizzare i primi sei MVPD all&#39;utente.

   In questo esempio vengono utilizzati i primi sei MVPD invece dei nove effettivi solo per semplificare l&#39;esempio. Tenere presente che l&#39;elenco dei risultati contiene l&#39;intersezione dei primi due elenchi e ha lo stesso ordine del secondo elenco. Notate inoltre che AT&amp;T U-verse non è nell&#39;elenco finale, in quanto vengono presi solo i primi sei MVPD corrispondenti.

| MVPD disponibili | MVPD principali | Visualizza 6 MVPD |
|--- |--- |--- |
| <ol><li>XFINITY Comcast</li><li>TWC</li><li>Mediacom</li><li>RCN</li><li>Piatto</li><li>AT&amp;T U-verse</li><li>CableOne</li><li>Faro</li><li>Banda larga atlantica</li><li>WOW!</li><li>MetroCast</li><li>DirectTV </li><li>Cox</li><li>Cablevision Optimum</li></ol> | <ol><li>XFINITY Comcast</li><li>DirectTV</li><li>Piatto</li><li> TWC</li><li>Cox</li><li>Charter</li><li>Verizon FiOS</li><li>Cablevision Optimum</li><li>AT&amp;T U-verse</li></ol> | <ol><li>XFINITY Comcast</li><li>DirectTV</li><li>Piatto</li><li>TWC</li><li>Cox</li><li>Cablevision Optimum</li></ol> |
