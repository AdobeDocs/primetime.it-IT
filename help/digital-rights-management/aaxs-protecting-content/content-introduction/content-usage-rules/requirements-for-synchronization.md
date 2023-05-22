---
title: Requisiti per la sincronizzazione
description: Requisiti per la sincronizzazione
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# Requisiti per la sincronizzazione{#requirements-for-synchronization}

Specifica la frequenza con cui il client sincronizzerà il proprio stato con il server. Se al client è stata rilasciata una licenza out-of-band (senza contattare il server licenze), le regole di utilizzo possono specificare che il client deve inviare messaggi di sincronizzazione al server per sincronizzare l&#39;ora protetta del client e segnalare lo stato del client al server.

Il comportamento di sincronizzazione viene definito utilizzando i seguenti parametri:

* Intervallo di avvio — specifica il tempo di attesa dopo l&#39;ultima sincronizzazione riuscita per avviare un&#39;altra richiesta di sincronizzazione.
* Intervallo di arresto rigido — (facoltativo). Non consentire la riproduzione se la sincronizzazione non ha avuto esito positivo per il periodo di tempo specificato.
* Forza probabilità di sincronizzazione — (facoltativo). Probabilità con cui il client deve inviare un messaggio di sincronizzazione prima del successivo intervallo di avvio.

>[!NOTE]
>
>Questa regola di utilizzo è supportata dai client Adobe Access versione 3.0 e successive. Il comportamento sui client meno recenti dipende dalla versione minima del client supportata dal server licenze. Vedi, [Versione client minima](../../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-minimum-client-version.md).

