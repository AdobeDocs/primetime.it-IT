---
description: È necessario assicurarsi di rilasciare le licenze in modo sicuro. Considera queste best practice per proteggere il server licenze
title: Protezione del server licenze
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1178'
ht-degree: 0%

---

# Protezione del server licenze {#protecting-the-license-server}

È necessario assicurarsi di rilasciare le licenze in modo sicuro. Per proteggere il server licenze, prendere in considerazione le procedure consigliate riportate di seguito.

## Utilizzo di CRL generati localmente {#consuming-locally-generated-crls}

Per utilizzare gli elenchi di revoche di certificati (CRL) generati localmente e gli elenchi di aggiornamento dei criteri, utilizza le API Adobe Primetime DRM per verificare la firma.

Le seguenti API verificano che gli elenchi non siano stati manomessi e che siano stati firmati dal server licenze corretto:

* Chiamata [RevocationList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html#verifySignature(java.security.cert.X509Certificate)) per verificare la firma prima di fornire [RevocationList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html) a qualsiasi API.

  Per ulteriori informazioni, consulta [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

* Chiamata [PolicyUpdateList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html#verifySignature(java.security.cert.X509Certificate)) per verificare la firma prima di fornire `PolicyUpdateList` a qualsiasi API.

  Per ulteriori informazioni, consulta [PolicyUpdateList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html).

## Utilizzo di CRL pubblicati da Adobe{#consuming-crls-published-by-adobe}

L’SDK scarica periodicamente i CRL pubblicati da Adobe. Assicurati che l’accesso a questi file non sia bloccato o che l’applicazione di questi CRL non sia impedita.

L’SDK dispone di un’opzione di configurazione che consente di ignorare gli errori durante il recupero dei CRL di Adobe e di applicare questa opzione solo negli ambienti di sviluppo. Negli ambienti di produzione, il server licenze deve recuperare i CRL da Adobe. Se il server licenze non è in grado di ottenere un CRL valido, si è verificato un errore.

## Generazione di CRL per integrare quelli pubblicati da Adobe{#generating-crls-to-supplement-those-published-by-adobe}

È possibile utilizzare Adobe Primetime DRM per creare CRL che integrano il CRL del computer pubblicato da Adobe.

L’SDK di Primetime DRM verifica e applica i CRL Adobe. Tuttavia, è possibile non consentire l&#39;aggiunta di computer client creando un CRL che revoca le credenziali del computer aggiuntive passando il CRL all&#39;SDK DRM di Primetime. Quando rilasci una licenza, l’SDK controlla l’Adobe CRL e l’CRL.

Per generare i CRL, consulta [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

## Rilevamento rollback {#rollback-detection}

Se l&#39;implementazione di Adobe Primetime DRM utilizza regole aziendali che richiedono al client di mantenere lo stato (ad esempio, l&#39;intervallo di intervallo della finestra di riproduzione), l&#39;Adobe consiglia al server di tenere traccia del contatore di rollback e di utilizzare l&#39;elenco Consentiti di AIR o SWF.

Il contatore di rollback viene inviato al server nella maggior parte delle richieste provenienti dal client. Se l’implementazione di Primetime DRM non richiede il contatore di rollback, questo può essere ignorato. In caso contrario, Adobe consiglia che il server memorizzi l’ID computer casuale, ottenuto utilizzando [MachineToken.getUniqueId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId())e il valore del contatore corrente in un database.

Per ulteriori informazioni su come incrementare e tenere traccia del contatore di rollback, vedere [ClientState](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/ClientState.html) e il rilevamento di rollback.

## Conteggio computer al momento del rilascio delle licenze {#machine-count-when-issuing-licenses}

Se le regole business richiedono la registrazione del numero di computer per un utente, il server licenze o il server di dominio deve memorizzare gli ID computer associati all&#39;utente.

Il modo più affidabile per tenere traccia degli ID macchina è memorizzare il valore restituito dalla [MachineId.getBytes()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getBytes()) in un database. Quando viene ricevuta una nuova richiesta, confronta l’ID computer nella richiesta con gli ID computer noti utilizzando [MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)).

[MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)) esegue un confronto tra gli ID per determinare se questi rappresentano la stessa macchina. Questo confronto è utile solo se il numero di ID computer è limitato. Ad esempio, se nel dominio degli utenti sono consentiti cinque computer, è possibile cercare nel database gli ID computer associati al nome utente dell&#39;utente e ottenere un piccolo set di dati da confrontare.

Questo confronto non è pratico per le distribuzioni che consentono l’accesso anonimo. In questo caso, [MachineId.getUniqueID()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()) possono essere utilizzati. Tuttavia, questo ID non può essere lo stesso se l’utente accede al contenuto dal Flash e dai runtime di Adobe AIR®.

>[!NOTE]
>
>L&#39;ID non viene mantenuto se l&#39;utente riformatta il disco rigido.

## Protezione dalla ripetizione {#replay-protection}

La protezione della ripetizione impedisce a un utente malintenzionato di riprodurre un messaggio di richiesta di licenza e può causare un attacco Denial of Service (DoS) contro il client.

Un attacco DoS è un tentativo da parte degli aggressori di impedire agli utenti legittimi di un servizio di utilizzare tale servizio. Ad esempio, un attacco di ripetizione che utilizza il contatore di rollback potrebbe essere utilizzato per &quot;ingannare&quot; il server licenze a pensare che il client DRM abbia ripristinato il suo stato, causando una sospensione dell’account.

Per ulteriori informazioni sulla protezione dalla ripetizione, consulta [AbstractRequestMessage.getMessageId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/AbstractRequestMessage.html#getMessageId()).

## Gestisci un elenco consentiti di pacchetti di contenuti attendibili {#maintain-a-allowlist-of-trusted-content-packagers}

Un elenco consentiti è un elenco di entità attendibili.

Per i creatori di pacchetti di contenuti, le entità sono organizzazioni considerate attendibili dal proprietario del contenuto per creare pacchetti (o crittografare) di file video e creare contenuti protetti da DRM. Durante l’implementazione di Adobe Primetime DRM, è necessario mantenere un elenco consentiti di pacchetti di contenuti affidabili. Prima di rilasciare una licenza, è necessario verificare l&#39;identità del Content Packager nei metadati DRM di un file protetto da DRM.

Per informazioni su come ottenere informazioni sull’entità che ha creato il pacchetto del contenuto, consulta [V2ContentMetaData.getPackagerInfo()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo()).

## Timeout per i token di autenticazione{#timeout-for-authentication-tokens}

Tutti i token di autenticazione generati dall’SDK Adobe Primetime DRM presentano un intervallo di timeout per proteggere la sicurezza dell’applicazione.

La scadenza per il token di autenticazione è specificata utilizza l’SDK DRM di Primetime durante la gestione di una richiesta di autenticazione. Dopo la scadenza, il token non è più valido e l’utente deve autenticarsi di nuovo con il server licenze.

Per ulteriori informazioni sulle richieste di autenticazione, consulta [AuthenticationHandler](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/authentication/AuthenticationHandler.html).

## Sovrascrittura delle opzioni dei criteri {#overriding-policy-options}

Quando si rilascia una licenza, il server licenze può ignorare le regole di utilizzo specificate nel criterio.

Se il criterio specifica una data di inizio, la licenza non viene generata prima di tale data. Tuttavia, è possibile impostare una data di inizio futura nella licenza dopo la generazione della licenza. Questa opzione deve essere utilizzata con cautela perché il client non può impedire all’utente di posticipare l’ora di sistema per aggirare la data di inizio.
