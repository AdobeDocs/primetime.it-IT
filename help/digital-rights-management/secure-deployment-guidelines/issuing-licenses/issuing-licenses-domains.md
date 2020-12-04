---
description: Per impedire agli utenti di eseguire il backup e il ripristino dei file per evitare la deregistrazione del dominio, è necessario implementare alcuni approcci di gestione del dominio.
seo-description: Per impedire agli utenti di eseguire il backup e il ripristino dei file per evitare la deregistrazione del dominio, è necessario implementare alcuni approcci di gestione del dominio.
seo-title: Gestione dei domini
title: Gestione dei domini
uuid: 30b73e38-d6ed-43c6-89ba-ae8616383779
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---


# Gestione dei domini {#managing-domains}

Per impedire agli utenti di eseguire il backup e il ripristino dei file per evitare la deregistrazione del dominio, è necessario implementare alcuni approcci di gestione del dominio.

Di seguito sono riportati alcuni approcci di gestione del dominio:

* Limita il tempo di validità delle credenziali del dominio.

   I client devono contattare il server del dominio per riacquisire le credenziali del dominio alla scadenza delle credenziali. In quel momento, il server di dominio può verificare che il computer sia ancora autorizzato a appartenere al dominio.
* Passate il puntatore del mouse sulle chiavi del dominio ogni volta che un utente si registra.

   Il server licenze deve rilasciare licenze solo ai client con la chiave di dominio più recente. Questo approccio presuppone che il server licenze possa coordinarsi con il server di dominio per sapere quale chiave è più recente. Se si passa il puntatore del mouse sulle chiavi del dominio, verrà generata una nuova coppia di chiavi per il dominio. Quando passi il cursore sopra le chiavi di un dominio, incrementa la versione chiave in `generateDomainCredential`.
* Se il server di dominio è lo stesso del server licenze, il server può utilizzare il contatore di rollback per rilevare un backup e un ripristino.

   Per ulteriori informazioni, vedere [Elaborazione  richieste Adobe Primetime DRM](../../protecting-content/implementing-the-license-server/processing-drm-requests.md).

