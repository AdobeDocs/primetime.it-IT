---
seo-title: Utilizzare gli identificatori del computer
title: Utilizzare gli identificatori del computer
uuid: 14eee414-62f1-4a9d-84bd-689ca2271d19
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Utilizzare gli identificatori del computer{#use-machine-identifiers}

Tutte le richieste DRM di Adobe Primetime (ad eccezione delle richieste che supportano la compatibilità FMRMS) includono informazioni sul token computer che è stato rilasciato al client durante l&#39;individualizzazione. Il token del computer include un ID computer, che è un identificatore assegnato durante l&#39;individualizzazione. Potete utilizzare questo identificatore per contare il numero di computer da cui un utente ha richiesto una licenza o ha aderito a un dominio.

Potete usare un identificatore come segue:

* Il `getUniqueId()` metodo restituisce una stringa che è stata assegnata a un dispositivo durante l&#39;individualizzazione. È possibile memorizzare le stringhe in un database e cercare per identificatore. Tuttavia, questo identificatore viene modificato se l&#39;utente riformatta il disco rigido e lo individua di nuovo. Questo identificatore ha anche un valore diverso tra Adobe AIR e Adobe Flash Player in diversi browser sullo stesso computer.
* Se si desidera contare più accuratamente i computer, è possibile utilizzare `getBytes()` per memorizzare l&#39;intero identificatore. Per determinare se il computer è stato visto in precedenza, ottenere tutti gli identificatori per un nome utente e chiamare `matches()` per verificare se esiste una corrispondenza. Poiché il `matches()` metodo deve essere utilizzato per confrontare i valori restituiti da `MachineId.getBytes`, questa opzione è pratica solo se vi è un numero limitato di valori da confrontare; ad esempio, i computer associati a un utente specifico.

