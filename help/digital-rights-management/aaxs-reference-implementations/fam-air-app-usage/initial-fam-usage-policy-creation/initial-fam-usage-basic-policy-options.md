---
title: Opzioni di base dei criteri
description: Opzioni di base dei criteri
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Opzioni di base dei criteri {#basic-policy-options}

Nella tabella seguente vengono descritte le preferenze dei criteri di base:

| Preferenza | Descrizione |
|---|---|
| Durata criterio | Specifica il periodo di validità del contenuto protetto con questo criterio. |
|  | Inizia da | Le licenze non possono essere utilizzate fino a questa data/ora. |
|  | Termina a | Le licenze non possono essere utilizzate dopo questa data/ora. |
|  | Termina dopo | Specifica la durata di validità (in minuti) di una licenza, a partire dal momento in cui viene compilata. |
| Caching delle licenze | Specifica se le licenze possono essere memorizzate nella cache dal client. |
|  | | Le licenze non possono essere utilizzate dopo questa data/ora. |
|  | Elimina dopo | Specifica la durata di validità (in minuti) di una licenza, a partire dal momento in cui la licenza viene rilasciata dal server licenze. |
|  | Memorizza nella cache a tempo indefinito | La licenza può essere memorizzata nella cache del client a tempo indeterminato. |
|  | Nessuna memorizzazione nella cache delle licenze | La licenza non può essere memorizzata nella cache dal client. È necessario ottenere una nuova licenza dal server ogni volta che l’utente riproduce il contenuto. |
| Autenticazione | |
|  | Anonimo | Non è richiesta alcuna autenticazione per visualizzare il contenuto. |
|  | Autenticato | È richiesta l&#39;autenticazione nome utente/password. |
| Abilita concatenamento licenze | Consente di aggiornare una licenza utilizzando una licenza radice padre per l&#39;aggiornamento in batch delle licenze. Una volta scaduta la licenza foglia, il server può rilasciare al client una licenza root, che rinnoverà tutto il contenuto protetto con questo criterio. |
