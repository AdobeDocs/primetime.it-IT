---
title: Gestione degli aggiornamenti dei certificati alla scadenza dei certificati rilasciati dagli Adobi
description: Gestione degli aggiornamenti dei certificati alla scadenza dei certificati rilasciati dagli Adobi
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# Gestione degli aggiornamenti dei certificati alla scadenza dei certificati rilasciati dagli Adobi{#handling-certificate-updates-when-adobe-issued-certificates-expire}

Potrebbe essere necessario ottenere un nuovo certificato da Adobe. Ad esempio, un certificato di produzione scade quando scade un certificato di valutazione o quando si passa da una valutazione a un certificato di produzione. Ogni volta che un certificato scade e non si desidera creare un nuovo pacchetto del contenuto che utilizza il certificato precedente, è possibile rendere noti al server licenze i certificati vecchi e nuovi.

Per aggiornare un server con nuovi certificati:

1. (Facoltativo) Quando si aggiungono nuove voci a un elenco di aggiornamento o di revoca dei criteri DRM esistente, è necessario firmare con le nuove credenziali e utilizzare il certificato precedente per convalidare la firma sul file esistente.

   Ad esempio, è possibile utilizzare la riga di comando seguente per aggiungere una voce a un elenco di aggiornamento dei criteri DRM esistente, firmato con credenziali diverse:

   ```
   java -jar AdobePolicyUpdateListManager.jar newList -f oldList oldSigningCert.cer -u pol 0 "" ""
   ```

1. (Facoltativo) Utilizzare l&#39;API Java per aggiornare il server licenze con il nuovo elenco di aggiornamento o l&#39;elenco di revoche dei criteri DRM:

   ```
   HandlerConfiguration.setRevocationList() 
   ```

   oppure:

   ```
   HandlerConfiguration.setPolicyUpdateList()
   ```

   Nell’implementazione di riferimento, le proprietà utilizzate sono `HandlerConfiguration.RevocationList` e `HandlerConfiguration.PolicyUpdateList`. È inoltre necessario aggiornare il certificato utilizzato per verificare le firme: `RevocationList.verifySignature.X509Certificate`.

1. Aggiornare il server licenze con i certificati nuovi e precedenti.

   Se si desidera utilizzare contenuto creato con i vecchi certificati, assicurarsi che il server licenze abbia accesso alle credenziali del server licenze precedente e nuovo e alle credenziali di trasporto.

   Per le credenziali del server licenze:

   * Assicurati che le credenziali correnti siano passate al `LicenseHandler` costruttore:

      * Nell’implementazione di riferimento, impostala con `LicenseHandler.ServerCredential` proprietà.
      * Nel server Adobe Primetime DRM per lo streaming protetto, le credenziali correnti devono essere le prime credenziali specificate nel `LicenseServerCredential` nel file flashaccess-tenant.xml.

   * Assicurati che le credenziali attuali e precedenti siano fornite a `AsymmetricKeyRetrieval`

      * Nell’implementazione di riferimento, impostala con `LicenseHandler.ServerCredential` e `AsymmetricKeyRetrieval.ServerCredential. n` proprietà.

      * Nel server DRM Primetime per lo streaming protetto, le vecchie credenziali vengono specificate dopo la prima credenziale nel `LicenseServerCredential` nel file flashaccess-tenant.xml.

   Per le credenziali trasporto:

   * Assicurati che le credenziali correnti siano passate al `HandlerConfiguration.setServerTransportCredential()` metodo:

      * Nell’implementazione di riferimento, impostala con `HandlerConfiguration.ServerTransportCredential` proprietà.
      * Nel server DRM di Primetime per lo streaming protetto, le credenziali correnti devono essere le prime credenziali specificate in `TransportCredential` elemento nel [!DNL flashaccess-tenant.xml] file.

   * Assicurati che le vecchie credenziali vengano fornite a `HandlerConfiguration.setAdditionalServerTransportCredentials`():

      * Nell’implementazione di riferimento, impostala con `HandlerConfiguration.AdditionalServerTransportCredential. n` proprietà.
      * Nel server DRM Primetime per lo streaming protetto, questo viene specificato dopo la prima credenziale nel `TransportCredential` nel file flashaccess-tenant.xml.

1. Aggiorna gli strumenti di creazione pacchetti per assicurarti che stiano creando pacchetti di contenuto con le credenziali correnti. Verificare che per la creazione di pacchetti vengano utilizzati il certificato del server licenze, il certificato di trasporto e le credenziali del packager più recenti.
1. Aggiornare il certificato del server licenze del server chiavi nel modo seguente:

   * Aggiornare le credenziali nel file di configurazione del tenant Adobe Primetime DRM Key Server includendo sia le credenziali del server chiavi precedenti che quelle nuove in flashaccess-keyserver-tenant.xml.
   * Verifica che il certificato corrente sia passato al `HandlerConfiguration.setKeyServerCertificate()` metodo.

      * Nell’implementazione di riferimento, impostala con `HandlerConfiguration.KeyServerCertificate` proprietà.
      * In Primetime DRM Server for Protected Streaming, specificare il certificato del server chiavi nell&#39;elemento tramite Configuration/Tenant/Certificates/KeyServer.
