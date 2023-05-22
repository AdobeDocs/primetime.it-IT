---
description: Personalizza l’implementazione di riferimento per integrare l’autenticazione Adobe Primetime per l’ambiente di produzione.
title: Integrare l’autenticazione Primetime
exl-id: ef6dc75d-d00f-481f-a620-4ec402cbebb6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 0%

---

# Integrare l’autenticazione Primetime {#integrate-primetime-authentication}

Personalizza l’implementazione di riferimento per integrare l’autenticazione Adobe Primetime per l’ambiente di produzione.

L’integrazione dell’implementazione di riferimento del servizio di autenticazione Primetime funziona come dimostrazione preconfigurata. Tuttavia, per utilizzare l’integrazione in un lettore pronto per la produzione, è necessario implementare le seguenti personalizzazioni:

1. Attiva o disattiva i flussi di adesione.

   Il `EntitlementManager` deve prima inizializzare e ottenere un’istanza dell’SDK di autenticazione Primetime da abilitare. Se il `EntitlementManager` non inizializza questa libreria, il gestore verrà disabilitato.
1. Abilita `EntitlementManger`, dalla classe dell&#39;applicazione principale:

   ```java
   // initialize the AccessEnabler library, required for Primetime PayTV Pass entitlement workflows 
   EntitlementManager.initializeAccessEnabler(this); // comment out this line to disable entitlement workflows
   ```

1. Utilizza il `ManagerFactory` classe per ottenere un&#39;istanza di `EntitlementManager`.

   È sempre necessario utilizzare `ManagerFactory` per ottenere un&#39;istanza di `EntitlementManager`, come `ManagerFactory` mantiene una singola istanza di EntitlementManager per l&#39;applicazione. Non creare mai un&#39;istanza di `EntitlementManager` o `EntitlementManagerOn` classi mediante i relativi costruttori.

   ```java
   EntitlementManager entitlementManager =  
   ManagerFactory.getEntitlementManager();
   ```

   Il `ManagerFactory` restituisce un&#39;istanza di `EntitlementManagerOn`, con i flussi di adesione abilitati, se in precedenza hai chiamato `EntitlementManager.initializeAccessEnabler`. Se non chiami prima `EntitlementManager.initializeAccessEnabler`, quindi `ManagerFactory` restituirà un’istanza di `EntitlementManager`, con i flussi dei diritti disabilitati. 1. Configura l’ID richiedente.

   L’implementazione di riferimento è preconfigurata con l’ID richiedente del test impostato su: &quot;REF&quot;. Puoi usare questo ID richiedente per testare l’applicazione. Quando sei pronto a utilizzare l’ID richiedente fornito dal rappresentante di autenticazione di Primetime, aggiorna i [!DNL res/values/strings.xml] file con il tuo ID richiedente.

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

   Inoltre, potrebbe essere necessario modificare gli URL utilizzati dall’applicazione per connettersi ai servizi di autenticazione di Primetime. Questi includono gli URL del server di staging e produzione per l’autenticazione Primetime e l’URL di un servizio di verifica dei token. Per ulteriori informazioni, rivolgiti al tuo rappresentante Adobe Primetime. 1. Firma l’ID richiedente.

   Al fine di stabilire l&#39;identità del programmatore all&#39;interno del sistema di autenticazione Primetime, l&#39;ID del richiedente del programmatore viene inviato al sistema di autenticazione Primetime. Come ulteriore livello di sicurezza, l’ID richiedente deve essere firmato dal programmatore prima di essere inviato all’Adobe. L’Adobe consiglia al programmatore di impostare un servizio per firmare l’ID richiedente su una rete attendibile.

   L’implementazione di riferimento di Primetime illustra come firmare l’ID richiedente, ma questo serve solo a scopo dimostrativo. L’Adobe consiglia vivamente che il certificato di firma e il codice del generatore di firme, in `com.adobe.primetime.reference.crypto`, non devono essere inclusi in un&#39;applicazione di produzione. È invece consigliabile spostarlo in un servizio di rete attendibile.

1. Configurare l’ambiente server.

   Il servizio di autenticazione Primetime può essere eseguito in due ambienti separati:

   * Staging: l’ambiente di staging viene utilizzato per testare l’applicazione.
   * Produzione: l’ambiente di produzione viene utilizzato per le implementazioni live dell’applicazione.

   È possibile impostare gli URI sia per gli ambienti di staging che per quelli di produzione utilizzando l’applicazione, ma è necessario impostare quali di questi vengono utilizzati dall’applicazione all’interno del codice. In `com.adobe.primetime.reference.manager.EntitlementManger` classe, imposta `environmentUri` variabile a uno dei due `STAGING_URI` o `PRODUCTION_URI` a seconda dell’ambiente del servizio di autenticazione Primetime in uso.

   >[!NOTE]
   >
   >L’ID richiedente (&quot;REF&quot;) fornito deve essere utilizzato solo con l’ambiente di staging.

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

1. Personalizzare la griglia di selezione MVPD.

   Nella pagina di selezione del provider di contenuti viene visualizzata una tabella dei primi nove MVPD selezionabili dall’utente. L&#39;applicazione richiama i primi nove MVPD da un elenco ordinato all&#39;interno dell&#39;applicazione che corrispondono agli MVPD disponibili integrati con il Programmatore nel sistema di autenticazione Primetime. L&#39;elenco ordinato degli MVPD primari è basato sull&#39;ID MVPD all&#39;interno del sistema di autenticazione Primetime, non sul nome visualizzato MVPD. È importante verificare che gli ID MVPD nell&#39;elenco degli MVPD primari corrispondano agli ID MVPD integrati con l&#39;account del programmatore, in quanto in alcuni casi gli ID possono essere diversi tra le integrazioni. Di seguito è riportato l’elenco ordinato di MVPD primari presenti nella classe `com.adobe.primetime.reference.ui.entitlement.MvpdPickerFragment`.

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

   La tabella seguente fornisce un esempio di come viene utilizzato l’elenco ordinato di MVPD primari. La prima colonna elenca gli MVPD integrati con il Programmatore. La seconda colonna è l&#39;elenco ordinato (abbreviato) degli MVPD. La terza colonna è l’elenco dei risultati utilizzato per visualizzare i primi sei MVPD per l’utente.

   Questo esempio utilizza i primi sei MVPD invece dei nove effettivi solo per mantenere l’esempio semplice. L&#39;elenco dei risultati contiene l&#39;intersezione dei primi due elenchi e ha lo stesso ordine del secondo elenco. Inoltre, si noti che AT&amp;T U-verse non è nella lista finale, in quanto vengono presi solo i primi sei MVPD corrispondenti.

| MVPD disponibili | MVPD primari | Visualizzati 6 MVPD |
|--- |--- |--- |
| <ol><li>XFINITY compresso</li><li>TWC</li><li>Mediacom</li><li>RCN</li><li>Piatto</li><li>A&amp;T U-verso</li><li>CableOne</li><li>Brighthouse</li><li>Banda larga atlantica</li><li>WOW!</li><li>MetroCast</li><li>DirectTV </li><li>Cox</li><li>Ottimo Cablevision</li></ol> | <ol><li>XFINITY compresso</li><li>DirectTV</li><li>Piatto</li><li> TWC</li><li>Cox</li><li>Carta</li><li>Verizon FiOS</li><li>Ottimo Cablevision</li><li>A&amp;T U-verso</li></ol> | <ol><li>XFINITY compresso</li><li>DirectTV</li><li>Piatto</li><li>TWC</li><li>Cox</li><li>Ottimo Cablevision</li></ol> |
