---
description: Personalizza l’implementazione di riferimento per integrare l’autenticazione Adobe Primetime per l’ambiente di produzione.
title: Integrare l’autenticazione Primetime
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 0%

---


# Integrare l&#39;autenticazione Primetime {#integrate-primetime-authentication}

Personalizza l’implementazione di riferimento per integrare l’autenticazione Adobe Primetime per l’ambiente di produzione.

L’integrazione Implementazione di riferimento del servizio di autenticazione Primetime funziona come una dimostrazione predefinita. Tuttavia, per utilizzare l’integrazione in un lettore pronto per la produzione, è necessario implementare le seguenti personalizzazioni:

1. Attiva o disattiva i flussi di adesione.

   Per prima cosa è necessario inizializzare `EntitlementManager` e ottenere un&#39;istanza dell&#39;SDK di autenticazione Primetime. Se la `EntitlementManager` non inizializza questa libreria, la gestione verrà disabilitata.
1. Abilita `EntitlementManger` dalla classe dell&#39;applicazione principale:

   ```java
   // initialize the AccessEnabler library, required for Primetime PayTV Pass entitlement workflows 
   EntitlementManager.initializeAccessEnabler(this); // comment out this line to disable entitlement workflows
   ```

1. Utilizza la classe `ManagerFactory` per ottenere un&#39;istanza del `EntitlementManager`.

   È sempre necessario utilizzare il `ManagerFactory` per ottenere un&#39;istanza del `EntitlementManager`, in quanto il `ManagerFactory` mantiene una singola istanza di EntitlementManager per l&#39;applicazione. Non creare mai un&#39;istanza delle classi `EntitlementManager` o `EntitlementManagerOn` utilizzando i relativi costruttori.

   ```java
   EntitlementManager entitlementManager =  
   ManagerFactory.getEntitlementManager();
   ```

   Il `ManagerFactory` restituisce un&#39;istanza di `EntitlementManagerOn`, con i flussi di adesione abilitati, se hai precedentemente chiamato `EntitlementManager.initializeAccessEnabler`. Se non chiami prima `EntitlementManager.initializeAccessEnabler`, il `ManagerFactory` restituirà un&#39;istanza di `EntitlementManager`, con i flussi di adesione disattivati. 1. Configura l&#39;ID del richiedente.

   L’implementazione di riferimento è preconfigurata con l’ID del richiedente del test impostato su: &quot;REF&quot;. Puoi utilizzare questo ID richiedente per testare l’applicazione. Quando sei pronto a utilizzare l’ID richiedente fornito dal tuo rappresentante di autenticazione Primetime, aggiorna il file [!DNL res/values/strings.xml] dell’applicazione con il tuo ID richiedente.

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

   Inoltre, potrebbe essere necessario modificare gli URL utilizzati dall&#39;applicazione per connettersi ai servizi di autenticazione di Primetime. tra cui gli URL del server di staging e produzione di Primetime Authentication e un URL per un servizio di verifica dei token. Per ulteriori informazioni, rivolgiti al tuo rappresentante Adobe Primetime. 1. Firma l&#39;ID richiedente.

   Per stabilire l&#39;identità del programmatore all&#39;interno del sistema di autenticazione Primetime, l&#39;ID del richiedente del programmatore viene inviato al sistema di autenticazione Primetime. Come ulteriore livello di sicurezza, il Requestor ID deve essere firmato dal programmatore prima di inviarlo all&#39;Adobe. L&#39;Adobe consiglia al programmatore di impostare un servizio per firmare l&#39;ID del richiedente su una rete attendibile.

   L’implementazione di riferimento di Primetime dimostra come firmare l’ID del richiedente, tuttavia questo è solo a scopo dimostrativo. L’Adobe consiglia vivamente di non includere il certificato di firma e il codice del generatore di firme sotto `com.adobe.primetime.reference.crypto` all’interno di un’applicazione di produzione. Invece, devi spostarlo in un servizio di rete affidabile.

1. Configura l&#39;ambiente server.

   Il servizio di autenticazione Primetime può essere eseguito in due ambienti separati:

   * Staging : l&#39;ambiente di staging viene utilizzato per testare l&#39;applicazione.
   * Produzione: l’ambiente di produzione viene utilizzato per le implementazioni live dell’applicazione.

   È possibile impostare gli URI sia per gli ambienti di staging che per quelli di produzione utilizzando l’applicazione. Tuttavia, è necessario impostare quali di questi vengono utilizzati dall’applicazione all’interno del codice. Nella classe `com.adobe.primetime.reference.manager.EntitlementManger` , imposta la variabile `environmentUri` su `STAGING_URI` o `PRODUCTION_URI` a seconda dell’ambiente del servizio di autenticazione Primetime in uso.

   >[!NOTE]
   >
   >L&#39;ID richiedente fornito (&quot;REF&quot;) deve essere utilizzato solo con l&#39;ambiente di staging.

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

1. Personalizza la griglia di selezione MVPD.

   Nella pagina di selezione del provider di contenuti viene visualizzata una tabella dei primi nove MVPD selezionati dall’utente. L&#39;applicazione estrae i primi nove MVPD da un elenco ordinato all&#39;interno dell&#39;applicazione che corrispondono agli MVPD disponibili integrati con il programmatore nel sistema di autenticazione Primetime. L&#39;elenco ordinato degli MVPD principali è basato sull&#39;ID MVPD all&#39;interno del sistema di autenticazione Primetime, non sul nome visualizzato MVPD. È importante verificare che gli ID MVPD nell’elenco degli MVPD principali corrispondano agli ID MVPD integrati con l’account del programmatore, in quanto in alcuni casi gli ID possono essere diversi tra le integrazioni. Di seguito è riportato l&#39;elenco ordinato degli MVPD principali che si trova nella classe `com.adobe.primetime.reference.ui.entitlement.MvpdPickerFragment`.

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

   Nella tabella seguente è riportato un esempio di utilizzo dell’elenco ordinato degli MVPD principali. La prima colonna elenca gli MVPD integrati con il programmatore. La seconda colonna è l&#39;elenco (abbreviato) ordinato degli MVPD. La terza colonna è l’elenco dei risultati utilizzati per visualizzare i primi sei MVPD per l’utente.

   Questo esempio utilizza i primi sei MVPD invece dei nove effettivi solo per mantenere l&#39;esempio semplice. Tenere presente che l’elenco dei risultati contiene l’intersezione dei primi due elenchi e ha lo stesso ordine del secondo elenco. Inoltre, notare che AT&amp;T U-verse non è nella lista finale, in quanto vengono presi solo i primi sei MVPD corrispondenti.

| MVPD disponibili | MVPD principali | Visualizzati 6 MVPD |
|--- |--- |--- |
| <ol><li>XFINITÀ COMcast</li><li>TWC</li><li>Mediacom</li><li>RCN</li><li>Piatto</li><li>AT&amp;T verso U</li><li>CableOne</li><li>Faro</li><li>Broadband atlantica</li><li>WOW!</li><li>MetroCast</li><li>DirectTV </li><li>Cox</li><li>Ottimizzazione della visione</li></ol> | <ol><li>XFINITÀ COMcast</li><li>DirectTV</li><li>Piatto</li><li> TWC</li><li>Cox</li><li>Carta</li><li>Verizon FiOS</li><li>Ottimizzazione della visione</li><li>AT&amp;T verso U</li></ol> | <ol><li>XFINITÀ COMcast</li><li>DirectTV</li><li>Piatto</li><li>TWC</li><li>Cox</li><li>Ottimizzazione della visione</li></ol> |
