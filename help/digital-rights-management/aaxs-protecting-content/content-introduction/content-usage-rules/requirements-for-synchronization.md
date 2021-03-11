---
title: Requisiti per la sincronizzazione
description: Requisiti per la sincronizzazione
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# Requisiti per la sincronizzazione{#requirements-for-synchronization}

Specifica la frequenza con cui il client sincronizzerà il proprio stato con il server. Se al client è stata rilasciata una licenza fuori banda (senza contattare un server licenze), le regole di utilizzo possono specificare che il client deve inviare messaggi di sincronizzazione al server al fine di sincronizzare l&#39;orario protetto del client e segnalare lo stato del client al server.

Il comportamento di sincronizzazione viene definito utilizzando i seguenti parametri:

* Intervallo iniziale - Specifica il tempo di attesa dopo l&#39;ultima sincronizzazione riuscita per avviare un&#39;altra richiesta di sincronizzazione.
* Intervallo di arresto rigido — (facoltativo). Disabilitare la riproduzione se la sincronizzazione non si è verificata correttamente nel tempo specificato.
* Forza probabilità di sincronizzazione — (facoltativo). Probabilità con cui il client deve inviare un messaggio di sincronizzazione prima dell’intervallo di avvio successivo.

>[!NOTE]
>
>Questa regola di utilizzo è supportata dai client Adobe Access versione 3.0 e successive. Il comportamento dei client meno recenti dipende dalla versione client minima supportata dal server licenze. Vedere [Versione minima del client](../../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-minimum-client-version.md).

