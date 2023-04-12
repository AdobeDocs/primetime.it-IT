---
title: Percorso di aggiornamento di AccessEnabler iOS/tvOS 3.7.0
description: Percorso di aggiornamento di AccessEnabler iOS/tvOS 3.7.0
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---


# Percorso di aggiornamento di AccessEnabler iOS/tvOS 3.7.0 {#accessenabler-iostvos-370-upgrade-path}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

</br>

Modifiche allo spazio di archiviazione Keychain [nuova versione di AccessEnabler 3.7.0](/help/authentication/authn-rn-ios-tvos-370.md) sono incompatibili con l&#39;implementazione dell&#39;archiviazione Keychain dalla versione di AccessEnabler inferiore alla 3.7.0.

Il percorso di aggiornamento per un&#39;applicazione che adotta la nuova versione 3.7.0 di AccessEnabler migrerà tutti i token dalle versioni precedenti dello storage Keychain. Pertanto, gli utenti finali **non dovrebbe subire la perdita di sessioni di autenticazione/autorizzazione** durante il processo di aggiornamento del framework di AccessEnabler.

## Limitazioni note

Alcune limitazioni, descritte di seguito, potrebbero essere riscontrate dagli implementatori.


1. L&#39;SSO regolare (Adobe) non funziona tra un&#39;applicazione che utilizza AccessEnabler versione 3.7.0 e un&#39;applicazione che utilizza AccessEnabler versione/e inferiore a 3.7.0, anche per le applicazioni sviluppate dallo stesso fornitore.

   - **Importante:**
      - L&#39;SSO a livello di sistema (Apple) non sarà interessato!
      - L&#39;SSO regolare (Adobe) continuerà a funzionare se entrambe le applicazioni sono sviluppate dallo stesso fornitore e utilizzano le versioni di AccessEnabler inferiori alla 3.7.0!
      - L&#39;SSO regolare (Adobe) funzionerà se entrambe le applicazioni sono sviluppate dallo stesso fornitore e utilizzano AccessEnabler versione 3.7.0!

1. In una situazione in cui si sta eseguendo il downgrade di un&#39;applicazione che utilizza AccessEnabler versione 3.7.0 a una versione inferiore di AccessEnabler, i nuovi token generati non verranno migrati. Pertanto, gli utenti finali potrebbero rilevare la perdita di sessioni di autenticazione/autorizzazione, senza aspettarselo.

   - **Importante:**
      - Gli utenti finali autenticati tramite l&#39;SSO a livello di sistema (Apple) non saranno interessati!
      - Gli utenti finali che erano già autenticati prima dell&#39;aggiornamento alla nuova applicazione utilizzando AccessEnabler versione 3.7.0 non saranno interessati.

1. In una situazione in cui si sta eseguendo il downgrade di un&#39;applicazione che utilizza AccessEnabler versione 3.7.0 a una versione inferiore di AccessEnabler, i token eliminati non verranno riconosciuti. Pertanto, gli utenti finali potrebbero sperimentare la presenza di sessioni di autenticazione/autorizzazione, senza aspettarselo.
