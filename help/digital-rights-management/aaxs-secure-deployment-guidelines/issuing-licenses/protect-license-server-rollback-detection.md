---
title: Rilevamento del ripristino
description: Rilevamento del ripristino
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---


# Rilevamento di ripristino {#rollback-detection}

Se l&#39;implementazione di Adobe Access utilizza regole aziendali che richiedono al client di mantenere lo stato (ad esempio, l&#39;intervallo della finestra di riproduzione), l&#39;Adobe consiglia vivamente al server di tenere traccia del contatore di rollback e utilizzare AIR o SWF per l&#39;inserimento nell&#39;elenco Consentiti.

Il contatore di rollback viene inviato al server nella maggior parte delle richieste dal client. Se l&#39;implementazione di Adobe Access non richiede il contatore di rollback, può essere ignorata. In caso contrario, Adobe consiglia al server di memorizzare l&#39;ID computer casuale, ottenuto utilizzando `MachineToken.getMachineId().getUniqueId()`, e il valore del contatore corrente in un database. Per ulteriori informazioni sull&#39;incremento e il tracciamento del contatore di rollback, consulta ClientState in *Riferimento API di accesso agli Adobi* e *Rilevamento di rollback* in *Utilizzo dell&#39;SDK di accesso agli Adobi per la protezione dei contenuti*.
