---
title: Requisiti per la sincronizzazione
description: Requisiti per la sincronizzazione
copied-description: true
exl-id: 0368e363-893f-4b51-a317-00791d0ab54f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---

# Requisiti per la sincronizzazione {#requirements-for-synchronization}

I requisiti per la sincronizzazione specificano la frequenza con cui il client sincronizza il proprio stato con il server. Se al client è stata rilasciata una licenza out-of-band (senza contattare il server licenze), le regole di utilizzo possono specificare che il client deve inviare messaggi di sincronizzazione al server per sincronizzare l&#39;ora sicura del client e segnalare lo stato del client al server.

Il comportamento di sincronizzazione viene definito utilizzando i seguenti parametri:

* **Intervallo di inizio** - Specifica il tempo di attesa dopo l&#39;ultima sincronizzazione riuscita per avviare un&#39;altra richiesta di sincronizzazione.
* **Intervallo di arresto rigido** - (facoltativo). Non consentire la riproduzione se la sincronizzazione non ha avuto esito positivo per il periodo di tempo specificato.
* **Forza probabilità di sincronizzazione** - (facoltativo). Probabilità con cui il client deve inviare un messaggio di sincronizzazione prima del successivo intervallo di avvio.

>[!NOTE]
>
>Questa regola di utilizzo è supportata dai client DRM Primetime versione 3.0 o successiva. Il comportamento sui client meno recenti dipende dalla versione minima del client supportata dal server licenze.
