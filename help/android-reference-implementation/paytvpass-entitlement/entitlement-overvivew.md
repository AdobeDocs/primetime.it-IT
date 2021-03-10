---
description: Entitlement Manager è il gestore di funzioni che supporta l’implementazione di autenticazione Primetime.
title: Panoramica di Entitlement Manager
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 0%

---


# Panoramica di Entitlement Manager {#entitlement-manager-overview}

Entitlement Manager è il gestore di funzioni che supporta l’implementazione di autenticazione Primetime.

## Panoramica delle funzioni

L’integrazione di autenticazione Primetime con l’implementazione di riferimento dell’SDK di Primetime per Android viene aggiunta una nuova funzionalità manager all’applicazione. Tuttavia, a differenza di molti altri gestori di funzioni, *EntitlementManager viene utilizzato in diverse posizioni in tutta l&#39;applicazione*. Di seguito viene fornita una panoramica delle modifiche e delle aggiunte apportate all’implementazione di riferimento per supportare l’autenticazione Primetime:

### Classe EntitlementManager

La classe `EntitlementManager` gestisce tutte le comunicazioni con l&#39;SDK di autenticazione Primetime, oltre a incapsula la logica dell&#39;applicazione necessaria per i flussi di lavoro di adesione. L&#39;API pubblica di `EntitlementManager` viene utilizzata dall&#39;applicazione per avviare i flussi di lavoro di adesione, mentre l&#39;interfaccia `EntitlementMangerListener` fornisce un meccanismo di callback che consente all&#39;applicazione di gestire gli eventi `EntitlementManger`.

### callback di Entitlement Manager

L’attività principale dell’implementazione di riferimento, il `CatalogActivity`, crea un’istanza di `EntitlementManagerListener` e la registra con il `EntitlementManager`. In questo modo, il `EntitlementManager` potrebbe segnalare gli aggiornamenti dell&#39;interfaccia utente necessari per il resto dell&#39;applicazione. I callback includono la visualizzazione/l’eliminazione di una finestra di dialogo di caricamento, la visualizzazione delle finestre di dialogo di stato, l’aggiornamento delle icone di autorizzazione e autenticazione e l’avvio della riproduzione video dopo l’autorizzazione.

### Finestre di dialogo di adesione

La classe `EntitlementDialogFragment` genera messaggi di dialogo in base allo stato di adesione passato al costruttore di classe. Questa classe viene utilizzata per l’autenticazione dei messaggi di successo e per tutti i messaggi di errore. Il `CatalogActivity` visualizza le finestre di dialogo di adesione quando riceve eventi specifici dal `EntitlementManager`. Inoltre, `CatalogActivity` implementa l&#39;interfaccia `EntitlementDialogListener`, che include metodi di callback per segnalare quando una finestra di dialogo viene chiusa o quando l&#39;utente si disconnette dal servizio di autenticazione Primetime.

### Selezione e accesso del provider di contenuti

Durante l&#39;autenticazione con Primetime, due nuove attività, `MvpdPickerActivity` e `MvpdLoginActivity`, consentono all&#39;utente di selezionare il proprio provider di contenuti e di effettuare l&#39;accesso. Entrambe queste attività sono avviate da `CatalogActivity` tramite `EntitlementManager`. Inoltre, sia i risultati di ritorno `MvpdPickerActivity` che `MvpdLoginActivity` a `CatalogActivity` e quindi a `CatalogActivity` devono sovrascrivere il metodo `Activity.onActivityResult`.

### Pulsante Accedi

L’attività principale dell’implementazione di riferimento, la `CatalogActivity`, include un nuovo pulsante &quot;Accedi&quot; nella barra delle azioni. Il pulsante Accedi consente all’utente di avviare l’autenticazione con l’autenticazione Primetime. Inoltre, l&#39;utente può avviare l&#39;autenticazione selezionando un video protetto per la riproduzione. L&#39;icona e il testo del pulsante Accedi cambiano a seconda dello stato di autenticazione dell&#39;utente e il `CatalogActivity` contiene il codice necessario per aggiornare l&#39;icona e il testo del pulsante quando la pagina viene aggiornata. A questo scopo, all&#39;avvio di `CatalogActivity`, richiama `EntitlementManager.checkAuthentication()` per aggiornare lo stato di autenticazione dell&#39;utente.

### Adesione al contenuto

All’interno di `CatalogView`, vengono visualizzate nuove icone sopra l’icona del contenuto per segnalare lo stato di autorizzazione dell’utente per quel contenuto. Ad esempio, se l’utente è autorizzato a visualizzare un video, sul contenuto viene visualizzata un’icona a forma di cerchio verde. Tuttavia, se l’utente non è autorizzato a visualizzare il video, viene visualizzata un’icona chiave. La visualizzazione di queste icone viene gestita in `ContentTileAdapter`, tuttavia l&#39;aggiornamento del relativo stato viene avviato dal `CatalogActivity` quando viene chiamato un callback nel `EntitlementManagerListener`.

### Riproduzione dei contenuti

La riproduzione video richiede ora un controllo di autorizzazione da parte di `EntitlementManager`. La chiamata a `EntitlementManager.getAuthorization()` si verifica all&#39;interno di `CatalogView`. Se il video richiede un&#39;autorizzazione e l&#39;utente è autorizzato, il percorso `PlayerActivity` viene avviato dal percorso `CatalogActivity`.

