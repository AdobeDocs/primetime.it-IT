---
seo-title: Revoca delle credenziali del computer
title: Revoca delle credenziali del computer
uuid: 3647c843-5f1a-457e-949d-10a6278b1c29
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 0%

---


# Revoca delle credenziali {#revoking-machine-credentials}

 Adobe mantiene un CRL per la revoca delle credenziali del computer notoriamente compromesse. L&#39;SDK applica automaticamente questo CRL. Se sono presenti computer aggiuntivi ai quali non si desidera che il server licenze rilasci licenze, è possibile creare un elenco di revoche dei computer e aggiungere il nome dell&#39;emittente e il numero di serie dei token computer che si desidera escludere (utilizzare `MachineToken.getMachineTokenId()` per recuperare il nome dell&#39;emittente e il numero di serie del certificato del computer).

La revoca delle credenziali del computer implica l&#39;utilizzo di un oggetto `RevocationListFactory`. Per creare un elenco di revoche, caricare un elenco di revoche esistente e verificare se un token computer è stato revocato utilizzando l&#39;API Java, eseguire le operazioni seguenti:

1. Configurate l&#39;ambiente di sviluppo e includete tutti i file JAR menzionati in [Impostazione dell&#39;ambiente di sviluppo](../../protecting-content/setting-up-the-sdk/setup-dev-env.md) all&#39;interno del progetto.
1. Creare un&#39;istanza `ServerCredentialFactory` per caricare le credenziali necessarie per la firma. Le credenziali del server licenze vengono utilizzate per firmare l&#39;elenco di revoche.
1. Create un&#39;istanza `RevocationListFactory`.
1. Specificare l&#39;emittente e il numero di serie del token computer da revocare utilizzando un oggetto `IssuerAndSerialNumber`. Tutte  richieste Adobe Primetime DRM contengono un token computer.
1. Creare un oggetto `RevocationList` utilizzando l&#39;oggetto `IssuerAndSerialNumber` appena creato e aggiungerlo all&#39;elenco di revoche trasmettendolo in `RevocationListFactory.addRevocationEntry()`. Generare il nuovo elenco di revoche chiamando `RevocationListFactory.generateRevocationList()`.

1. Per salvare l&#39;elenco di revoche, è possibile serializzarlo chiamando `RevocationList.getBytes()`. Per caricare l’elenco, chiamare `RevocationListFactory.loadRevocationList()` e passare all’elenco serializzato.

1. Verificare che la firma sia valida e che l&#39;elenco sia stato firmato dal server licenze corretto chiamando `RevocationList.verifySignature()`.
1. Per verificare se una voce è stata revocata, passare l&#39;oggetto `IssuerAndSerialNumber` in `RevocationList.isRevoked()`. L&#39;elenco di revoche può anche essere passato in `HandlerConfiguration` affinché l&#39;SDK applichi l&#39;elenco di revoche per tutte le richieste di autenticazione e licenza.

Per aggiungere altre voci a un `RevocationList` esistente, caricare un elenco di revoche esistente. Creare una nuova istanza `RevocationListFactory` e assicurarsi di incrementare il numero CRL. Chiamare `RevocationListFactioryEntries.addRevocationEntries` per aggiungere tutte le voci dal vecchio elenco al nuovo elenco. Chiamare `RevocationListFactory.addRevocationEntry` per aggiungere nuove voci di revoca a RevocationList.

Per un esempio di codice che illustra come creare un elenco di revoche, caricare un elenco di revoche esistente e verificare la revoca di un token computer, vedere `com.adobe.flashaccess.samples.revocation.CreateRevocationList` nella directory Strumenti della riga di comando di implementazione di riferimento [!DNL samples].
