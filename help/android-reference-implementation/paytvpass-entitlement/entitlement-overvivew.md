---
description: Gestione diritti è il gestore delle funzioni che supporta l’implementazione dell’autenticazione Primetime.
title: Panoramica di Gestione diritti
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 0%

---

# Panoramica di Gestione diritti {#entitlement-manager-overview}

Gestione diritti è il gestore delle funzioni che supporta l’implementazione dell’autenticazione Primetime.

## Panoramica delle funzioni

L’integrazione dell’autenticazione Primetime con l’implementazione di riferimento dell’SDK per Android Primetime aggiunge una nuova funzione di gestione all’applicazione. Tuttavia, a differenza di molti altri gestori di funzionalità, *EntitlementManager viene utilizzato in diverse aree dell&#39;applicazione*. Di seguito viene fornita una panoramica delle modifiche e delle aggiunte apportate all’implementazione di riferimento per supportare l’autenticazione Primetime:

### Classe EntitlementManager

Il `EntitlementManager` La classe gestisce tutte le comunicazioni con l’SDK di autenticazione Primetime e incapsula la logica dell’applicazione necessaria per i flussi di lavoro di adesione. Il `EntitlementManager`L’API pubblica di viene utilizzata dall’applicazione per avviare flussi di lavoro di adesione, mentre `EntitlementMangerListener` fornisce un meccanismo di callback che l&#39;applicazione può gestire `EntitlementManger` eventi.

### Callback di EntitlementManager

L’attività principale dell’implementazione di riferimento, `CatalogActivity`, crea un&#39;istanza di `EntitlementManagerListener` e la registra con `EntitlementManager`. In questo modo, `EntitlementManager` potrebbe segnalare aggiornamenti dell’interfaccia utente necessari al resto dell’applicazione. I callback includono la visualizzazione o l’eliminazione di una finestra di dialogo di caricamento, la visualizzazione di finestre di dialogo di stato, l’aggiornamento delle icone di autorizzazione e autenticazione e l’avvio della riproduzione video in caso di autorizzazione riuscita.

### Finestre di dialogo diritti

Il `EntitlementDialogFragment` class genera messaggi di dialogo in base allo stato di adesione passato al costruttore di classe. Questa classe viene utilizzata per i messaggi di successo dell’autenticazione e per tutti i messaggi di errore. Il `CatalogActivity` visualizza le finestre di dialogo di adesione quando riceve eventi specifici dal `EntitlementManager`. Inoltre, la `CatalogActivity` implementa `EntitlementDialogListener` che include metodi di callback da segnalare quando una finestra di dialogo viene chiusa o quando l’utente si disconnette dal servizio di autenticazione di Primetime.

### Selezione e accesso al provider di contenuti

Durante l’autenticazione con l’autenticazione Primetime, due nuove attività: `MvpdPickerActivity` e `MvpdLoginActivity`, consente all’utente di selezionare il proprio provider di contenuti e di effettuare l’accesso. Entrambe queste attività sono avviate dal `CatalogActivity` tramite `EntitlementManager`. Inoltre, entrambi i `MvpdPickerActivity` e `MvpdLoginActivity` restituisce i risultati al `CatalogActivity` e pertanto `CatalogActivity` deve ignorare `Activity.onActivityResult` metodo.

### Pulsante Accedi

L’attività principale dell’implementazione di riferimento, `CatalogActivity`, include un nuovo pulsante &quot;Accedi&quot; nella barra delle azioni. Il pulsante Accedi consente all’utente di avviare l’autenticazione con l’autenticazione Primetime. Inoltre, l’utente può avviare l’autenticazione selezionando un video protetto per la riproduzione. L&#39;icona e il testo del pulsante Accedi cambiano a seconda dello stato di autenticazione dell&#39;utente e del `CatalogActivity` contiene codice per aggiornare l’icona e il testo del pulsante quando la pagina viene aggiornata. Per eseguire questa operazione, quando `CatalogActivity` inizia, chiama `EntitlementManager.checkAuthentication()` per aggiornare lo stato di autenticazione dell&#39;utente.

### Adesione al contenuto

All&#39;interno del `CatalogView`, le nuove icone vengono visualizzate sopra l’icona del contenuto per segnalare lo stato di autorizzazione dell’utente per quel contenuto. Ad esempio, se l’utente è autorizzato a visualizzare un video, sopra il contenuto viene visualizzata un’icona verde con un cerchio. Tuttavia, se l’utente non è autorizzato a visualizzare il video, viene visualizzata un’icona a forma di chiave. La visualizzazione di queste icone viene gestita in `ContentTileAdapter`, tuttavia, l&#39;aggiornamento del loro stato è avviato dal `CatalogActivity` quando un callback in `EntitlementManagerListener` viene chiamato.

### Riproduzione dei contenuti

La riproduzione di un video richiede un controllo di autorizzazione da parte di `EntitlementManager`. La chiamata a `EntitlementManager.getAuthorization()` si verifica in `CatalogView`. Se il video richiede l’autorizzazione e l’utente è autorizzato, il `PlayerActivity` inizia da `CatalogActivity`.
