---
seo-title: Opzioni dei criteri di base
title: Opzioni dei criteri di base
uuid: b09543b6-26a7-4e4d-8e8f-866b4bf9cc50
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---


# Opzioni del criterio di base {#basic-policy-options}

Nella tabella seguente sono descritte le preferenze Criteri di base:

| Preferenza | Descrizione |
|---|---|
| Durata criterio | Specifica il periodo di validità del contenuto protetto con questo criterio. |
|  | Inizia da | Le licenze non possono essere utilizzate fino a questa data/ora. |
|  | Fine a | Le licenze non possono essere utilizzate dopo tale data/ora. |
|  | Fine dopo | Specifica il tempo di validità della licenza (in minuti), a partire dal momento in cui viene creato il pacchetto. |
| Memorizzazione delle licenze | Specifica se le licenze possono essere memorizzate nella cache dal client. |
|  |  | Le licenze non possono essere utilizzate dopo tale data/ora. |
|  | Elimina dopo | Specifica il tempo di validità di una licenza (in minuti), a partire dal momento in cui la licenza viene rilasciata dal server licenze. |
|  | Cache indefinitamente | La licenza può essere memorizzata nella cache del client a tempo indeterminato. |
|  | Nessuna memorizzazione delle licenze | La licenza non può essere memorizzata nella cache dal client. È necessario ottenere una nuova licenza dal server ogni volta che l&#39;utente riproduce il contenuto. |
| Autenticazione |  |
|  | Anonimo | Per visualizzare il contenuto non è richiesta alcuna autenticazione. |
|  | Autenticato | Autenticazione nome utente/password obbligatoria. |
| Abilita concatenamento licenze | Consente di aggiornare una licenza utilizzando una licenza principale padre per l&#39;aggiornamento batch delle licenze. Una volta scaduta la licenza foglia, il server potrebbe rilasciare al client una licenza root, che rinnoverà tutto il contenuto protetto con questo criterio. |

