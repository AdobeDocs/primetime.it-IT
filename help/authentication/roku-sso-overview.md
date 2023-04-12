---
title: Panoramica di Roku SSO
description: Informazioni su Roku SSO
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---


# Panoramica di Roku SSO {#overview}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Introduzione {#roku-sso-intro}

Questo documento descrive le informazioni necessarie per sfruttare la funzionalità Single Sign-On sui dispositivi Roku. Adobe Primetime Authentication collabora con Roku per migliorare l&#39;esperienza utente di accesso e per facilitare l&#39;accesso Single Sign-On tra le applicazioni TV Everywhere per gli abbonati TV.

La soluzione si basa sull’API REST Clientless di Adobe Primetime Authentication, pertanto la maggior parte dei programmatori non dovrà aggiornare le proprie applicazioni per beneficiare del Single Sign-On.

## Abilitazione di Roku SSO {#enable-roku-sso}

Roku SSO è abilitato per impostazione predefinita a meno che il programmatore o MVPD non richiedano la disattivazione dell&#39;SSO.

Ogni programmatore può attivare/disattivare SSO sulla piattaforma Roku per integrazioni specifiche.

### Cosa dovrebbe fare un programmatore per Roku SSO lavorare {#make-roku-sso-work}

Per le applicazioni dei programmatori che implementano l&#39;API REST sui dispositivi client, l&#39;SSO Roku funzionerà senza alcuna modifica. Roku OS aggiungerà due intestazioni HTTP su qualsiasi richiesta agli endpoint di autenticazione di Adobe Primetime.

Per le applicazioni dei programmatori che implementano una soluzione Server to Server per API REST , il programmatore deve contattare il team Roku e chiedere una configurazione in cui queste due intestazioni verranno inviate al loro dominio su tutti i flussi api.

L’ID utente iscritto fornito da Roku deve essere utilizzato al posto di qualsiasi ID dispositivo passato dall’applicazione per garantire l’accesso SSO tra più applicazioni (e tra dispositivi).

Per informazioni specifiche sul formato delle intestazioni necessarie, contatta il tuo rappresentante di Adobe.

### Problemi possibili {#possible-issues}

I programmatori dovrebbero verificare che le loro implementazioni attuali basate sull’API REST Clientless di Adobe non ostacolino la piattaforma-SSO di Roku. Di seguito è riportato un elenco dei possibili problemi e di come dovrebbero essere risolti.

| Problema | Possibile causa | Soluzioni possibili | |-|-|-| |Nessuna intestazione Roku SSO inviata ad Adobe|Utilizzo di HTTP invece di HTTPS per le chiamate ai domini di autenticazione Adobe Primetime|Usa HTTPS| |Logo MVPD non visualizzato / non aggiornato per i token SSO|L&#39;interfaccia utente si basa sull&#39;archiviazione locale|Le applicazioni devono aggiornare l&#39;interfaccia utente (e l&#39;archiviazione locale, se necessario) dopo aver controllato l&#39;autenticazione| |Disconnessione attivata su AuthZ|Progettazione applicazioni|L&#39;applicazione deve essere aggiornata per non eseguire mai il logout dietro le quinte|

## Domande frequenti {#faq}

* **Come funzionerà l&#39;SSO?**

   SSO funzionerà su tutte le applicazioni Programmatore fornite dall&#39;autenticazione Adobe Primetime su tutti i dispositivi Roku associati allo stesso utente Roku.
Non tutti gli MVPD permetteranno Roku SSO.

* **Verrà apportata una modifica ai TTL di autenticazione?**

   Il primo token di autenticazione valido verrà utilizzato per l&#39;esecuzione di SSO e, in questo caso, tutte le altre applicazioni che saranno autenticate tramite SSO utilizzeranno lo stesso TTL fino alla scadenza. Quindi, quando si passa da un&#39;applicazione all&#39;altra, la seconda applicazione condividerà il TTL della prima applicazione che esegue l&#39;autenticazione.

* **Altre funzionalità di Adobe funzioneranno come prima?**

   Tutte le funzionalità di autenticazione di Primetime funzioneranno come prima.

* **Esiste un processo di consenso/rinuncia del programmatore che beneficia di SSO sulla piattaforma Roku?**

   Si tratta di una modifica alla configurazione nel dashboard TVE di Adobe. Ogni programmatore può attivare/disattivare SSO sulla piattaforma Roku per integrazioni specifiche.
