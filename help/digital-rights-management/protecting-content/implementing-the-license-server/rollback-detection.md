---
seo-title: Rilevamento del rollback
title: Rilevamento del rollback
uuid: ec124bac-a1d7-45be-bf09-a99d5eec5042
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---


# Rilevamento del rollback {#rollback-detection}

Per il rilevamento del rollback, alcune regole di utilizzo richiedono al client di mantenere le informazioni di stato per l&#39;applicazione dei diritti. Ad esempio, per applicare la regola di utilizzo della finestra di riproduzione, il client memorizza la data e l&#39;ora in cui l&#39;utente ha iniziato a visualizzare il contenuto per la prima volta. Questo evento attiva l&#39;avvio della finestra di riproduzione. Per applicare in modo sicuro la finestra di riproduzione, il server deve assicurarsi che l&#39;utente non effettui il backup e ripristini lo stato del client per rimuovere l&#39;ora di inizio della finestra di riproduzione memorizzata sul client. Il server esegue questa operazione monitorando il valore del contatore di rollback del client.

Per ogni richiesta, il server ottiene il valore del contatore chiamando `RequestMessageBase.getClientState()` per ottenere l&#39;oggetto `ClientState`, quindi chiamando `ClientState.getCounter()` per ottenere il valore corrente del contatore di stato del client. Il server deve memorizzare questo valore per ciascun client (utilizzare `MachineId.getUniqueId()` per identificare il client associato al valore del contatore di rollback), quindi chiamare `ClientState.incrementCounter()` per aumentare il valore del contatore di uno. Se il server rileva che il valore del contatore è inferiore all&#39;ultimo valore visualizzato dal server, è possibile che sia stato eseguito il rollback dello stato del client.

Per ulteriori informazioni sul rilevamento delle manomissioni da parte del client, consultate la documentazione di riferimento delle API `ClientState`.
