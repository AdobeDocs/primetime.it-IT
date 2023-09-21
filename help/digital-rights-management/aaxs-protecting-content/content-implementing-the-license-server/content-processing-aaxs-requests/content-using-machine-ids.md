---
title: Utilizzo degli identificatori macchina
description: Utilizzo degli identificatori macchina
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# Utilizzo degli identificatori macchina{#using-machine-identifiers}

Tutte le richieste di accesso Adobe (ad eccezione delle richieste che supportano la compatibilità FMRMS) contengono informazioni sul token del computer rilasciato al client durante l’individualizzazione. Il token del computer contiene un ID computer, un identificatore assegnato durante l’individualizzazione. Utilizzare questo identificatore per contare il numero di computer da cui un utente ha richiesto una licenza o è entrato a far parte di un dominio.

Esistono due modi per utilizzare l’identificatore. Il `getUniqueId()` Il metodo restituisce una stringa assegnata al dispositivo durante l&#39;individualizzazione. È possibile memorizzare le stringhe in un database e cercare per identificatore. Tuttavia, questo identificatore cambierà se l&#39;utente riformatta il disco rigido e individualizza nuovamente. Questo identificatore avrà anche un valore diverso tra Adobe® AIR® e Adobe® Flash® Player in browser diversi sullo stesso computer.

Per contare più accuratamente le macchine, è possibile utilizzare `getBytes()` per memorizzare l&#39;intero identificatore. Per determinare se il computer è già stato visto in precedenza, ottieni tutti gli identificatori per un nome utente e una chiamata `matches()` per verificare eventuali corrispondenze. Perché il `matches()` deve essere utilizzato per confrontare i valori restituiti da `MachineId.getBytes`, questa opzione è utile solo quando è presente un numero limitato di valori da confrontare (ad esempio, i computer associati a un utente specifico).
