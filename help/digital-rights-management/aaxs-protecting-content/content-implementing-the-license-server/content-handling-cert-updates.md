---
title: Gestione degli aggiornamenti dei certificati alla scadenza dei certificati rilasciati dagli Adobi
description: Gestione degli aggiornamenti dei certificati alla scadenza dei certificati rilasciati dagli Adobi
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---


# Gestione degli aggiornamenti dei certificati alla scadenza dei certificati rilasciati dagli Adobi {#handling-certificate-updates-when-your-adobe-issued-certifcates-expire}

In alcuni casi potrebbe essere necessario ottenere un nuovo certificato dall’Adobe. Ad esempio, quando un certificato di produzione scade, scade un certificato di valutazione o quando si passa da una valutazione a un certificato di produzione. Quando un certificato scade e non desideri creare un nuovo pacchetto per il contenuto che ha utilizzato il vecchio certificato. È possibile fare in modo che il server licenze conosca i certificati vecchi e nuovi.

Segui la procedura seguente per aggiornare il server con i nuovi certificati:

1. (Facoltativo) Quando si aggiungono nuove voci a un elenco di aggiornamenti dei criteri o a un elenco di revoche esistenti, assicurarsi di firmare con le nuove credenziali e utilizzare il vecchio certificato per convalidare la firma nel file esistente.

   Ad esempio, utilizzare la riga di comando seguente per aggiungere una voce a un elenco di aggiornamento dei criteri esistente, firmato utilizzando una credenziale diversa:

   ```
   java -jar AdobePolicyUpdateListManager.jar newList -f oldList oldSigningCert.cer -u pol 0 "" ""
   ```

1. Utilizza l’API Java per aggiornare il server licenze con il nuovo elenco di aggiornamenti dei criteri o l’elenco di revoche:

   ```
    HandlerConfiguration.setRevocationList() 
   ```

   o:

   ```
    HandlerConfiguration.setPolicyUpdateList()
   ```

   Nell’implementazione di riferimento, le proprietà utilizzate sono `HandlerConfiguration.RevocationList` e `HandlerConfiguration.PolicyUpdateList`. Aggiorna anche il certificato utilizzato per verificare le firme: `RevocationList.verifySignature.X509Certificate`.

1. Per utilizzare il contenuto compilato utilizzando i vecchi certificati, il server licenze richiede le credenziali del server licenze vecchie e nuove e le credenziali di trasporto. Aggiorna il server licenze con i certificati nuovi e vecchi.

   Per le credenziali del server licenze:

   * Assicurati che la credenziale corrente sia passata nel costruttore `LicenseHandler` :

      * Nell&#39;implementazione di riferimento, impostala tramite la proprietà `LicenseHandler.ServerCredential` .
      * In Adobe Access Server per lo streaming protetto, la credenziale corrente deve essere la prima credenziale specificata nell&#39;elemento `LicenseServerCredential` nel file flashaccess-tenant.xml .
   * Assicurati che le credenziali attuali e precedenti siano fornite a `AsymmetricKeyRetrieval`

      * Nell’implementazione di riferimento, impostala tramite le proprietà `LicenseHandler.ServerCredential` e `AsymmetricKeyRetrieval.ServerCredential. n` .
      * In Adobe Access Server per lo streaming protetto, le vecchie credenziali vengono specificate dopo la prima credenziale nell&#39;elemento `LicenseServerCredential` nel file flashaccess-tenant.xml .

   Per le credenziali di trasporto:

   * Assicurati che la credenziale corrente sia passata nel metodo `HandlerConfiguration.setServerTransportCredential()` :

      * Nell&#39;implementazione di riferimento, impostala tramite la proprietà `HandlerConfiguration.ServerTransportCredential` .
      * In Adobe Access Server per lo streaming protetto, la credenziale corrente deve essere la prima credenziale specificata nell&#39;elemento `TransportCredential` nel file flashaccess-tenant.xml .
   * Assicurati che le vecchie credenziali siano fornite a `HandlerConfiguration.setAdditionalServerTransportCredentials`():

      * Nell’implementazione di riferimento, impostala tramite le proprietà `HandlerConfiguration.AdditionalServerTransportCredential. n` .
      * In Adobe Access Server per lo streaming protetto, questo viene specificato dopo la prima credenziale nell&#39;elemento `TransportCredential` nel file flashaccess-tenant.xml.




1. Aggiorna gli strumenti di packaging per assicurarti che il contenuto venga compilato con le credenziali correnti. Assicurati che per il packaging siano utilizzati il certificato del server licenze, il certificato di trasporto e le credenziali del packager più recenti.
1. Per aggiornare il certificato del server licenze del server chiavi:

   * Aggiornare le credenziali nel file di configurazione del tenant del server chiavi di accesso Adobe. Includere le credenziali vecchie e nuove del server chiavi in flashaccess-keyserver-tenant.xml.
   * Verifica che il certificato corrente sia passato nel metodo `HandlerConfiguration.setKeyServerCertificate()` .

      * Nell&#39;implementazione di riferimento, impostala tramite la proprietà `HandlerConfiguration.KeyServerCertificate` .
      * In Adobe Access Server per lo streaming protetto, specifica il certificato del server chiavi in tramite l’elemento Configuration/Tenant/Certificates/KeyServer .

