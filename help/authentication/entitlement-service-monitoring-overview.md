---
title: Panoramica sul monitoraggio dei servizi di adesione
description: Panoramica sul monitoraggio dei servizi di adesione
exl-id: ebd5d650-0a32-4583-9045-5156356494e2
source-git-commit: 84a16ce775a0aab96ad954997c008b5265e69283
workflow-type: tm+mt
source-wordcount: '1179'
ht-degree: 0%

---

# Panoramica sul monitoraggio dei servizi di adesione {#entitlement-service-monitoring-overview}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente di Adobe. Non è consentito alcun uso non autorizzato.

## Introduzione {#introduction}

I siti e le app TVE devono essere disponibili 24 ore su 24, 7 giorni su 7; pertanto, i clienti devono essere informati in tempo reale sugli eventi di adesione per poter rilevare e correggere i problemi il più rapidamente possibile. Inoltre, devono analizzare i dati mensili per determinare quali piattaforme forniscono la maggior parte del traffico, e quali piattaforme potrebbero avere una cattiva implementazione e tassi di conversione insoddisfacenti.

Entitlement Service Monitoring (ESM) fornisce a programmatori e MVPD un feed di dati che offre visibilità in tempo reale sui loro eventi di autenticazione e autorizzazione. I dati vengono raccolti dai sistemi di autenticazione di Adobe Primetime e forniti tramite un’API RESTful.  I clienti possono utilizzare i dati in modo diretto o dall’interno delle proprie dashboard operative personalizzate.

Gli elementi principali del sistema ESM sono le metriche e le dimensioni. ESM genera rapporti che contengono metriche aggregate in base alla selezione della dimensione. Poiché gli eventi Adobe Pass vengono registrati nel fuso orario PST, i rapporti ESM sono disponibili anche nel fuso orario PST.

L’API ESM non è generalmente disponibile.  Per domande sulla disponibilità, contatta il rappresentante di Adobe.

## ESM per programmatori {#esm-for-programmers}

### I programmatori possono monitorare le metriche seguenti: {#programmers-monitor-metrics}


| *Nome metrica* | *Descrizione* |
|-------------------------|--------------------------|
| authn-try | Numero di flussi di autenticazione avviati |
| author-success | Numero di token di autenticazione ottenuti correttamente dai client |
| in attesa di autenticazione | Numero di token di autenticazione generati correttamente (a prescindere dal fatto che il client lo abbia effettivamente ottenuto o meno) |
| author-failed | Numero di autenticazione non riuscita eseguita tramite un sistema esterno. |
| clientless-tokens | Numero di token senza client emessi correttamente |
| clientless-failures | Numero di tentativi non riusciti di ricevere token dall’API senza client |
| authz-try | Numero di tentativi di autorizzazione |
| autenticazione riuscita | Numero di autorizzazioni riuscite |
| autorizzazione non riuscita | Numero di autorizzazioni negate dagli MVPD a livello di applicazione |
| Autore-rifiutato | Numero di tentativi di autorizzazione considerati dannosi da Adobe Service Provider e rifiutati in seguito alla prevenzione di attacchi DoS |
| autentz-latenza | Numero totale di millisecondi passati sull&#39;endpoint MVPD |
| media-token | Numero di token multimediali brevi generati (assimilati al numero di richieste di riproduzione) |
| account univoci | Numero di utenti univoci che hanno eseguito azioni di adesione (AuthN/AuthZ) nell’intervallo di tempo selezionato. (Questa metrica viene visualizzata solo se sono richiesti valori giornalieri). </br> Questo viene calcolato per ogni singolo centro dati. Quando non è richiesta la dimensione &quot;dc&quot;, questa metrica non viene visualizzata. |
| sessioni univoche | Numero di sessioni univoche che hanno eseguito chiamate del flusso di autenticazione al servizio di autenticazione di Adobe Primetime entro l’intervallo di tempo selezionato. (Questa metrica viene visualizzata solo se sono richiesti valori giornalieri). </br> Questo viene calcolato per ogni singolo centro dati. Quando non è richiesta la dimensione &quot;dc&quot;, questa metrica non viene visualizzata. |
| count | Contatore semplice utilizzato nei rapporti orientati agli eventi |

</br>

### I programmatori possono filtrare le metriche elencate sopra in base alle seguenti dimensioni: {#progr-filter-metrics}


