---
title: Revoca delle credenziali del computer
description: Revoca delle credenziali del computer
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 0%

---

# Revoca delle credenziali del computer{#revoking-machine-credentials}

L&#39;Adobe mantiene un CRL per la revoca delle credenziali del computer notoriamente compromesse. Questo CRL viene applicato automaticamente dall’SDK. Se sono presenti altri computer per i quali non si desidera che il server licenze rilasci licenze, è possibile creare un elenco di revoche di computer e aggiungere il nome dell&#39;autorità emittente e il numero di serie dei token di computer che si desidera escludere (utilizzare `MachineToken.getMachineTokenId()` per recuperare il nome dell&#39;emittente e il numero di serie del certificato del computer).

La revoca delle credenziali del computer comporta l&#39;utilizzo di un `RevocationListFactory` oggetto. Per creare un elenco di revoche, caricare un elenco di revoche esistente e verificare se un token computer è stato revocato utilizzando l’API Java, effettua le seguenti operazioni:

1. Configura l’ambiente di sviluppo e includi tutti i file JAR menzionati in [Configurazione dell’ambiente di sviluppo](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) all’interno del progetto.
1. Creare un `ServerCredentialFactory` per caricare le credenziali necessarie per la firma. Le credenziali del server licenze vengono utilizzate per firmare l&#39;elenco di revoche.
1. Creare un `RevocationListFactory` dell&#39;istanza.
1. Specificare l&#39;autorità emittente e il numero di serie del token del computer da revocare utilizzando un `IssuerAndSerialNumber` oggetto. Tutte le richieste di accesso Adobe contengono un token computer.
1. Creare un `RevocationList` oggetto utilizzando `IssuerAndSerialNumber` l&#39;oggetto appena creato e aggiungerlo all&#39;elenco di revoche trasmettendolo in `RevocationListFactory.addRevocationEntry()`. Genera il nuovo elenco di revoche chiamando `RevocationListFactory.generateRevocationList()`.
1. Per salvare l&#39;elenco di revoche, è possibile serializzarlo chiamando `RevocationList.getBytes()`. Per caricare l’elenco, chiama `RevocationListFactory.loadRevocationList()` e passa nell’elenco serializzato.
1. Verificare che la firma sia valida e che l&#39;elenco sia stato firmato dal server licenze corretto chiamando `RevocationList.verifySignature()`.
1. Per verificare se una voce è stata revocata, passare il `IssuerAndSerialNumber` oggetto in `RevocationList.isRevoked()`. L’elenco di revoca può anche essere trasmesso in `HandlerConfiguration` affinché l’SDK applichi l’elenco di revoche per tutte le richieste di autenticazione e licenza.

Per aggiungere altre voci a un elemento esistente `RevocationList`, carica un elenco di revoche esistente. Crea un nuovo `RevocationListFactory` e assicurati di incrementare il numero CRL. Chiamata `RevocationListFactioryEntries.addRevocationEntries` per aggiungere al nuovo elenco tutte le voci del vecchio elenco. Chiamata `RevocationListFactory.addRevocationEntry` per aggiungere nuove voci di revoca all&#39;elenco di revoche.

Per un codice di esempio che illustra come creare un elenco di revoche, caricare un elenco di revoche esistente e verificare se un token computer è stato revocato, vedere `com.adobe.flashaccess.samples.revocation.CreateRevocationList` nella directory &quot;samples&quot; degli strumenti della riga di comando per l’implementazione di riferimento.
