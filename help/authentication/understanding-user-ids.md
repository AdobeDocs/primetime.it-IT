---
title: Informazioni sugli ID utente
description: Informazioni sugli ID utente
exl-id: 813a8501-db72-4850-a387-c8db6120db80
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 0%

---

# Informazioni sugli ID utente {#understanding-user-ids}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente di Adobe. Non è consentito alcun uso non autorizzato.

Concettualmente, ogni utente che avvia un flusso di adesione è associato a un singolo ID utente univoco. Tuttavia, attraverso il corso di un flusso di adesione, tale ID utente può essere presentato in modi diversi, a seconda dell’API da cui ottieni l’ID.

Il `sessionGUID` in Short Media Token è la forma sicura dell’ID utente, disponibile tramite `sendTrackingData()` chiamare. In tutte le integrazioni correnti, si tratta di un GUID persistente per l’utente nel tempo e nei dispositivi. L&#39;origine del GUID inizia con l&#39;ID utente della risposta di autenticazione proveniente dall&#39;MVPD. Tuttavia, alcuni MVPD potrebbero cambiare idea in futuro e iniziare a inviare un GUID transitorio. Se un programmatore vuole assicurarsi che l’ID utente sorgente MVPD nella risposta AuthN sia persistente, deve provvedere in tal senso nei suoi accordi con gli MVPD.

Di seguito sono riportati i diversi modi in cui l’ID utente viene rappresentato nelle API di autenticazione di Adobe Primetime:

| Proprietà | Finalità | Hash | Firma digitale | Descrizione |
| --- | --- | --- | --- | --- |
| Proprietà GUID sendTrackingData() | Tracciamento/analisi | Sì | No | : ID utente MVPD, con hash per Adobe. L&#39;ID utente non può essere ricondotto all&#39;origine all&#39;MVPD. </br> </br> - Questo tipo di ID non dispone di firma digitale, pertanto non è sicuro per la prevenzione delle frodi. Tuttavia, è sufficiente per l’analisi.  </br> </br> : questo modulo dell’ID utente viene fornito lato client su tutti gli eventi generati dall’autenticazione Adobe Primetime nel flusso AuthN/AuthZ. |
| Proprietà sessionGUID del token multimediale corto | Tracciamento delle frodi relative all’utilizzo simultaneo | Sì | Sì | : corrisponde all’ID utente tramite sendTrackingData(), tuttavia è dotato di firma digitale per proteggerne l’integrità e può essere utilizzato per il monitoraggio delle frodi. </br> </br> - Deve essere elaborato sul lato server dopo aver utilizzato la libreria di convalida e può essere analizzato per individuare eventuali modelli di frode prima di rilasciare il flusso video al client.  È compito del programmatore eseguire una qualsiasi di queste operazioni. |
| getMetadata(), proprietà userID | Collegamento di account, indagine antifrode con MVPD | No | No | - Questa proprietà consente ad Adobe di esporre l&#39;ID utente MVPD della sorgente effettiva al programmatore. </br> </br> - Nella configurazione di Adobe può essere impostato come crittografato o meno (a seconda della preferenza MVPD). Se crittografato, verrà crittografato con la chiave pubblica del certificato del programmatore fornito ad Adobe, in modo che non venga esposto in modo chiaro al client. </br> </br> - Questo fornisce al programmatore l&#39;ID utente effettivo dall&#39;MVPD, quindi è qualcosa che può essere utilizzato per il collegamento dell&#39;account o per l&#39;indagine antifrode direttamente con l&#39;MVPD. |


**In conclusione**

* In generale, MVPD fornisce un ID univoco persistente <u>e lo trasmette all’Adobe in caso di autenticazione riuscita</u>. Generalmente è coerente su tutte le reti. L’eccezione è Comcast MVPD, che fornisce un ID utente diverso per ogni canale.

* L&#39;ID utente MVPD non contiene dati PII e NON è un numero di account. Non è necessario esporlo in forma crittografata poiché abbiamo verificato con tutti gli MVPD che non viene inviato alcun PII.

La modalità di utilizzo dell’ID utente dipende dal caso d’uso:

* Se ne hai bisogno per il tracciamento/analisi, il punto più pratico è ottenerlo da `sendTrackingData()`.
* Se ne hai bisogno sul lato server per la versione di flusso, la frode o i dati operativi, puoi ottenerli dalla convalida Media Token.
* Se ne hai bisogno per il collegamento dell’account e per frodi più profonde, verifica la disponibilità con il tuo contatto di Adobe.
