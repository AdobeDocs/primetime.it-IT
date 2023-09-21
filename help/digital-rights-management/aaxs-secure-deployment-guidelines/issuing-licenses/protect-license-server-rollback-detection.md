---
title: Rilevamento rollback
description: Rilevamento rollback
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---

# Rilevamento rollback {#rollback-detection}

Se l’implementazione di Adobe Access utilizza regole aziendali che richiedono al client di mantenere lo stato (ad esempio, l’intervallo di intervallo della finestra di riproduzione), Adobe consiglia vivamente al server di tenere traccia del contatore di rollback e di utilizzare l’elenco Consentiti di AIR o SWF.

Il contatore di rollback viene inviato al server nella maggior parte delle richieste provenienti dal client. Se l’implementazione di Adobe Access non richiede il contatore di rollback, questo può essere ignorato. In caso contrario, Adobe consiglia che il server memorizzi l’ID macchina casuale, ottenuto utilizzando `MachineToken.getMachineId().getUniqueId()`- e il valore del contatore corrente in un database. Per ulteriori informazioni sull&#39;incremento e il tracciamento del contatore di rollback, vedere ClientState in *Riferimento API per l’accesso agli Adobi* e *Rilevamento rollback* in *Utilizzo dell’SDK per l’accesso agli Adobi per la protezione dei contenuti*.
