---
title: Panoramica di Roku SSO
description: Informazioni su Roku SSO
exl-id: 77b154bc-c09f-49d4-b1af-cc33bc6dd22b
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---

# Panoramica di Roku SSO {#overview}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente di Adobe. Non è consentito alcun uso non autorizzato.

## Introduzione {#roku-sso-intro}

Questo documento descrive le informazioni necessarie per sfruttare la funzionalità Single Sign-On sui dispositivi Roku. Adobe Primetime Authentication collabora con Roku per migliorare l’esperienza di accesso degli utenti e facilitare l’accesso Single Sign-On tra le applicazioni TV Everywhere per gli abbonati TV.

La soluzione si basa sull’API REST senza client dell’autenticazione Adobe Primetime, pertanto la maggior parte dei programmatori non dovrà aggiornare le proprie applicazioni per beneficiare del Single Sign-On.

## Abilitazione di Roku SSO {#enable-roku-sso}

Roku SSO è abilitato per impostazione predefinita a meno che il programmatore o MVPD non richiedano la disabilitazione dell&#39;SSO.

Ogni programmatore può abilitare/disabilitare SSO sulla piattaforma Roku per integrazioni specifiche.

### Cosa deve fare un programmatore affinché Roku SSO funzioni {#make-roku-sso-work}

Per le applicazioni dei programmatori che implementano l’API REST su dispositivi client, l’SSO Roku funzionerà senza alcuna modifica. Roku OS aggiungerà due intestazioni HTTP su qualsiasi richiesta agli endpoint di autenticazione di Adobe Primetime.

Per le applicazioni dei programmatori che implementano una soluzione Server-to-Server per l’API REST, il programmatore deve contattare il team Roku e richiedere una configurazione in cui queste due intestazioni verranno inviate al proprio dominio su tutti i flussi API.

L’ID dell’abbonato fornito da Roku deve essere utilizzato al posto dell’ID del dispositivo trasmesso dall’applicazione per garantire l’SSO tra applicazioni (e tra dispositivi).

Per informazioni specifiche sul formato delle intestazioni necessarie, contatta il rappresentante del tuo Adobe.

### Possibili problemi {#possible-issues}

I programmatori devono verificare che le loro implementazioni correnti basate sull’API REST senza client di Adobe non impediscano l’SSO della piattaforma Roku. Di seguito è riportato un elenco di possibili problemi e come risolverli.

| Problema | Possibile causa | Soluzioni possibili | |-|-|-| |Nessuna intestazione SSO Roku inviata ad Adobe|Utilizzo di HTTP invece di HTTPS per le chiamate ai domini di autenticazione Adobe Primetime|Utilizzo di HTTPS| Logo MVPD non visualizzato/non aggiornato per i token SSO|L’interfaccia utente si basa sull’archiviazione locale|Le applicazioni devono aggiornare l’interfaccia utente (e l’archiviazione locale, se necessario) dopo aver verificato l’autenticazione| |Disconnessione attivata su AuthZ|Progettazione applicazione|L’applicazione deve essere aggiornata per non eseguire mai la disconnessione dietro le quinte|

## Domande frequenti {#faq}

* **Come funzionerà l&#39;SSO?**

   L’SSO funziona su tutte le applicazioni Programmer basate sull’autenticazione Adobe Primetime su tutti i dispositivi Roku associati allo stesso utente Roku.
Non tutti gli MVPD consentiranno Roku SSO.

* **Verranno modificati i TTL di autenticazione?**

   Il primo token di autenticazione valido verrà utilizzato per l&#39;esecuzione dell&#39;SSO e, in questo caso, tutte le altre applicazioni che verranno autenticate tramite l&#39;SSO utilizzeranno lo stesso TTL fino alla scadenza. Pertanto, quando si passa da un’applicazione all’altra, la seconda applicazione condividerà il TTL della prima applicazione che si autentica.

* **Altre funzionalità di Adobe funzioneranno come prima?**

   Tutte le funzionalità di autenticazione di Primetime funzioneranno come prima.

* **Esiste un processo di consenso/rinuncia del programmatore che trae vantaggio dall’SSO sulla piattaforma Roku?**

   Si tratta di una modifica alla configurazione nel dashboard TVE di Adobe. Ogni programmatore può abilitare/disabilitare SSO sulla piattaforma Roku per integrazioni specifiche.
