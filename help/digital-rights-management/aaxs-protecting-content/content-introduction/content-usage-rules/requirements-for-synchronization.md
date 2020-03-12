---
seo-title: Requisiti per la sincronizzazione
title: Requisiti per la sincronizzazione
uuid: 976a0ae1-bece-437e-b95b-6cd222525d13
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Requisiti per la sincronizzazione{#requirements-for-synchronization}

Specifica la frequenza con cui il client sincronizzerà il proprio stato con il server. Se al client è stata rilasciata una licenza fuori banda (senza contattare un server licenze), le regole di utilizzo potrebbero specificare che il client deve inviare messaggi di sincronizzazione al server al fine di sincronizzare l&#39;ora protetta del client e lo stato del client del report al server.

Il comportamento di sincronizzazione è definito utilizzando i seguenti parametri:

* Intervallo iniziale — Specifica quanto tempo attendere dopo l’ultima sincronizzazione per avviare un’altra richiesta di sincronizzazione.
* Intervallo di arresto rigido — (Facoltativo). Disattiva la riproduzione se la sincronizzazione non ha avuto esito positivo nel tempo specificato.
* Forza probabilità di sincronizzazione — (Facoltativo). Probabilità con cui il client deve inviare un messaggio di sincronizzazione prima del successivo intervallo di inizio.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Questa regola di utilizzo è supportata dai client Adobe Access versione 3.0 e successive. Il comportamento dei client meno recenti dipende dalla versione client minima supportata dal server licenze. Vedere, Versione [client](../../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-minimum-client-version.md)minima.

