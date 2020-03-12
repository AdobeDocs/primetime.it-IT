---
seo-title: Gestione degli aggiornamenti dei certificati alla scadenza dei certificati rilasciati da Adobe
title: Gestione degli aggiornamenti dei certificati alla scadenza dei certificati rilasciati da Adobe
uuid: 5151ef15-daf6-4fb3-bf83-25ebac1d003b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Gestione degli aggiornamenti dei certificati alla scadenza dei certificati rilasciati da Adobe {#handling-certificate-updates-when-your-adobe-issued-certifcates-expire}

In alcuni casi potrebbe essere necessario ottenere un nuovo certificato da Adobe. Ad esempio, alla scadenza di un certificato di produzione, scade un certificato di valutazione o al passaggio da una valutazione a un certificato di produzione. Quando un certificato scade e non si desidera creare nuovamente un pacchetto per il contenuto che utilizzava il vecchio certificato. È possibile fare in modo che il server licenze conosca sia i vecchi che i nuovi certificati.

Per aggiornare il server con i nuovi certificati, effettuate le seguenti operazioni:

1. (Facoltativo) Quando si aggiungono nuove voci a un elenco di aggiornamenti dei criteri o a un elenco di revoche, assicurarsi di firmare con le nuove credenziali e utilizzare il vecchio certificato per convalidare la firma sul file esistente.

   Ad esempio, utilizzare la riga di comando seguente per aggiungere una voce a un elenco di aggiornamento criteri esistente, firmato utilizzando una credenziale diversa:

   ```
   java -jar AdobePolicyUpdateListManager.jar newList -f oldList oldSigningCert.cer -u pol 0 "" ""
   ```

1. Utilizzate l&#39;API Java per aggiornare il server licenze con il nuovo elenco di aggiornamento criteri o l&#39;elenco di revoche:

   ```
    HandlerConfiguration.setRevocationList() 
   ```

   oppure:

   ```
    HandlerConfiguration.setPolicyUpdateList()
   ```

   Nell’implementazione dei riferimenti, le proprietà utilizzate sono `HandlerConfiguration.RevocationList` e `HandlerConfiguration.PolicyUpdateList`. Aggiornate inoltre il certificato utilizzato per verificare le firme: `RevocationList.verifySignature.X509Certificate`.

1. Per utilizzare il contenuto creato in pacchetti utilizzando i vecchi certificati, il server licenze richiede le credenziali vecchie e nuove del server licenze e le credenziali di trasporto. Aggiornate il server licenze con i certificati nuovi e vecchi.

   Per le credenziali del server licenze:

   * Assicurarsi che la credenziale corrente sia passata al `LicenseHandler` costruttore:

      * Nell&#39;implementazione del riferimento, impostatela tramite la `LicenseHandler.ServerCredential` proprietà.
      * In Adobe Access Server for Protected Streaming, la credenziale corrente deve essere la prima credenziale specificata nell&#39; `LicenseServerCredential` elemento nel file flashaccess-tenant.xml.
   * Assicurarsi che le credenziali correnti e vecchie siano fornite a `AsymmetricKeyRetrieval`

      * Nell&#39;implementazione di riferimento, impostatela attraverso le `LicenseHandler.ServerCredential` `AsymmetricKeyRetrieval.ServerCredential. n` proprietà e.
      * In Adobe Access Server for Protected Streaming, le vecchie credenziali vengono specificate dopo la prima credenziale nell&#39; `LicenseServerCredential` elemento nel file flashaccess-tenant.xml.
   Per le credenziali di trasporto:

   * Assicurarsi che la credenziale corrente sia passata al `HandlerConfiguration.setServerTransportCredential()` metodo:

      * Nell&#39;implementazione del riferimento, impostatela tramite la `HandlerConfiguration.ServerTransportCredential` proprietà.
      * In Adobe Access Server per lo streaming protetto, la credenziale corrente deve essere la prima credenziale specificata nell&#39; `TransportCredential` elemento nel file flashaccess-tenant.xml.
   * Assicurarsi che le vecchie credenziali siano fornite a `HandlerConfiguration.setAdditionalServerTransportCredentials`():

      * Nell&#39;implementazione di riferimento, impostatela attraverso le `HandlerConfiguration.AdditionalServerTransportCredential. n` proprietà.
      * In Adobe Access Server per lo streaming protetto, questo viene specificato dopo la prima credenziale nell&#39; `TransportCredential` elemento nel file flashaccess-tenant.xml.




1. Aggiornate gli strumenti per la creazione di pacchetti in modo da essere certi di creare pacchetti di contenuto con le credenziali correnti. Verificate che per la creazione del pacchetto siano utilizzati il certificato del server licenze, il certificato di trasporto e le credenziali del packager più recenti.
1. Per aggiornare il certificato del server licenze del server chiavi:

   * Aggiorna le credenziali nel file di configurazione del tenant del server di chiavi di Adobe Access. Includete sia le credenziali vecchie che nuove per il server chiavi in flashaccess-keyserver-tenant.xml.
   * Assicurarsi che il certificato corrente sia passato al `HandlerConfiguration.setKeyServerCertificate()` metodo.

      * Nell&#39;implementazione del riferimento, impostatela tramite la `HandlerConfiguration.KeyServerCertificate` proprietà.
      * In Adobe Access Server for Protected Streaming, specificate il certificato del server di chiavi nell&#39;elemento tramite l&#39;elemento Configuration/Tenant/Certificates/KeyServer.

