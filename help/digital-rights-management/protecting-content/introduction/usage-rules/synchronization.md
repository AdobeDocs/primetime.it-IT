---
description: 'null'
seo-description: 'null'
seo-title: Requisiti per la sincronizzazione
title: Requisiti per la sincronizzazione
uuid: 594a4bb2-c042-4485-9cae-73b8f9f93d82
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# Requisiti per la sincronizzazione {#requirements-for-synchronization}

I requisiti per la sincronizzazione specificano la frequenza con cui il client sincronizza il proprio stato con il server. Se al client è stata rilasciata una licenza fuori banda (senza contattare un server licenze), le regole di utilizzo potrebbero specificare che il client deve inviare messaggi di sincronizzazione al server per sincronizzare l&#39;ora protetta del client e segnalare lo stato del client al server.

Il comportamento di sincronizzazione è definito utilizzando i seguenti parametri:

* **Intervallo** di inizio - Specifica per quanto tempo attendere dopo l’ultima sincronizzazione per avviare un’altra richiesta di sincronizzazione.
* **Intervallo** di arresto rigido - (facoltativo). Disattiva la riproduzione se la sincronizzazione non ha avuto esito positivo nel tempo specificato.
* **Forza probabilità** sincronizzazione - (facoltativo). Probabilità con cui il client deve inviare un messaggio di sincronizzazione prima del successivo intervallo di inizio.

>[!NOTE]
>
>Questa regola di utilizzo è supportata dai client DRM Primetime versione 3.0 o successiva. Il comportamento dei client meno recenti dipende dalla versione client minima supportata dal server licenze.

