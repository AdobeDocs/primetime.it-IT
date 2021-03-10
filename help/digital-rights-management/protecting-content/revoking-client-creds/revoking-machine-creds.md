---
title: Revoca delle credenziali del computer
description: Revoca delle credenziali del computer
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 0%

---


# Revoca delle credenziali della macchina {#revoking-machine-credentials}

In Adobe viene conservato un CRL per la revoca delle credenziali del computer notoriamente compromesse. Questo CRL viene applicato automaticamente dall’SDK. Se esistono altri computer a cui non si desidera che il server licenze rilasci licenze, è possibile creare un elenco di revoche dei computer e aggiungere il nome dell&#39;emittente e il numero di serie dei token computer che si desidera escludere (utilizzare `MachineToken.getMachineTokenId()` per recuperare il nome dell&#39;emittente e il numero di serie del certificato del computer).

La revoca delle credenziali del computer comporta l&#39;utilizzo di un oggetto `RevocationListFactory`. Per creare un elenco di revoche, caricare un elenco di revoche esistente e verificare se un token computer è stato revocato utilizzando l&#39;API Java, eseguire le operazioni seguenti:

1. Configura l&#39;ambiente di sviluppo e includi tutti i file JAR menzionati in [Impostazione dell&#39;ambiente di sviluppo](../../protecting-content/setting-up-the-sdk/setup-dev-env.md) all&#39;interno del progetto.
1. Crea un&#39;istanza `ServerCredentialFactory` per caricare le credenziali necessarie per la firma. Le credenziali del server licenze vengono utilizzate per firmare l&#39;elenco di revoche.
1. Crea un&#39;istanza `RevocationListFactory`.
1. Specificare l&#39;emittente e il numero di serie del token computer da revocare utilizzando un oggetto `IssuerAndSerialNumber`. Tutte le richieste Adobe Primetime DRM contengono un token computer.
1. Creare un oggetto `RevocationList` utilizzando l&#39;oggetto `IssuerAndSerialNumber` appena creato e aggiungerlo all&#39;elenco di revoche passandolo a `RevocationListFactory.addRevocationEntry()`. Generare il nuovo elenco di revoche chiamando `RevocationListFactory.generateRevocationList()`.

1. Per salvare l&#39;elenco di revoche, è possibile serializzarlo chiamando `RevocationList.getBytes()`. Per caricare l’elenco, chiama `RevocationListFactory.loadRevocationList()` e passa l’elenco serializzato.

1. Verificare che la firma sia valida e che l&#39;elenco sia stato firmato dal server di licenza corretto chiamando `RevocationList.verifySignature()`.
1. Per verificare se una voce è stata revocata, passa l&#39;oggetto `IssuerAndSerialNumber` in `RevocationList.isRevoked()`. L’elenco di revoche può anche essere trasmesso in `HandlerConfiguration` affinché l’SDK faccia rispettare l’elenco di revoche per tutte le richieste di autenticazione e licenza.

Per aggiungere altre voci a un `RevocationList` esistente, caricare un elenco di revoche esistente. Crea una nuova istanza `RevocationListFactory` e assicurati di incrementare il numero dell&#39;elenco di conformità. Invoca `RevocationListFactioryEntries.addRevocationEntries` per aggiungere tutte le voci del vecchio elenco al nuovo elenco. Chiamare `RevocationListFactory.addRevocationEntry` per aggiungere nuove voci di revoca all&#39;elenco di revoca.

Per un esempio di codice che illustra come creare un elenco di revoche, caricare un elenco di revoche esistente e verificare se un token computer è stato revocato, vedere `com.adobe.flashaccess.samples.revocation.CreateRevocationList` nella directory Strumenti della riga di comando per l&#39;implementazione di riferimento [!DNL samples].
