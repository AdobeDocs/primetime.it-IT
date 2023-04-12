---
title: Panoramica dell’API di degradazione
description: Panoramica dell’API di degradazione
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# Panoramica dell’API di degradazione {#degradation-api-overview}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Informazioni generali {#general_info}

>[!NOTE]
>
>Questa API non è generalmente disponibile. Contatta il tuo rappresentante di Adobe per gli aggiornamenti di disponibilità.

Questa funzione fornisce a tutte le tre parti principali di un&#39;integrazione (programmatori, MVPD e Adobe) la capacità di bypassare temporaneamente specifici endpoint di autenticazione e autorizzazione MVPD. Di solito è il programmatore ad avviare tale azione, ma indipendentemente da chi innesca un evento di degrado, l&#39;azione dipende da accordi precedentemente concordati con gli MVPD interessati.

Il caso d’uso principale di questa funzione si verifica durante eventi sportivi live o di grandi dimensioni. In scenari di traffico così elevato è possibile che il carico su un endpoint MVPD specifico diventi troppo alto, con conseguente tempi di risposta molto lunghi per gli utenti. Al fine di preservare una buona esperienza utente durante tale scenario, il programmatore può decidere di attivare una regola di degrado che può temporaneamente autenticare/autorizzare automaticamente gli utenti, o disabilitare un MVPD rimuovendolo dall&#39;elenco MVPD disponibili.

Una regola di degradazione viene applicata solo per un periodo di tempo fisso. Anche se i clienti principali di questa funzione sono i canali sportivi e i canali di news live, tutti i programmatori potrebbero voler avere accesso a questa funzione, in quanto i servizi MVPD scendono di tanto in tanto.

Note sulla degradazione:

* Questa funzione è progettata per essere utilizzata insieme all’API di monitoraggio dell’utilizzo, che fornisce informazioni in tempo reale sul numero di autenticazioni e autorizzazioni per MVPD, sulla latenza media di autorizzazione e su altre metriche necessarie per una panoramica completa del servizio.
* Questa funzione non consente di bypassare il servizio di autenticazione Adobe Primetim. Se l’autenticazione di Primetime è inattiva, non esiste alcun meccanismo all’interno del servizio che possa essere utilizzato per consentire agli utenti di visualizzare il contenuto. I siti o le app potrebbero, tuttavia, aggirare l&#39;autenticazione Primetime da soli.
* L&#39;Adobe attualmente non attiverà direttamente il degrado: la decisione deve sempre risiedere con un programmatore specifico che ha accettato tali condizioni con gli MVPD. In futuro, l&#39;autenticazione Primetime potrebbe essere proattiva nell&#39;attivare le regole di degradazione se è possibile raggiungere accordi (protezione SLA) con MVPD.

<!--
## Related Information {#related}

- [ESM API](/help/authentication/entitlement-service-monitoring-api.md)
- [Server-side Metrics](/help/authentication/understanding-serverside-metrics.md)
-->