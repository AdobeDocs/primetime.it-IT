---
title: Informazioni sugli ID utente
description: Informazioni sugli ID utente
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 0%

---


# Informazioni sugli ID utente {#understanding-user-ids}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

Concettualmente, ogni utente che avvia un flusso di adesione è associato a un singolo ID utente univoco. Tuttavia, nel corso di un flusso di adesione, un ID utente può essere presentato in modi diversi, a seconda dell&#39;API da cui si ottiene l&#39;ID.

La `sessionGUID` nel token per contenuti multimediali brevi è la forma sicura dell’ID utente, disponibile tramite il `sendTrackingData()` chiama. In tutte le integrazioni correnti, si tratta di un GUID permanente per l’utente in più dispositivi e nel tempo. L’origine del GUID inizia con l’ID utente dalla risposta di autenticazione proveniente dall’MVPD. Tuttavia, alcuni MVPD potrebbero cambiare idea in futuro, e iniziare a inviare un GUID transitorio. Se un programmatore vuole garantire che l&#39;ID utente di origine MVPD nella risposta AuthN sia persistente, dovrebbe organizzarlo nei loro accordi con gli MVPD.

Di seguito sono elencati i diversi modi in cui l’ID utente viene rappresentato nelle API di autenticazione di Adobe Primetime:

| Proprietà | Finalità | Hashed | Firma digitale | Descrizione |
| --- | --- | --- | --- | --- |
| sendTrackingData(), proprietà GUID | Tracciamento/analisi | Sì | No | - ID utente MVPD, con hash per Adobe. L&#39;ID utente non è rintracciabile all&#39;origine nel MVPD. </br> </br> - Questo tipo di ID non è firmato digitalmente, quindi non è sicuro per la prevenzione delle frodi. Tuttavia, è sufficiente per l’analisi.  </br> </br> - Questo modulo dell’ID utente viene fornito lato client su tutti gli eventi generati dall’autenticazione Adobe Primetime nel flusso AuthN/AuthZ. |
| Proprietà sessionGUID del token multimediale breve | Tracciamento delle frodi relative all’utilizzo simultaneo | Sì | Sì | - Questo è lo stesso ID utente tramite sendTrackingData(), tuttavia, questo è firmato digitalmente per proteggere la sua integrità ed è sufficientemente buono per essere utilizzato per il tracciamento delle frodi. </br> </br> - Deve essere elaborato sul lato server dopo aver utilizzato la libreria di convalida e può essere analizzato per individuare i pattern di frode prima di rilasciare il flusso video al client.  Eseguire uno di questi compiti è compito del programmatore. |
| getMetadata(), proprietà userID | Collegamento di account, indagine per frode con MVPD | No | No | - Questa proprietà consente ad Adobe di esporre l&#39;ID utente MVPD di origine effettiva al programmatore. </br> </br> - Nella configurazione dell&#39;Adobe può essere impostato come crittografato o meno (a seconda della preferenza MVPD). Se è crittografato, verrà crittografato con la chiave pubblica dal certificato del programmatore fornito all&#39;Adobe, in modo che non venga esposto in modo chiaro al client. </br> </br> - Questo dà al programmatore l&#39;ID utente effettivo dall&#39;MVPD, quindi è qualcosa che può essere utilizzato per il collegamento dell&#39;account o le indagini di frode direttamente con l&#39;MVPD. |


**In conclusione**

* In generale, l&#39;MVPD fornisce un ID univoco persistente <u>e lo trasmette ad Adobe in caso di esito positivo dell&#39;autenticazione</u>. È generalmente coerente in tutte le reti. L&#39;eccezione è Comcast MVPD, che fornisce un ID utente diverso per ogni canale.

* L&#39;ID utente MVPD non contiene PII e NON è un numero di account. Non è necessario esporlo in forma criptata poiché abbiamo convalidato con tutti gli MVPD che non viene inviato alcun PII.

Il modo in cui utilizzi l’ID utente dipende dal caso d’uso:

* Se necessario per il tracciamento/analisi, il posto più pratico è quello di ottenerlo da `sendTrackingData()`.
* Se è necessario sul lato server per la versione del flusso, la frode o i dati operativi, è possibile ottenerlo dal validatore del token multimediale.
* Se ti serve per il collegamento dell&#39;account e la frode più profonda, controlla con il tuo contatto Adobe per la disponibilità.

