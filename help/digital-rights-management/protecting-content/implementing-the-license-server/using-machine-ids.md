---
title: Usa identificatori macchina
description: Usa identificatori macchina
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---


# Usa identificatori macchina{#use-machine-identifiers}

Tutte le richieste DRM di Adobe Primetime (ad eccezione delle richieste che supportano la compatibilità FMRMS) includono informazioni sul token del computer rilasciato al client durante l’individualizzazione. Il token del computer include un ID computer, che è un identificatore assegnato durante l’individualizzazione. È possibile utilizzare questo identificatore per contare il numero di computer da cui un utente ha richiesto una licenza o è entrato in un dominio.

Puoi utilizzare un identificatore come segue:

* Il `getUniqueId()` Il metodo restituisce una stringa assegnata a un dispositivo durante l&#39;individualizzazione. È possibile memorizzare le stringhe in un database e cercare per identificatore. Tuttavia, questo identificatore cambia se l&#39;utente riformatta il disco rigido e individualizza nuovamente. Questo identificatore ha anche un valore diverso tra Adobe AIR e il Flash Player Adobe in browser diversi sulla stessa macchina.
* Se si desidera contare con maggiore precisione i macchinari, è possibile utilizzare `getBytes()` per memorizzare l&#39;intero identificatore. Per determinare se il computer è già stato visto in precedenza, ottieni tutti gli identificatori per un nome utente e una chiamata `matches()` per verificare eventuali corrispondenze. Perché il `matches()` per confrontare i valori restituiti da è necessario utilizzare il metodo `MachineId.getBytes`, questa opzione è utile solo quando è presente un numero limitato di valori da confrontare, ad esempio i computer associati a un utente specifico.

