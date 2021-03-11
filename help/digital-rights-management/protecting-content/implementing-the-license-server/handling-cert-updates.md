---
title: Gestione degli aggiornamenti dei certificati alla scadenza dei certificati rilasciati da Adobi
description: Gestione degli aggiornamenti dei certificati alla scadenza dei certificati rilasciati da Adobi
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---


# Gestione degli aggiornamenti dei certificati alla scadenza dei certificati rilasciati da Adobi{#handling-certificate-updates-when-adobe-issued-certificates-expire}

Potrebbe essere necessario ottenere un nuovo certificato dall’Adobe. Ad esempio, un certificato di produzione scade alla scadenza di un certificato di valutazione o al passaggio da una valutazione a un certificato di produzione. Ogni volta che un certificato scade e non si desidera creare un nuovo pacchetto per il contenuto che utilizza il certificato precedente, è possibile rendere il server licenze consapevole sia dei certificati vecchi che dei nuovi.

Per aggiornare un server con nuovi certificati:

1. (Facoltativo) Quando si aggiungono nuove voci a un elenco di aggiornamento o di revoca dei criteri DRM esistente, è necessario firmare con le nuove credenziali e utilizzare il vecchio certificato per convalidare la firma sul file esistente.

   Ad esempio, è possibile utilizzare la riga di comando seguente per aggiungere una voce a un elenco di aggiornamento dei criteri DRM esistente, firmato utilizzando una credenziale diversa:

   ```
   java -jar AdobePolicyUpdateListManager.jar newList -f oldList oldSigningCert.cer -u pol 0 "" ""
   ```

1. (Facoltativo) Utilizza l&#39;API Java per aggiornare il server licenze con il nuovo elenco di aggiornamenti dei criteri DRM o l&#39;elenco di revoche:

   ```
   HandlerConfiguration.setRevocationList() 
   ```

   o:

   ```
   HandlerConfiguration.setPolicyUpdateList()
   ```

   Nell’implementazione di riferimento, le proprietà utilizzate sono `HandlerConfiguration.RevocationList` e `HandlerConfiguration.PolicyUpdateList`. È inoltre necessario aggiornare il certificato utilizzato per verificare le firme: `RevocationList.verifySignature.X509Certificate`.

1. Aggiorna il server licenze con i certificati nuovi e vecchi.

   Se si desidera utilizzare il contenuto compilato utilizzando i certificati precedenti, assicurarsi che il server licenze abbia accesso alle credenziali del server licenze vecchie e nuove, nonché alle credenziali di trasporto.

   Per le credenziali del server licenze:

   * Assicurati che la credenziale corrente sia passata al costruttore `LicenseHandler` :

      * Nell&#39;implementazione di riferimento, impostala con la proprietà `LicenseHandler.ServerCredential` .
      * Nel server DRM di Adobe Primetime per lo streaming protetto, la credenziale corrente deve essere la prima credenziale specificata nell&#39;elemento `LicenseServerCredential` nel file flashaccess-tenant.xml .
   * Assicurati che le credenziali attuali e precedenti siano fornite a `AsymmetricKeyRetrieval`

      * Nell’implementazione di riferimento, impostala con le proprietà `LicenseHandler.ServerCredential` e `AsymmetricKeyRetrieval.ServerCredential. n` .

      * Nel server DRM di Primetime per lo streaming protetto, le vecchie credenziali vengono specificate dopo la prima credenziale nell&#39;elemento `LicenseServerCredential` nel file flashaccess-tenant.xml .

   Per le credenziali di trasporto:

   * Assicurati che la credenziale corrente sia passata al metodo `HandlerConfiguration.setServerTransportCredential()` :

      * Nell&#39;implementazione di riferimento, impostala con la proprietà `HandlerConfiguration.ServerTransportCredential` .
      * Nel server DRM di Primetime per lo streaming protetto, la credenziale corrente deve essere la prima credenziale specificata nell&#39;elemento `TransportCredential` nel file [!DNL flashaccess-tenant.xml].
   * Assicurati che le vecchie credenziali siano fornite a `HandlerConfiguration.setAdditionalServerTransportCredentials`():

      * Nell’implementazione di riferimento, impostala con le proprietà `HandlerConfiguration.AdditionalServerTransportCredential. n` .
      * Nel server DRM di Primetime per lo streaming protetto, questo viene specificato dopo la prima credenziale nell&#39;elemento `TransportCredential` nel file flashaccess-tenant.xml .




1. Aggiorna gli strumenti di imballaggio per assicurarti che stiano creando il pacchetto del contenuto con le credenziali correnti. Assicurati che per il packaging siano utilizzati il certificato del server licenze, il certificato di trasporto e le credenziali del packager più recenti.
1. Aggiorna il certificato del server licenze del server chiavi come segue:

   * Aggiorna le credenziali nel file di configurazione del tenant del server chiave DRM di Adobe Primetime includendo sia le credenziali vecchie che nuove del server chiavi in flashaccess-keyserver-tenant.xml.
   * Verifica che il certificato corrente sia passato al metodo `HandlerConfiguration.setKeyServerCertificate()` .

      * Nell&#39;implementazione di riferimento, impostala con la proprietà `HandlerConfiguration.KeyServerCertificate` .
      * Nel server DRM di Primetime per lo streaming protetto, specifica il certificato del server chiavi in attraverso l&#39;elemento Configuration/Tenant/Certificates/KeyServer .

