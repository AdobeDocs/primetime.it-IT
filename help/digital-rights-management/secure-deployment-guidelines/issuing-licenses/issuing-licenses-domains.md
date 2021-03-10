---
description: Per impedire agli utenti di eseguire il backup e il ripristino dei file per ignorare la deregistrazione del dominio, devi implementare alcuni approcci di gestione del dominio.
title: Gestione dei domini
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---


# Gestione dei domini {#managing-domains}

Per impedire agli utenti di eseguire il backup e il ripristino dei file per ignorare la deregistrazione del dominio, devi implementare alcuni approcci di gestione del dominio.

Di seguito sono riportati alcuni approcci di gestione del dominio:

* Limita il tempo di validità delle credenziali del dominio.

   I client devono contattare il server di dominio per riacquisire le credenziali del dominio alla scadenza delle credenziali. In quel momento, il server di dominio può verificare che il computer sia ancora autorizzato ad essere membro del dominio.
* Passa il puntatore del mouse sulle chiavi di dominio ogni volta che un utente si disinserisce.

   Il server licenze deve rilasciare licenze solo ai client con la chiave di dominio più recente. Questo approccio presuppone che il server licenze possa coordinarsi con il server di dominio per sapere quale chiave è più recente. Se passi il cursore sopra le chiavi di dominio, viene generata una nuova coppia di chiavi per il dominio . Quando passi il cursore sulle chiavi di un dominio, incrementa la versione chiave in `generateDomainCredential`.
* Se il server di dominio è lo stesso del server licenze, il server può utilizzare il contatore di rollback per rilevare un backup e un ripristino.

   Per ulteriori informazioni, consulta [Elaborazione di richieste Adobe Primetime DRM](../../protecting-content/implementing-the-license-server/processing-drm-requests.md).

