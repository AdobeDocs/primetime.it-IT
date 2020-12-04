---
seo-title: Gestione dei domini
title: Gestione dei domini
uuid: aee02196-8704-46ee-add9-82b371722f0f
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# Gestione dei domini{#managing-domains}

Per evitare che gli utenti possano eseguire il backup e ripristinare i propri file nel tentativo di evitare la deregistrazione del dominio, si consiglia di implementare uno dei seguenti approcci per la gestione del dominio:

* Limita il tempo di validità delle credenziali del dominio. I client dovranno contattare il server del dominio per acquisire nuovamente le credenziali del dominio alla scadenza. In quel momento, il server di dominio può assicurarsi che il computer sia ancora autorizzato a appartenere al dominio.
* Eseguire il rollover delle chiavi di dominio ogni volta che un utente si deregistra. Il server licenze deve rilasciare licenze solo ai client con la chiave di dominio più recente. Ciò presuppone che il server licenze possa coordinarsi con il server di dominio per sapere quale chiave è la più recente. Se si passa il puntatore del mouse sulle chiavi del dominio, verrà generata una nuova coppia di chiavi per il dominio. Quando si passa il puntatore del mouse sulle chiavi di un dominio specifico, assicurarsi di incrementare la versione chiave in `generateDomainCredential`. Per ulteriori informazioni sull&#39;implementazione di un rollover chiave, vedere *RefImplDomainReqHandler* nell&#39;implementazione di riferimento.
* Se il server di dominio è lo stesso del server licenze, il server può utilizzare il contatore di rollback per rilevare il backup e il ripristino. Vedere *Elaborazione delle richieste di accesso al Adobe *in *Utilizzo dell&#39;SDK  accesso al Adobe per la protezione dei contenuti.*

