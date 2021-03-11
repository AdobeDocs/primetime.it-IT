---
description: 'Devi accertarti di aver rilasciato licenze in modo sicuro. Prendere in considerazione queste best practice per proteggere il server licenze '
title: Protezione del server licenze
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '1178'
ht-degree: 0%

---


# Protezione del server licenze {#protecting-the-license-server}

Devi accertarti di aver rilasciato licenze in modo sicuro. Per proteggere il server licenze, prendere in considerazione le seguenti best practice:

## Utilizzo di CRL generati localmente {#consuming-locally-generated-crls}

Per utilizzare elenchi di revoche di certificati (CRL) generati localmente e elenchi di aggiornamenti dei criteri, utilizza le API DRM di Adobe Primetime per verificare la firma.

Le seguenti API verificano che gli elenchi non siano stati manomessi e che siano stati firmati dal server licenze corretto:

* Chiama [RevocationList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html#verifySignature(java.security.cert.X509Certificate)) per controllare la firma prima di fornire il [RevocationList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html) a qualsiasi API.

   Per ulteriori informazioni, vedere [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

* Chiama [PolicyUpdateList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html#verifySignature(java.security.cert.X509Certificate)) per controllare la firma prima di fornire `PolicyUpdateList` a qualsiasi API.

   Per ulteriori informazioni, vedere [PolicyUpdateList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html).

## Utilizzo dei CRL pubblicati da Adobe{#consuming-crls-published-by-adobe}

L’SDK scarica periodicamente i CRL pubblicati da Adobe. È necessario assicurarsi che l&#39;accesso a questi file non sia bloccato o che l&#39;applicazione di tali CRL non sia impedita.

L’SDK dispone di un’opzione di configurazione per ignorare gli errori durante il recupero dei CRL di Adobe e puoi applicare questa opzione solo negli ambienti di sviluppo. Negli ambienti di produzione, il server licenze deve recuperare i CRL da Adobe. Se il server licenze non è in grado di ottenere un CRL valido, si è verificato un errore.

## Generazione di CRL per completare quelli pubblicati da Adobe{#generating-crls-to-supplement-those-published-by-adobe}

È possibile utilizzare Adobe Primetime DRM per creare CRL che integrano il machine CRL pubblicato da Adobe.

L’SDK DRM di Primetime controlla e applica gli Adobe CRL. Tuttavia, puoi impedire l’utilizzo di computer client aggiuntivi creando un CRL che revoca le credenziali aggiuntive del computer passando il CRL all’SDK DRM di Primetime. Quando rilasci una licenza, l&#39;SDK controlla l&#39;Adobe CRL e il tuo CRL.

Per generare CRL, vedere [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

## Rilevamento di ripristino {#rollback-detection}

Se l&#39;implementazione di Adobe Primetime DRM utilizza regole aziendali che richiedono al client di mantenere lo stato (ad esempio, l&#39;intervallo della finestra di riproduzione), l&#39;Adobe consiglia al server di tenere traccia del contatore di rollback e di utilizzare l&#39;elenco Consentiti in AIR o SWF.

Il contatore di rollback viene inviato al server nella maggior parte delle richieste dal client. Se l&#39;implementazione di Primetime DRM non richiede il contatore di rollback, può essere ignorato. In caso contrario, Adobe consiglia al server di memorizzare l&#39;ID computer casuale, ottenuto utilizzando [MachineToken.getUniqueId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()), e il valore del contatore corrente in un database.

Per ulteriori informazioni su come incrementare e tenere traccia del contatore di rollback, vedere [ClientState](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/ClientState.html) e Rilevamento di rollback.

## Numero di macchine al momento del rilascio delle licenze {#machine-count-when-issuing-licenses}

Se le regole business richiedono il tracciamento del numero di computer per un utente, il server licenze o il server di dominio devono memorizzare gli ID computer associati all&#39;utente.

Il modo più efficace per tenere traccia degli ID computer è quello di memorizzare il valore restituito dal metodo [MachineId.getBytes()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getBytes()) in un database. Quando viene ricevuta una nuova richiesta, confronta l’ID computer nella richiesta con gli ID computer noti utilizzando [MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)).

[MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)) esegue un confronto degli ID per determinare se gli ID rappresentano la stessa macchina. Questo confronto è pratico solo se è presente un numero limitato di ID macchina. Ad esempio, se agli utenti sono consentiti cinque computer nel loro dominio, puoi cercare nel database gli ID computer associati al nome utente dell’utente e ottenere un piccolo set di dati da confrontare.

Questo confronto non è pratico per le distribuzioni che consentono l’accesso anonimo. In questo caso, è possibile utilizzare [MachineId.getUniqueID()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()). Tuttavia, questo ID non può essere lo stesso se l&#39;utente accede al contenuto dai runtime Flash e Adobe AIR®.

>[!NOTE]
>
>L&#39;ID non sopravvive se l&#39;utente riformatta il disco rigido.

## Protezione di riproduzione {#replay-protection}

La protezione dalla riproduzione impedisce a un autore dell’attacco di riprodurre un messaggio di richiesta di licenza e potrebbe causare un attacco Denial of Service (DoS) contro il client.

Un attacco DoS è un tentativo da parte degli aggressori di impedire agli utenti legittimi di un servizio di utilizzare quel servizio. Ad esempio, un attacco di ripetizione che utilizza il contatore di rollback potrebbe essere utilizzato per &quot;ingannare&quot; il server licenze a pensare che il client DRM abbia ripristinato il proprio stato, il che causa una sospensione dell&#39;account.

Per ulteriori informazioni sulla protezione della riproduzione, consulta [ AbstractRequestMessage.getMessageId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/AbstractRequestMessage.html#getMessageId()).

## Gestisci un elenco consentiti di pacchetti di contenuti affidabili {#maintain-a-allowlist-of-trusted-content-packagers}

Un elenco consentiti è un elenco di entità affidabili.

Per i pacchetti di contenuti, le entità sono organizzazioni affidabili dal proprietario del contenuto per creare pacchetti (o cifrare) dei file video e creare contenuti protetti da DRM. Quando distribuisci Adobe Primetime DRM, devi mantenere un elenco consentiti di pacchetti di contenuti affidabili. È inoltre necessario verificare l&#39;identità del content packager nei metadati DRM di un file protetto DRM prima di rilasciare una licenza.

Per informazioni su come ottenere informazioni sull&#39;entità che ha generato il contenuto, consulta [V2ContentMetaData.getPackagerInfo()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo()).

## Timeout per token di autenticazione{#timeout-for-authentication-tokens}

Tutti i token di autenticazione generati dall’SDK DRM di Adobe Primetime hanno un intervallo di timeout per proteggere la sicurezza dell’applicazione.

La scadenza per il token di autenticazione è specificata utilizza l’SDK DRM di Primetime quando gestisci una richiesta di autenticazione. Una volta scaduto, il token non è più valido e l’utente deve eseguire nuovamente l’autenticazione con il server licenze.

Per ulteriori informazioni sulle richieste di autenticazione, consulta [AuthenticationHandler](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/authentication/AuthenticationHandler.html).

## Opzioni dei criteri di sovrascrittura {#overriding-policy-options}

Quando si rilascia una licenza, il server licenze può ignorare le regole di utilizzo specificate nel criterio.

Se il criterio specifica una data di inizio, una licenza non viene generata prima di tale data di inizio. Tuttavia, puoi impostare una data di inizio futura nella licenza dopo la generazione della licenza. Questa opzione deve essere utilizzata con cautela perché il client non può impedire all’utente di spostare l’ora del sistema in avanti per aggirare la data di inizio.