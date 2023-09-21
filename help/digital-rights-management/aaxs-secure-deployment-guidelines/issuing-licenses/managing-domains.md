---
title: Gestione dei domini
description: Gestione dei domini
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# Gestione dei domini{#managing-domains}

Per evitare che gli utenti possano eseguire il backup e il ripristino dei file senza annullare la registrazione del dominio, si consiglia di implementare uno dei seguenti approcci per la gestione del dominio:

* Limita il tempo di validità delle credenziali del dominio. I client dovranno contattare il server di dominio per acquisire nuovamente le credenziali del dominio alla scadenza. In tale momento, il server di dominio può garantire che il computer sia ancora autorizzato a essere membro del dominio.
* Esegui il rollover delle chiavi di dominio ogni volta che un utente annulla la registrazione. Il server licenze deve rilasciare licenze solo ai client che dispongono della chiave di dominio più recente. Ciò presuppone che il server licenze possa coordinarsi con il server di dominio per sapere quale chiave è la più recente. Il passaggio al dominio delle chiavi comporta la generazione di una nuova coppia di chiavi per il dominio. Quando passi il mouse sui tasti di un determinato dominio, accertati di incrementare la versione della chiave in `generateDomainCredential`. Per ulteriori informazioni sull’implementazione di un rollover della chiave, consulta *RefImplDomainReqHandler* nell’implementazione di riferimento.
* Se il server di dominio è uguale al server licenze, il server può utilizzare il contatore di rollback per rilevare il backup e il ripristino. Consulta *Elaborazione delle richieste di accesso di Adobe *in *Utilizzo dell’SDK di accesso di Adobe per proteggere il contenuto.*
