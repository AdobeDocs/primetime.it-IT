---
title: Gestione dei domini
description: Gestione dei domini
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# Gestione dei domini{#managing-domains}

Per evitare che gli utenti possano eseguire il backup e il ripristino dei propri file nel tentativo di bypassare la deregistrazione del dominio, si consiglia di implementare uno dei seguenti approcci per la gestione del dominio:

* Limita il tempo di validità delle credenziali del dominio. I client dovranno contattare il server di dominio per riacquisire le credenziali del dominio quando scadono. In quel momento, il server di dominio può garantire che il computer sia ancora autorizzato a essere membro del dominio.
* Esegui il rollover delle chiavi di dominio ogni volta che un utente si disregistra. Il server licenze deve rilasciare licenze solo ai client con la chiave di dominio più recente. Ciò presuppone che il server licenze possa coordinarsi con il server di dominio per sapere quale chiave è più recente. Se passi il cursore sopra le chiavi di dominio, viene generata una nuova coppia di chiavi per il dominio . Quando passi il cursore sulle chiavi di un determinato dominio, assicurati di incrementare la versione chiave in `generateDomainCredential`. Per ulteriori informazioni sull&#39;implementazione di un rollover chiave, consulta *RefImplDomainReqHandler* nell&#39;implementazione di riferimento.
* Se il server di dominio è lo stesso del server licenze, il server può utilizzare il contatore di rollback per rilevare il backup e il ripristino. Consulta *Elaborazione delle richieste di accesso agli Adobi *in *Utilizzo dell&#39;SDK per l&#39;accesso agli Adobi per la protezione dei contenuti.*

