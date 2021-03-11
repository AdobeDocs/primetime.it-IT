---
title: Uso degli identificatori macchina
description: Uso degli identificatori macchina
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---


# Uso degli identificatori macchina{#using-machine-identifiers}

Tutte le richieste di accesso di Adobe (ad eccezione delle richieste che supportano la compatibilità FMRMS) contengono informazioni sul token macchina rilasciato al client durante l&#39;individualizzazione. Il token del computer contiene un ID computer, un identificatore assegnato durante l&#39;individualizzazione. Utilizzare questo identificatore per contare il numero di computer da cui un utente ha richiesto una licenza o è entrato in un dominio.

L’identificatore può essere utilizzato in due modi. Il metodo `getUniqueId()` restituisce una stringa assegnata al dispositivo durante l&#39;individualizzazione. È possibile memorizzare le stringhe in un database e cercare per identificatore. Tuttavia, questo identificatore cambierà se l&#39;utente riformatta il disco rigido e si individualizza nuovamente. Questo identificatore avrà anche un valore diverso tra Adobe® AIR® e Adobe® Flash® Player in diversi browser sullo stesso computer.

Per contare più accuratamente le macchine, è possibile utilizzare `getBytes()` per memorizzare l&#39;intero identificatore. Per determinare se il computer è stato visto in precedenza, ottieni tutti gli identificatori per un nome utente e chiama `matches()` per verificare se esiste una corrispondenza. Poiché il metodo `matches()` deve essere utilizzato per confrontare i valori restituiti da `MachineId.getBytes`, questa opzione è pratica solo quando vi sono pochi valori da confrontare (ad esempio, i computer associati a un particolare utente).
