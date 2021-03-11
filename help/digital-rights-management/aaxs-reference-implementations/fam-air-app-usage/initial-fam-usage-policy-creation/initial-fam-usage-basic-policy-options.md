---
title: Opzioni dei criteri di base
description: Opzioni dei criteri di base
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---


# Opzioni dei criteri di base {#basic-policy-options}

Nella tabella seguente sono descritte le preferenze di Criteri di base:

| Preferenza | Descrizione |
|---|---|
| Durata dei criteri | Specifica il periodo di validità del contenuto protetto da questo criterio. |
|  | Inizia da | Le licenze non possono essere utilizzate fino a questa data/ora. |
|  | Fine a | Le licenze non possono essere utilizzate dopo questa data/ora. |
|  | Fine dopo | Specifica il tempo di validità di una licenza (in minuti) a partire dal momento in cui viene imballata. |
| Memorizzazione in cache delle licenze | Specifica se le licenze possono essere memorizzate nella cache del client. |
|  |  | Le licenze non possono essere utilizzate dopo questa data/ora. |
|  | Elimina dopo | Specifica il tempo di validità di una licenza (in minuti) a partire dal momento in cui la licenza viene rilasciata dal server licenze. |
|  | Cache indefinitamente | La licenza può essere memorizzata nella cache del client a tempo indeterminato. |
|  | Nessun caching delle licenze | La licenza non può essere memorizzata nella cache dal client. È necessario ottenere una nuova licenza dal server ogni volta che l’utente riproduce il contenuto. |
| Autenticazione |  |
|  | Anonimo | Per visualizzare il contenuto non è necessaria alcuna autenticazione. |
|  | Autenticato | È richiesta l’autenticazione tramite nome utente/password. |
| Abilita concatenamento licenze | Consente di aggiornare una licenza utilizzando una licenza principale per l&#39;aggiornamento batch delle licenze. Una volta scaduta la licenza foglia, il server può rilasciare al client una licenza root, che rinnoverà tutti i contenuti protetti con questo criterio. |

