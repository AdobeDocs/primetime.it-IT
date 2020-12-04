---
seo-title: Utilizzo di identificatori di computer
title: Utilizzo di identificatori di computer
uuid: 2832c158-fade-4bbf-ae89-f95ce9dfc369
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---


# Utilizzo di identificatori macchina{#using-machine-identifiers}

Tutte  richieste di accesso al Adobe (ad eccezione delle richieste che supportano la compatibilità FMRMS) contengono informazioni sul token computer rilasciato al client durante l&#39;individualizzazione. Il token del computer contiene un ID computer, un identificatore assegnato durante l&#39;individualizzazione. Utilizzate questo identificatore per contare il numero di computer da cui un utente ha richiesto una licenza o ha aderito a un dominio.

Esistono due modi per utilizzare l&#39;identificatore. Il metodo `getUniqueId()` restituisce una stringa assegnata al dispositivo durante l&#39;individualizzazione. È possibile memorizzare le stringhe in un database e cercare per identificatore. Tuttavia, questo identificatore cambierà se l&#39;utente riformatta il disco rigido e si individualizza di nuovo. Questo identificatore avrà anche un valore diverso tra  Adobe® AIR® e  Adobe® Flash Player in diversi browser sullo stesso computer.

Per contare più accuratamente i computer, è possibile utilizzare `getBytes()` per memorizzare l&#39;intero identificatore. Per determinare se il computer è stato visto in precedenza, ottenere tutti gli identificatori per un nome utente e chiamare `matches()` per verificare se esiste una corrispondenza. Poiché il metodo `matches()` deve essere utilizzato per confrontare i valori restituiti da `MachineId.getBytes`, questa opzione è pratica solo se è presente un numero limitato di valori da confrontare (ad esempio, i computer associati a un utente specifico).
