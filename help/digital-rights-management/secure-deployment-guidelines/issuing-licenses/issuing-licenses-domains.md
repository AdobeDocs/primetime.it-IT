---
description: Per evitare che gli utenti eseguano il backup e il ripristino dei file per ignorare l'annullamento della registrazione del dominio, è necessario implementare alcuni approcci di gestione del dominio.
title: Gestione dei domini
exl-id: cbf745d2-ba6e-4144-9608-23870bdfe16d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# Gestione dei domini {#managing-domains}

Per evitare che gli utenti eseguano il backup e il ripristino dei file per ignorare l&#39;annullamento della registrazione del dominio, è necessario implementare alcuni approcci di gestione del dominio.

Di seguito sono riportati alcuni approcci di gestione dei domini:

* Limita il tempo di validità delle credenziali del dominio.

   I client devono contattare il server di dominio per acquisire nuovamente le credenziali del dominio alla scadenza delle credenziali. In tale momento, il server di dominio può verificare che il computer sia ancora autorizzato a essere membro del dominio.
* Esegui il rollover delle chiavi di dominio ogni volta che un utente annulla la registrazione.

   Il server licenze deve rilasciare licenze solo ai client che dispongono della chiave di dominio più recente. Questo approccio presuppone che il server licenze possa coordinarsi con il server di dominio per sapere quale chiave è la più recente. Il passaggio al dominio delle chiavi comporta la generazione di una nuova coppia di chiavi per il dominio. Quando passi il cursore sui tasti di un dominio, incrementa la versione della chiave in `generateDomainCredential`.
* Se il server di dominio è uguale al server licenze, il server può utilizzare il contatore di rollback per rilevare un backup e un ripristino.

   Per ulteriori informazioni, consulta [Elaborazione delle richieste Adobe Primetime DRM](../../protecting-content/implementing-the-license-server/processing-drm-requests.md).
