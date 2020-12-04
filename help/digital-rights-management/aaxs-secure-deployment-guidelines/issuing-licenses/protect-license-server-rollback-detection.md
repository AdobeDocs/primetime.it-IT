---
seo-title: Rilevamento del rollback
title: Rilevamento del rollback
uuid: fc80c98f-7ee5-414b-87fe-0dbb8d4f6019
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---


# Rilevamento del rollback {#rollback-detection}

Se &#39;implementazione di Access Adobe utilizza regole aziendali che richiedono al client di mantenere lo stato (ad esempio, l&#39;intervallo della finestra di riproduzione),  Adobe consiglia vivamente al server di tenere traccia del contatore di rollback e di utilizzare AIR o SWF per consentire l&#39;elencazione.

Il contatore di rollback viene inviato al server nella maggior parte delle richieste dal client. Se l&#39;implementazione di  Accesso Adobe non richiede il contatore di rollback, può essere ignorata. In caso contrario,  Adobe consiglia al server di memorizzare l&#39;ID computer casuale, ottenuto utilizzando `MachineToken.getMachineId().getUniqueId()`, e il valore del contatore corrente in un database. Per ulteriori informazioni sull&#39;incremento e il tracciamento del contatore di rollback, vedere ClientState in *Riferimento API di accesso al Adobe* e *Rilevamento del rollback* in *Utilizzo dell&#39;SDK di accesso al Adobe  per la protezione dei contenuti*.
