---
title: Rilevamento rollback
description: Rilevamento rollback
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# Rilevamento rollback{#rollback-detection}

Per il rilevamento del rollback, alcune regole di utilizzo richiedono al client di mantenere le informazioni sullo stato per l&#39;applicazione dei diritti. Ad esempio, per applicare la regola di utilizzo della finestra di riproduzione, il client memorizza la data e l’ora in cui l’utente ha iniziato a visualizzare il contenuto per la prima volta. Questo evento attiva l’inizio della finestra di riproduzione. Per applicare in modo sicuro la finestra di riproduzione, il server deve assicurarsi che l&#39;utente non esegua il backup e ripristini lo stato del client per rimuovere l&#39;ora di inizio della finestra di riproduzione memorizzata sul client. Il server esegue questa operazione tenendo traccia del valore del contatore di rollback del client. Per ogni richiesta, il server ottiene il valore del contatore chiamando `RequestMessageBase.getClientState()` per ottenere `ClientState` oggetto, quindi chiamata `ClientState.getCounter()` per ottenere il valore corrente del contatore stato client. Il server deve memorizzare questo valore per ogni client (utilizzare `MachineId.getUniqueId()` per identificare il client associato al valore del contatore di rollback), quindi chiamare `ClientState.incrementCounter()` per aumentare di uno il valore del contatore. Se il server rileva che il valore del contatore è minore dell&#39;ultimo valore visualizzato dal server, è possibile che sia stato eseguito il rollback dello stato del client. Per ulteriori informazioni sul rilevamento di manomissioni dello stato del client, vedere `ClientState` Documentazione di riferimento API.
