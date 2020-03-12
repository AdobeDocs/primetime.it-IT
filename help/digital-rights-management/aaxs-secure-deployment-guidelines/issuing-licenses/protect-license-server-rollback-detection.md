---
seo-title: Rilevamento del rollback
title: Rilevamento del rollback
uuid: fc80c98f-7ee5-414b-87fe-0dbb8d4f6019
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Rilevamento del rollback{#rollback-detection}

Se l&#39;implementazione di Adobe Access utilizza regole aziendali che richiedono al client di mantenere lo stato (ad esempio, l&#39;intervallo della finestra di riproduzione), Adobe consiglia vivamente al server di tenere traccia del contatore di rollback e di utilizzare la whitelist AIR o SWF.

Il contatore di rollback viene inviato al server nella maggior parte delle richieste dal client. Se l&#39;implementazione di Adobe Access non richiede il contatore di rollback, può essere ignorata. In caso contrario, Adobe consiglia al server di memorizzare l&#39;ID computer casuale ottenuto utilizzando `MachineToken.getMachineId().getUniqueId()`e il valore del contatore corrente in un database. Per ulteriori informazioni sull&#39;incremento e il tracciamento del contatore di rollback, vedi ClientState in *Adobe Access API Reference* and *Rollback detection* in *Utilizzo di Adobe Access SDK per la protezione del contenuto*.
