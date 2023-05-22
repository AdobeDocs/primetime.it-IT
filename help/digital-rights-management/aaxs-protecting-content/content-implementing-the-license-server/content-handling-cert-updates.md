---
title: Gestione degli aggiornamenti dei certificati alla scadenza dei certificati rilasciati dagli Adobi
description: Gestione degli aggiornamenti dei certificati alla scadenza dei certificati rilasciati dagli Adobi
copied-description: true
exl-id: 9768544e-7e92-4c3a-9863-af9aed74a0c0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---

# Gestione degli aggiornamenti dei certificati alla scadenza dei certificati rilasciati dagli Adobi {#handling-certificate-updates-when-your-adobe-issued-certifcates-expire}

In alcuni casi potrebbe essere necessario ottenere un nuovo certificato da Adobe. Ad esempio, quando scade un certificato di produzione, scade un certificato di valutazione o quando si passa da una valutazione a un certificato di produzione. Quando un certificato scade e non desideri creare un nuovo pacchetto del contenuto che ha utilizzato il certificato precedente. È possibile rendere noti al server licenze i certificati vecchi e quelli nuovi.

Per aggiornare il server con i nuovi certificati, attenersi alla procedura descritta di seguito.

1. (Facoltativo) Quando si aggiungono nuove voci a un elenco di aggiornamento dei criteri o a un elenco di revoche esistente, assicurarsi di firmare con le nuove credenziali e utilizzare il certificato precedente per convalidare la firma sul file esistente.

   Ad esempio, utilizzare la riga di comando seguente per aggiungere una voce a un elenco di aggiornamento dei criteri esistente, firmato con credenziali diverse:

   ```
   java -jar AdobePolicyUpdateListManager.jar newList -f oldList oldSigningCert.cer -u pol 0 "" ""
   ```

1. Utilizzare l&#39;API Java per aggiornare il server licenze con il nuovo elenco di aggiornamento o di revoca dei criteri:

   ```
    HandlerConfiguration.setRevocationList() 
   ```

   oppure:

   ```
    HandlerConfiguration.setPolicyUpdateList()
   ```

   Nell’implementazione di riferimento, le proprietà utilizzate sono `HandlerConfiguration.RevocationList` e `HandlerConfiguration.PolicyUpdateList`. Aggiorna anche il certificato utilizzato per verificare le firme: `RevocationList.verifySignature.X509Certificate`.

1. Per utilizzare il contenuto creato con i certificati precedenti, il server licenze richiede le credenziali del server licenze e del trasporto precedenti e nuove. Aggiornare il server licenze con i certificati nuovi e precedenti.

   Per le credenziali del server licenze:

   * Assicurati che le credenziali correnti siano passate nel `LicenseHandler` costruttore:

      * Nell’implementazione di riferimento, impostala tramite `LicenseHandler.ServerCredential` proprietà.
      * In Adobe Access Server for Protected Streaming, le credenziali correnti devono essere le prime credenziali specificate in `LicenseServerCredential` nel file flashaccess-tenant.xml.
   * Assicurati che le credenziali attuali e precedenti siano fornite a `AsymmetricKeyRetrieval`

      * Nell’implementazione di riferimento, impostala tramite `LicenseHandler.ServerCredential` e `AsymmetricKeyRetrieval.ServerCredential. n` proprietà.
      * In Adobe Access Server for Protected Streaming, le vecchie credenziali vengono specificate dopo la prima credenziale in `LicenseServerCredential` nel file flashaccess-tenant.xml.
   Per le credenziali trasporto:

   * Assicurati che le credenziali correnti siano passate nel `HandlerConfiguration.setServerTransportCredential()` metodo:

      * Nell’implementazione di riferimento, impostala tramite `HandlerConfiguration.ServerTransportCredential` proprietà.
      * In Adobe Access Server per lo streaming protetto, le credenziali correnti devono essere le prime credenziali specificate in `TransportCredential` nel file flashaccess-tenant.xml.
   * Assicurati che le vecchie credenziali vengano fornite a `HandlerConfiguration.setAdditionalServerTransportCredentials`():

      * Nell’implementazione di riferimento, impostala tramite `HandlerConfiguration.AdditionalServerTransportCredential. n` proprietà.
      * In Adobe Access Server per lo streaming protetto, questo viene specificato dopo la prima credenziale nel `TransportCredential` nel file flashaccess-tenant.xml.




1. Aggiorna gli strumenti di creazione pacchetti per assicurarti che stiano creando pacchetti di contenuto con le credenziali correnti. Verificare che per la creazione di pacchetti vengano utilizzati il certificato del server licenze, il certificato di trasporto e le credenziali del packager più recenti.
1. Per aggiornare il certificato del server licenze del server chiavi:

   * Aggiorna le credenziali nel file di configurazione del tenant Adobe Access Key Server. Includi sia le credenziali del server chiavi precedenti che quelle nuove in flashaccess-keyserver-tenant.xml.
   * Verifica che il certificato corrente sia passato in `HandlerConfiguration.setKeyServerCertificate()` metodo.

      * Nell’implementazione di riferimento, impostala tramite `HandlerConfiguration.KeyServerCertificate` proprietà.
      * In Adobe Access Server for Protected Streaming, specifica il certificato del server chiavi in tramite l&#39;elemento Configuration/Tenant/Certificates/KeyServer.
