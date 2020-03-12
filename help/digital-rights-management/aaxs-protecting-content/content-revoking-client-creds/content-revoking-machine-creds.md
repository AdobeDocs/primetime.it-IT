---
seo-title: Revoca delle credenziali del computer
title: Revoca delle credenziali del computer
uuid: 16119ff9-8147-4fe0-9744-a705d94a9400
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Revoca delle credenziali del computer{#revoking-machine-credentials}

Adobe gestisce un CRL per la revoca delle credenziali del computer notoriamente compromesse. L&#39;SDK applica automaticamente questo CRL. Se sono presenti computer aggiuntivi ai quali non si desidera che il server licenze rilasci licenze, è possibile creare un elenco di revoche dei computer e aggiungere il nome dell&#39;emittente e il numero di serie dei token computer che si desidera escludere (utilizzare `MachineToken.getMachineTokenId()` per recuperare il nome dell&#39;emittente e il numero di serie del certificato del computer).

La revoca delle credenziali del computer implica l&#39;utilizzo di un `RevocationListFactory` oggetto. Per creare un elenco di revoche, caricare un elenco di revoche esistente e verificare se un token computer è stato revocato utilizzando l&#39;API Java, eseguire le operazioni seguenti:

1. Configurate l&#39;ambiente di sviluppo e includete tutti i file JAR menzionati in [Impostazione dell&#39;ambiente](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) di sviluppo all&#39;interno del progetto.
1. Creare un&#39; `ServerCredentialFactory` istanza per caricare le credenziali necessarie per la firma. Le credenziali del server licenze vengono utilizzate per firmare l&#39;elenco di revoche.
1. Create un&#39; `RevocationListFactory` istanza.
1. Specificare l&#39;emittente e il numero di serie del token computer da revocare utilizzando un `IssuerAndSerialNumber` oggetto. Tutte le richieste di Adobe Access contengono un token computer.
1. Creare un `RevocationList` oggetto utilizzando l&#39; `IssuerAndSerialNumber` oggetto appena creato e aggiungerlo all&#39;elenco di revoca passandolo in `RevocationListFactory.addRevocationEntry()`. Generare il nuovo elenco di revoche chiamando `RevocationListFactory.generateRevocationList()`.
1. Per salvare l&#39;elenco di revoche, è possibile serializzarlo chiamando `RevocationList.getBytes()`. Per caricare l’elenco, chiamare `RevocationListFactory.loadRevocationList()` e trasmettere l’elenco serializzato.
1. Verificare che la firma sia valida e che l&#39;elenco sia stato firmato dal server licenze corretto chiamando `RevocationList.verifySignature()`.
1. Per verificare se una voce è stata revocata, passare l&#39; `IssuerAndSerialNumber` oggetto in `RevocationList.isRevoked()`. L&#39;elenco di revoche può anche essere passato in modo `HandlerConfiguration` che l&#39;SDK applichi l&#39;elenco di revoche per tutte le richieste di autenticazione e licenza.

Per aggiungere altre voci a un elenco esistente `RevocationList`, caricare un elenco di revoche esistente. Creare una nuova `RevocationListFactory` istanza e assicurarsi di incrementare il numero CRL. Chiamata `RevocationListFactioryEntries.addRevocationEntries` per aggiungere tutte le voci dal vecchio elenco al nuovo elenco. Chiamata `RevocationListFactory.addRevocationEntry` per aggiungere eventuali nuove voci di revoca all&#39;elenco RevocationList.

Per un esempio di codice che illustra come creare un elenco di revoche, caricare un elenco di revoche esistente e verificare se un token computer è stato revocato, vedere `com.adobe.flashaccess.samples.revocation.CreateRevocationList` nella directory &quot;sample&quot; degli strumenti della riga di comando di implementazione di riferimento.
