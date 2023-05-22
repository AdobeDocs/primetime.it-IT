---
title: Rilevamento rollback
description: Rilevamento rollback
copied-description: true
exl-id: 054d3634-5ce9-4a51-ac91-e6ae60a1fd6e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---

# Rilevamento rollback {#rollback-detection}

Se l’implementazione di Adobe Access utilizza regole aziendali che richiedono al client di mantenere lo stato (ad esempio, l’intervallo di intervallo della finestra di riproduzione), Adobe consiglia vivamente al server di tenere traccia del contatore di rollback e di utilizzare l’elenco Consentiti di AIR o SWF.

Il contatore di rollback viene inviato al server nella maggior parte delle richieste provenienti dal client. Se l’implementazione di Adobe Access non richiede il contatore di rollback, questo può essere ignorato. In caso contrario, Adobe consiglia che il server memorizzi l’ID macchina casuale, ottenuto utilizzando `MachineToken.getMachineId().getUniqueId()`- e il valore del contatore corrente in un database. Per ulteriori informazioni sull&#39;incremento e il tracciamento del contatore di rollback, vedere ClientState in *Riferimento API per l’accesso agli Adobi* e *Rilevamento rollback* in *Utilizzo dell’SDK per l’accesso agli Adobi per la protezione dei contenuti*.
