---
title: Rilevamento del ripristino
description: Rilevamento del ripristino
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---


# Rilevamento di rollback{#rollback-detection}

Per il rilevamento del rollback, alcune regole di utilizzo richiedono al client di mantenere le informazioni di stato per l&#39;applicazione dei diritti. Ad esempio, per applicare la regola di utilizzo della finestra di riproduzione, il client memorizza la data e l’ora in cui l’utente ha iniziato a visualizzare il contenuto per la prima volta. Questo evento attiva l&#39;avvio della finestra di riproduzione. Per applicare in modo sicuro la finestra di riproduzione, il server deve assicurarsi che l&#39;utente non esegua il backup e il ripristino dello stato del client, al fine di rimuovere l&#39;ora di avvio della finestra di riproduzione memorizzata sul client. Il server esegue questa operazione monitorando il valore del contatore di rollback del client. Per ogni richiesta, il server ottiene il valore del contatore chiamando `RequestMessageBase.getClientState()` per ottenere l&#39;oggetto `ClientState`, quindi chiamando `ClientState.getCounter()` per ottenere il valore corrente del contatore dello stato client. Il server deve memorizzare questo valore per ogni client (utilizzare `MachineId.getUniqueId()` per identificare il client associato al valore del contatore di rollback), quindi chiamare `ClientState.incrementCounter()` per aumentare il valore del contatore di uno. Se il server rileva che il valore del contatore è inferiore all&#39;ultimo valore rilevato dal server, è possibile che sia stato eseguito il rollback dello stato client. Per ulteriori informazioni sul rilevamento della manomissione dello stato del client, consulta la documentazione di riferimento `ClientState` API .
