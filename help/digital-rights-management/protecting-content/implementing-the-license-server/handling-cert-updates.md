---
seo-title: Gestione degli aggiornamenti dei certificati alla scadenza  certificati rilasciati dal Adobe
title: Gestione degli aggiornamenti dei certificati alla scadenza  certificati rilasciati dal Adobe
uuid: abc0ca3e-a78f-4078-9480-7116843cce05
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---


# Gestione degli aggiornamenti dei certificati quando  certificati rilasciati dal Adobe scadono{#handling-certificate-updates-when-adobe-issued-certificates-expire}

Potrebbe essere necessario ottenere un nuovo certificato da  Adobe. Ad esempio, un certificato di produzione scade alla scadenza di un certificato di valutazione o al passaggio da una valutazione a un certificato di produzione. Ogni volta che un certificato scade e che non si desidera creare un nuovo pacchetto per il contenuto che utilizza il vecchio certificato, è possibile rendere il server licenze consapevole sia del vecchio che del nuovo certificato.

Per aggiornare un server con nuovi certificati:

1. (Facoltativo) Quando si aggiungono nuove voci a un elenco di aggiornamenti dei criteri DRM esistente o a un elenco di revoche, è necessario firmare con le nuove credenziali e utilizzare il vecchio certificato per convalidare la firma sul file esistente.

   Ad esempio, è possibile utilizzare la riga di comando seguente per aggiungere una voce a un elenco di aggiornamento criteri DRM esistente, firmato utilizzando una credenziale diversa:

   ```
   java -jar AdobePolicyUpdateListManager.jar newList -f oldList oldSigningCert.cer -u pol 0 "" ""
   ```

1. (Facoltativo) Utilizzate l&#39;API Java per aggiornare il server licenze con il nuovo elenco di aggiornamento o di revoca dei criteri DRM:

   ```
   HandlerConfiguration.setRevocationList() 
   ```

   oppure:

   ```
   HandlerConfiguration.setPolicyUpdateList()
   ```

   Nell&#39;implementazione del riferimento, le proprietà utilizzate sono `HandlerConfiguration.RevocationList` e `HandlerConfiguration.PolicyUpdateList`. È inoltre necessario aggiornare il certificato utilizzato per verificare le firme: `RevocationList.verifySignature.X509Certificate`.

1. Aggiornate il server licenze con i certificati nuovi e vecchi.

   Se si desidera utilizzare il contenuto che è stato creato utilizzando i vecchi certificati, assicurarsi che il server licenze abbia accesso alle credenziali del server licenze vecchie e nuove, nonché alle credenziali di trasporto.

   Per le credenziali del server licenze:

   * Assicurarsi che la credenziale corrente sia passata al costruttore `LicenseHandler`:

      * Nell&#39;implementazione del riferimento, impostatela con la proprietà `LicenseHandler.ServerCredential`.
      * Nel server  Adobe Primetime DRM per lo streaming protetto, la credenziale corrente deve essere la prima credenziale specificata nell&#39;elemento `LicenseServerCredential` nel file flashaccess-tenant.xml.
   * Assicurarsi che le credenziali correnti e vecchie siano fornite a `AsymmetricKeyRetrieval`

      * Nell&#39;implementazione di riferimento, impostatela con le proprietà `LicenseHandler.ServerCredential` e `AsymmetricKeyRetrieval.ServerCredential. n`.

      * Nel server DRM di Primetime per lo streaming protetto, le vecchie credenziali vengono specificate dopo la prima credenziale nell&#39;elemento `LicenseServerCredential` nel file flashaccess-tenant.xml.

   Per le credenziali di trasporto:

   * Assicurarsi che la credenziale corrente sia passata al metodo `HandlerConfiguration.setServerTransportCredential()`:

      * Nell&#39;implementazione del riferimento, impostatela con la proprietà `HandlerConfiguration.ServerTransportCredential`.
      * Nel server DRM di Primetime per lo streaming protetto, la credenziale corrente deve essere la prima specificata nell&#39;elemento `TransportCredential` nel file [!DNL flashaccess-tenant.xml].
   * Assicurarsi che le vecchie credenziali siano fornite a `HandlerConfiguration.setAdditionalServerTransportCredentials`():

      * Nell&#39;implementazione di riferimento, impostatela con le proprietà `HandlerConfiguration.AdditionalServerTransportCredential. n`.
      * Nel server DRM di Primetime per lo streaming protetto, questo viene specificato dopo la prima credenziale nell&#39;elemento `TransportCredential` nel file flashaccess-tenant.xml.




1. Aggiornate gli strumenti di package per essere sicuri che stiano creando pacchetti di contenuto con le credenziali correnti. Verificate che per la creazione del pacchetto siano utilizzati il certificato del server licenze, il certificato di trasporto e le credenziali del packager più recenti.
1. Aggiornare il certificato del server licenze del server chiavi nel modo seguente:

   * Aggiornare le credenziali nel  file di configurazione del tenant del server di chiavi Adobe Primetime DRM includendo sia le credenziali vecchie che nuove del server di chiavi in flashaccess-keyserver-tenant.xml.
   * Assicurarsi che il certificato corrente sia passato al metodo `HandlerConfiguration.setKeyServerCertificate()`.

      * Nell&#39;implementazione del riferimento, impostatela con la proprietà `HandlerConfiguration.KeyServerCertificate`.
      * Nel server DRM di Primetime per lo streaming protetto, specifica il certificato del server chiavi nell&#39;elemento tramite l&#39;elemento Configuration/Tenant/Certificates/KeyServer.