| *Nome Dimension* | *Descrizione* |
|---|---|
| anno | Anno a 4 cifre |
| mese | Il mese dell&#39;anno (1-12) |
| giorno | Il giorno del mese (1-31) |
| ora | L&#39;ora del giorno |
| minuto | Il minuto dell&#39;ora |
| media-company | Società di media proprietaria del sito web che ha avviato il processo di adesione per l’utente |
| dc | (Centro dati) L’area geografica principale in cui è stata ricevuta la richiesta. |
| proxy | Il proxy MVPD (che sarà &quot;Direct&quot; per le integrazioni dirette) |
| mvpd | MVPD responsabile della concessione dell&#39;autorizzazione all&#39;utente |
| requestor-id | ID richiedente utilizzato per eseguire la richiesta di adesione |
| channel | Il sito web del canale, estratto dal campo della risorsa (estratto dal payload MRSS come canale/titolo, se fornito, o mappato al valore della risorsa, se non in formato RSS). |
| resource-id | Titolo effettivo della risorsa coinvolto nella richiesta di autorizzazione (estratto dal payload MRSS come articolo/titolo se fornito) |
| dispositivo | La piattaforma del dispositivo (PC, dispositivi mobili, console, ecc.) |
| eap | Il provider di autenticazione esterno quando il flusso di autenticazione viene eseguito tramite un sistema esterno. </br> I valori possono essere: </br> - N/D: l’autenticazione è stata fornita dall’autenticazione Primetime </br> - Apple: il sistema esterno che ha fornito l’autenticazione è Apple |
| famiglia di sistemi operativi | Sistema operativo in esecuzione sul dispositivo |
| famiglia di browser | Agente utente utilizzato per accedere all’autenticazione di Adobe Primetime |
| cdt | La piattaforma del dispositivo (alternativa), attualmente utilizzata per Clientless. </br>  I valori possono essere: </br> - N/D: l’evento non proviene da un SDK senza client </br> - Sconosciuto - Poiché il parametro deviceType da un’API senza client è facoltativo, esistono chiamate che non contengono alcun valore. </br> : qualsiasi altro valore inviato tramite l’API Clientless, ad esempio xbox, appletv, roku, ecc. </br> |
| platform-version | Versione dell’SDK senza client |
| tipo di sistema operativo | Sistema operativo in esecuzione sul dispositivo, alternativo (non attualmente utilizzato) |
| versione browser | Versione agente utente |
| tipo sdk | L’SDK client utilizzato (Flash, HTML5, Android nativo, iOS, Clientless, ecc.) |
| sdk-version | Versione dell’SDK del client di autenticazione di Adobe Primetime |
| evento | Nome dell’evento di autenticazione Adobe Primetime |
| motivo | Motivo degli errori, segnalato dall’autenticazione di Adobe Primetime |
| sso-type | Il meccanismo SSO sottostante: platform/passive/adobe. Indica che il token di autorizzazione è stato emesso riutilizzando l’AuthN in un’altra applicazione |

## ESM per MVPD {#esm-for-mvpds}

### Gli MVPD possono monitorare le metriche seguenti:

| *Nome della metrica* | *Descrizione* |
|---|---|
| authn-try | Numero di flussi di autenticazione avviati |
| author-success | Numero di token di autenticazione ottenuti correttamente dai client |
| in attesa di autenticazione | Numero di token di autenticazione generati correttamente (a prescindere dal fatto che il client lo abbia effettivamente ottenuto o meno) |
| author-failed | Numero di autenticazione non riuscita eseguita tramite un sistema esterno. |
| authz-try | Numero di tentativi di autorizzazione |
| autenticazione riuscita | Numero di autorizzazioni riuscite |
| autorizzazione non riuscita | Numero di autorizzazioni negate dagli MVPD a livello di applicazione |
| Autore-rifiutato | Numero di tentativi di autorizzazione considerati dannosi da Adobe Service Provider e rifiutati in seguito alla prevenzione di attacchi DoS |
| autentz-latenza | Numero totale di millisecondi passati sull&#39;endpoint MVPD |

### Gli MVPD possono filtrare le metriche elencate in precedenza in base alle seguenti dimensioni:

| *Nome Dimension* | *Descrizione* |
|---|---|
| anno | Anno a 4 cifre |
| mese | Il mese dell&#39;anno (1-12) |
| giorno | Il giorno del mese (1-31) |
| ora | L&#39;ora del giorno |
| minuto | Il minuto dell&#39;ora |
| requestor-id | ID richiedente utilizzato per eseguire la richiesta di adesione |
| eap | Il provider di autenticazione esterno quando il flusso di autenticazione viene eseguito tramite un sistema esterno. </br> I valori possono essere: </br> - N/D: l’autenticazione è stata fornita dall’autenticazione Primetime </br> - Apple: il sistema esterno che ha fornito l’autenticazione è Apple |
| cdt | La piattaforma del dispositivo (alternativa), attualmente utilizzata per Clientless. </br>  I valori possono essere: </br> - N/D: l’evento non proviene da un SDK senza client </br> - Sconosciuto - Poiché il parametro deviceType da un’API senza client è facoltativo, esistono chiamate che non contengono alcun valore. </br> : qualsiasi altro valore inviato tramite l’API Clientless, ad esempio xbox, appletv, roku, ecc. </br> |
| tipo sdk | L’SDK client utilizzato (Flash, HTML5, Android nativo, iOS, Clientless, ecc.) |


## Casi d’uso {#use-cases}

Puoi utilizzare i dati ESM per i seguenti casi d’uso:

- **Monitorare** - I gruppi operativi o di monitoraggio possono creare un dashboard o un grafico che richiama l’API ogni minuto. Utilizzando le informazioni visualizzate, è possibile rilevare un problema (con l’autenticazione Primetime o con un MVPD) nel momento in cui viene visualizzato.

- **Debug/Test di qualità** - Poiché i dati vengono suddivisi anche per piattaforma, dispositivo, browser e sistema operativo, l’analisi dei pattern di utilizzo può individuare problemi relativi a combinazioni specifiche (ad esempio, Safari su OSX).

- **Analytics** - I dati forniti possono essere utilizzati per integrare/controllare i dati lato client raccolti tramite Adobe Analytics o un altro strumento di analisi.

<!--
## Related Information {#related-information}

- [ESM API](/help/authentication/entitlement-service-monitoring-api.md)
- [Degradation API Overview](/help/authentication/degradation-api-overview.md)
- [Server-side Metrics](/help/authentication/understanding-serverside-metrics.md)
-->
