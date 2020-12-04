---
description: 'È necessario assicurarsi di rilasciare licenze in modo sicuro. Prendere in considerazione le procedure ottimali per proteggere il server licenze '
seo-description: 'È necessario assicurarsi di rilasciare licenze in modo sicuro. Prendere in considerazione le procedure ottimali per proteggere il server licenze '
seo-title: Protezione del server licenze
title: Protezione del server licenze
uuid: 7b5de17d-d0a7-41df-9651-4ff51c9965c6
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 0%

---


# Protezione del server licenze {#protecting-the-license-server}

È necessario assicurarsi di rilasciare licenze in modo sicuro. Per proteggere il server licenze, attenersi alle procedure ottimali riportate di seguito.

## Utilizzo di CRL generati localmente {#consuming-locally-generated-crls}

Per utilizzare elenchi di revoche di certificati (CRL, Certificate Revocation List) generati localmente ed elenchi di aggiornamenti di criteri, utilizzare  API DRM di Adobe Primetime per verificare la firma.

Le seguenti API verificano che gli elenchi non siano stati alterati e che gli elenchi siano stati firmati dal server licenze corretto:

* Chiamare [RevocationList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html#verifySignature(java.security.cert.X509Certificate)) per verificare la firma prima di fornire l&#39; [RevocationList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html) a qualsiasi API.

   Per ulteriori informazioni, vedere [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

* Chiama [PolicyUpdateList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html#verifySignature(java.security.cert.X509Certificate)) per controllare la firma prima di fornire la `PolicyUpdateList` a qualsiasi API.

   Per ulteriori informazioni, vedere [PolicyUpdateList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html).

## Utilizzo di CRL pubblicati da  Adobe{#consuming-crls-published-by-adobe}

L&#39;SDK scarica periodicamente i CRL pubblicati da  Adobe. È necessario assicurarsi che l&#39;accesso a questi file non sia bloccato o che l&#39;applicazione di tali CRL non sia impedita.

L&#39;SDK dispone di un&#39;opzione di configurazione che consente di ignorare gli errori durante il recupero  CRL di Adobe e potete applicare questa opzione solo in ambienti di sviluppo. Negli ambienti di produzione, il server licenze deve recuperare i CRL da  Adobe. Se il server licenze non è in grado di ottenere un CRL valido, si è verificato un errore.

## Generazione di CRL per completare quelli pubblicati da  Adobe{#generating-crls-to-supplement-those-published-by-adobe}

È possibile utilizzare  Adobe Primetime DRM per creare CRL che integrano il computer CRL pubblicato da  Adobe.

L&#39;SDK DRM di Primetime verifica e applica i CRL del Adobe . Tuttavia, è possibile rifiutare computer client aggiuntivi creando un CRL che revoca credenziali computer aggiuntive trasmettendo il CRL all&#39;SDK DRM di Primetime. Quando rilasci una licenza, l&#39;SDK verifica il CRL del Adobe  e il CRL.

Per generare CRL, vedere [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

## Rilevamento del rollback {#rollback-detection}

Se l&#39;implementazione di  Adobe Primetime DRM utilizza regole aziendali che richiedono al client di mantenere lo stato (ad esempio, l&#39;intervallo della finestra di riproduzione),  Adobe consiglia al server di tenere traccia del contatore di rollback e di utilizzare AIR o SWF per consentire l&#39;elencazione.

Il contatore di rollback viene inviato al server nella maggior parte delle richieste dal client. Se l&#39;implementazione di Primetime DRM non richiede il contatore di rollback, può essere ignorata. In caso contrario,  Adobe consiglia al server di memorizzare l&#39;ID computer casuale, ottenuto utilizzando [MachineToken.getUniqueId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()), e il valore del contatore corrente in un database.

Per ulteriori informazioni su come incrementare e monitorare il contatore di rollback, vedere [Rilevamento ClientState](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/ClientState.html) e Rilevamento di rollback.

## Conteggio computer per il rilascio delle licenze {#machine-count-when-issuing-licenses}

Se le regole aziendali richiedono il tracciamento del numero di computer per un utente, il server licenze o il server di dominio devono memorizzare gli ID computer associati all&#39;utente.

Il modo più efficace per tenere traccia degli ID computer è quello di memorizzare il valore restituito dal metodo [MachineId.getBytes()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getBytes()) in un database. Quando viene ricevuta una nuova richiesta, confrontate l&#39;ID computer della richiesta con gli ID computer noti utilizzando [MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)).

[MachineId.matches() ](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)) esegue un confronto degli ID per determinare se gli ID rappresentano lo stesso computer. Questo confronto è pratico solo se è presente un numero limitato di ID computer. Ad esempio, se agli utenti sono concessi cinque computer nel loro dominio, è possibile ricercare nel database gli ID computer associati al nome utente dell&#39;utente e ottenere un piccolo set di dati per il confronto.

Questo confronto non è pratico per le installazioni che consentono l&#39;accesso anonimo. In questo caso, è possibile utilizzare [MachineId.getUniqueID()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()). Tuttavia, questo ID non può essere lo stesso se l&#39;utente accede al contenuto dai runtime Adobe AIR® e di Flash e .

>[!NOTE]
>
>L&#39;ID non sopravvive se l&#39;utente riformatta il disco rigido.

## Protezione riproduzione {#replay-protection}

La protezione di ripetizione impedisce a un aggressore di riprodurre un messaggio di richiesta di licenza e potrebbe causare un attacco DoS (Denial of Service) contro il client.

Un attacco DoS è un tentativo da parte degli aggressori di impedire agli utenti legittimi di un servizio di utilizzare tale servizio. Ad esempio, un attacco di ripetizione che utilizza il contatore di rollback potrebbe essere utilizzato per &quot;ingannare&quot; il server licenze a pensare che il client DRM abbia ripristinato il suo stato, causando una sospensione dell&#39;account.

Per ulteriori informazioni sulla protezione della riproduzione, vedere [ AbstractRequestMessage.getMessageId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/AbstractRequestMessage.html#getMessageId()).

## Gestione di un elenco consentiti  di pacchetti di contenuti affidabili {#maintain-a-allowlist-of-trusted-content-packagers}

Un elenco consentiti  è un elenco di entità affidabili.

Per i pacchetti di contenuti, le entità sono organizzazioni considerate attendibili dal proprietario del contenuto per creare pacchetti (o cifrare) di file video e creare contenuto protetto DRM. Durante la distribuzione  Adobe Primetime DRM, è necessario mantenere un elenco consentiti  di pacchetti di contenuti affidabili. Prima di rilasciare una licenza, è inoltre necessario verificare l&#39;identità di Content Packager nei metadati DRM di un file protetto DRM.

Per informazioni su come ottenere informazioni sull&#39;entità che ha creato il pacchetto del contenuto, vedere [V2ContentMetaData.getPackagerInfo()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo()).

## Timeout per token di autenticazione{#timeout-for-authentication-tokens}

Tutti i token di autenticazione generati dall’SDK  Adobe Primetime DRM dispongono di un intervallo di timeout per proteggere la sicurezza dell’applicazione.

La scadenza per il token di autenticazione è specificata utilizza l&#39;SDK DRM di Primetime per gestire una richiesta di autenticazione. Una volta scaduto, il token non è più valido e l&#39;utente deve eseguire nuovamente l&#39;autenticazione con il server licenze.

Per ulteriori informazioni sulle richieste di autenticazione, vedere [AuthenticationHandler](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/authentication/AuthenticationHandler.html).

## Sovrapposizione delle opzioni del criterio {#overriding-policy-options}

Quando rilasciate una licenza, il server licenze può ignorare le regole di utilizzo specificate nel criterio.

Se il criterio specifica una data di inizio, una licenza non viene generata prima di tale data. Tuttavia, potete impostare una data di inizio futura nella licenza dopo la generazione della licenza. Questa opzione deve essere utilizzata con cautela perché il client non può impedire all&#39;utente di spostare l&#39;ora del sistema in avanti per eludere la data di inizio.