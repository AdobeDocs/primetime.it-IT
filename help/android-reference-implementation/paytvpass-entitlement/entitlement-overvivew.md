---
description: Entitlement Manager è il gestore di funzioni che supporta l'implementazione dell'autenticazione Primetime.
seo-description: Entitlement Manager è il gestore di funzioni che supporta l'implementazione dell'autenticazione Primetime.
seo-title: Panoramica di Entitlement Manager
title: Panoramica di Entitlement Manager
uuid: b33dfae3-a132-4215-9992-80cbf4c87a61
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---


# Panoramica di Entitlement Manager {#entitlement-manager-overview}

Entitlement Manager è il gestore di funzioni che supporta l&#39;implementazione dell&#39;autenticazione Primetime.

## Panoramica delle funzioni

L&#39;integrazione dell&#39;autenticazione Primetime con l&#39;implementazione di riferimento dell&#39;SDK di Android Primetime aggiunge all&#39;applicazione un nuovo gestore di funzioni. Tuttavia, a differenza di molti altri gestori di funzioni, *EntitlementManager viene utilizzato in diverse aree dell&#39;applicazione*. Di seguito viene fornita una panoramica delle modifiche e delle aggiunte apportate all&#39;implementazione di riferimento per supportare l&#39;autenticazione Primetime:

### EntitlementManager, classe

La classe `EntitlementManager` gestisce tutte le comunicazioni con l&#39;SDK dell&#39;autenticazione Primetime, oltre a racchiudere la logica dell&#39;applicazione necessaria per i flussi di lavoro di adesione. L&#39;API pubblica di `EntitlementManager` viene utilizzata dall&#39;applicazione per avviare flussi di lavoro di adesione, mentre l&#39;interfaccia `EntitlementMangerListener` fornisce un meccanismo di callback che consente all&#39;applicazione di gestire gli eventi `EntitlementManger`.

### Callback di EntitlementManager

L&#39;attività principale dell&#39;implementazione di riferimento, la `CatalogActivity`, crea un&#39;istanza di `EntitlementManagerListener` e la registra con la `EntitlementManager`. In questo modo, `EntitlementManager` potrebbe segnalare gli aggiornamenti dell&#39;interfaccia utente necessari per il resto dell&#39;applicazione. Le callback includono la visualizzazione/disattivazione di una finestra di dialogo di caricamento, la visualizzazione di finestre di dialogo di stato, l’aggiornamento delle icone di autorizzazione e autenticazione e l’avvio della riproduzione video dopo l’esito positivo dell’autorizzazione.

### Finestre Di Dialogo Di Adesione

La classe `EntitlementDialogFragment` genera messaggi di dialogo basati sullo stato di adesione passato al costruttore di classe. Questa classe viene utilizzata per i messaggi di successo dell&#39;autenticazione e per tutti i messaggi di errore. La `CatalogActivity` visualizza le finestre di dialogo di adesione quando riceve eventi specifici dalla `EntitlementManager`. Inoltre, l&#39; `CatalogActivity` implementa l&#39;interfaccia `EntitlementDialogListener`, che include metodi di callback per segnalare quando una finestra di dialogo viene chiusa o quando l&#39;utente si disconnette dal servizio di autenticazione Primetime.

### Selezione e login del fornitore di contenuti

Durante l&#39;autenticazione con l&#39;autenticazione Primetime, due nuove attività, `MvpdPickerActivity` e `MvpdLoginActivity`, consentono all&#39;utente di selezionare il proprio provider di contenuti e di effettuare il login. Entrambe queste attività sono iniziate dalla `CatalogActivity` tramite la `EntitlementManager`. Inoltre, sia i risultati `MvpdPickerActivity` che `MvpdLoginActivity` restituiscono i risultati a `CatalogActivity`, e quindi `CatalogActivity` devono sovrascrivere il metodo `Activity.onActivityResult`.

### Accedi, pulsante

L&#39;attività principale dell&#39;implementazione di riferimento, la `CatalogActivity`, include un nuovo pulsante &quot;Accedi&quot; nella barra delle azioni. Il pulsante Accedi consente all&#39;utente di avviare l&#39;autenticazione con l&#39;autenticazione Primetime. Inoltre, l&#39;utente può avviare l&#39;autenticazione selezionando un video protetto per la riproduzione. L&#39;icona e il testo del pulsante Accedi cambiano a seconda dello stato di autenticazione dell&#39;utente, e il `CatalogActivity` contiene il codice per aggiornare l&#39;icona e il testo del pulsante quando la pagina viene aggiornata. A questo scopo, all&#39;avvio di `CatalogActivity`, chiama `EntitlementManager.checkAuthentication()` per aggiornare lo stato di autenticazione dell&#39;utente.

### Adesione contenuto

All&#39;interno di `CatalogView`, vengono visualizzate nuove icone sopra l&#39;icona del contenuto per segnalare lo stato di autorizzazione dell&#39;utente per quel contenuto. Ad esempio, se l’utente è già autorizzato a visualizzare un video, sul contenuto viene visualizzata un’icona a forma di cerchio verde. Tuttavia, se l’utente non è autorizzato a visualizzare il video, viene visualizzata un’icona a forma di chiave. La visualizzazione di queste icone viene gestita in `ContentTileAdapter`, tuttavia l&#39;aggiornamento del relativo stato viene avviato da `CatalogActivity` quando viene chiamato un callback in `EntitlementManagerListener`.

### Riproduzione dei contenuti

La riproduzione video ora richiede un controllo di autorizzazione da parte di `EntitlementManager`. La chiamata a `EntitlementManager.getAuthorization()` si verifica all&#39;interno di `CatalogView`. Se il video richiede l&#39;autorizzazione e l&#39;utente è autorizzato, la `PlayerActivity` viene avviata dalla `CatalogActivity`.

