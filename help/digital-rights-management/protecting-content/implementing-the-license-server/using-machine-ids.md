---
title: Utilizzare gli identificatori macchina
description: Utilizzare gli identificatori macchina
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---


# Usa identificatori macchina{#use-machine-identifiers}

Tutte le richieste Adobe Primetime DRM (ad eccezione delle richieste che supportano la compatibilità FMRMS) includono informazioni sul token computer che è stato rilasciato al client durante l’individualizzazione. Il token del computer include un ID computer, che è un identificatore assegnato durante l&#39;individualizzazione. È possibile utilizzare questo identificatore per contare il numero di computer da cui un utente ha richiesto una licenza o è entrato in un dominio.

È possibile utilizzare un identificatore come segue:

* Il metodo `getUniqueId()` restituisce una stringa che è stata assegnata a un dispositivo durante l&#39;individualizzazione. È possibile memorizzare le stringhe in un database e cercare per identificatore. Tuttavia, questo identificatore cambia se l&#39;utente riformatta il disco rigido e si individualizza di nuovo. Questo identificatore ha anche un valore diverso tra Adobe AIR e Adobe Flash Player in diversi browser sullo stesso computer.
* Se si desidera contare più accuratamente le macchine, è possibile utilizzare `getBytes()` per memorizzare l&#39;intero identificatore. Per determinare se il computer è stato visto in precedenza, ottieni tutti gli identificatori per un nome utente e chiama `matches()` per verificare se esiste una corrispondenza. Poiché il metodo `matches()` deve essere utilizzato per confrontare i valori restituiti da `MachineId.getBytes`, questa opzione è pratica solo quando vi sono pochi valori da confrontare; ad esempio, i computer associati a un utente specifico.

