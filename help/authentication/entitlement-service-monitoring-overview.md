---
title: Panoramica sul monitoraggio del servizio di adesione
description: Panoramica sul monitoraggio del servizio di adesione
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1179'
ht-degree: 0%

---


# Panoramica sul monitoraggio del servizio di adesione {#entitlement-service-monitoring-overview}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Introduzione {#introduction}

I siti e le app TVE devono essere disponibili 24 ore su 24, 7 giorni su 7, per consentire ai clienti di accedere in tempo reale agli eventi di adesione per rilevare e correggere i problemi il più rapidamente possibile. Devono anche analizzare i dati mensili per determinare quali piattaforme stanno fornendo la maggior parte del traffico, e quali piattaforme potrebbero avere una cattiva implementazione e tassi di conversione scarsi.

Il monitoraggio del servizio di abilitazione (ESM) fornisce a programmatori e MVPD un feed di dati che offre visibilità in tempo reale nei loro eventi di autenticazione e autorizzazione. I dati vengono raccolti dai sistemi di autenticazione Adobe Primetime e forniti tramite un’API RESTful.  I clienti possono utilizzare i dati in modo diretto o direttamente dalle proprie dashboard operative personalizzate.

Gli elementi principali del sistema ESM sono le sue metriche e dimensioni. ESM genera rapporti che contengono metriche aggregate in base alla selezione delle dimensioni. Poiché gli eventi Adobe Pass vengono registrati nel fuso orario PST, i rapporti ESM sono disponibili anche nel fuso orario PST. 

L’API ESM non è generalmente disponibile.  Per domande sulla disponibilità, contatta il tuo rappresentante Adobe.

## ESM per programmatori {#esm-for-programmers}

### I programmatori possono monitorare le metriche seguenti: {#programmers-monitor-metrics}


| *Nome delle metriche* | *Descrizione* |
|-------------------------|--------------------------|
| tentativi di authoring | Numero di flussi di autenticazione avviati |
| authoring | Numero di token di autenticazione ottenuti dai client |
| in sospeso | Numero di token di autenticazione generati correttamente (senza tenere conto del fatto che il client lo abbia effettivamente ottenuto) |
| errore di autenticazione | Numero di autenticazioni non riuscite eseguite tramite un sistema esterno. |
| token senza client | Numero di token senza client emessi |
| fallimenti senza client | Numero di tentativi non riusciti di ricevere token dall’API Clientless |
| tentativi di autenticazione | Numero di autorizzazioni tentate |
| authz riuscito | Numero di autorizzazioni riuscite |
| authz-failed | Numero di autorizzazioni negate da MVPD a livello di applicazione |
| authz rifiutato | Numero di tentativi di autorizzazione considerati dannosi da Adobe Service Provider e rifiutati a seguito di una prevenzione degli attacchi DoS |
| authz-latency | Numero totale di millisecondi trascorsi sull&#39;endpoint MVPD |
| media-token | Numero di token multimediali brevi generati (che si assimilano al numero di richieste di riproduzione) |
| account univoci | Numero di utenti univoci che hanno eseguito azioni di adesione (AuthN / AuthZ) nell&#39;intervallo di tempo selezionato. Questa metrica verrà visualizzata solo se sono richiesti valori giornalieri. </br> Viene calcolato per ogni singolo centro dati. Quando la dimensione &quot;dc&quot; non è richiesta, questa metrica non verrà visualizzata. |
| sessioni uniche | Numero di sessioni univoche che hanno eseguito chiamate al flusso di autenticazione al servizio di autenticazione di Adobe Primetime entro l&#39;intervallo di tempo selezionato. Questa metrica verrà visualizzata solo se sono richiesti valori giornalieri. </br> Viene calcolato per ogni singolo centro dati. Quando la dimensione &quot;dc&quot; non è richiesta, questa metrica non verrà visualizzata. |
| count | Un semplice contatore utilizzato nei report orientati agli eventi |

</br>

### I programmatori possono filtrare le metriche elencate sopra per le seguenti dimensioni: {#progr-filter-metrics}


| *Nome Dimension* | *Descrizione* |
|---|---|
| anno | L&#39;anno a 4 cifre |
| mese | Il mese dell&#39;anno (1-12) |
| giorno | Il giorno del mese (1-31) |
| ora | Ora del giorno |
| minuto | Il minuto dell&#39;ora |
| media company | Società di media proprietaria del sito web che ha avviato il processo di adesione per l&#39;utente |
| dc | (Centro dati) L&#39;area principale in cui è stata ricevuta la richiesta. |
| proxy | Il proxy MVPD (che sarà &quot;Diretto&quot; per le integrazioni dirette) |
| mvpd | MVPD responsabile della concessione del diritto all&#39;utente |
| requestor-id | ID richiedente utilizzato per eseguire la richiesta di adesione |
| canale | Il sito web del canale, estratto dal campo della risorsa (estratto dal payload MRSS come canale/titolo se fornito, o mappato al valore della risorsa se non è in formato RSS). |
| resource-id | Titolo della risorsa effettiva coinvolta nella richiesta di autorizzazione (estratto dal payload MRSS come elemento/titolo, se fornito) |
| dispositivo | La piattaforma del dispositivo (PC, mobile, console, ecc.) |
| eap | Provider di autenticazione esterno quando il flusso di autenticazione viene eseguito tramite un sistema esterno. </br> I valori possono essere: </br> - N/D - l&#39;autenticazione è stata fornita da Primetime Authentication </br> - Apple - il sistema esterno che ha fornito l’autenticazione è Apple |
| os-family | Sistema operativo in esecuzione sul dispositivo |
| famiglia di browser | Agente utente utilizzato per accedere all’autenticazione Adobe Primetime |
| cdt | La piattaforma dispositivo (alternativa), attualmente utilizzata per Clientless. </br>  I valori possono essere: </br> - N/D - l’evento non è nato da un SDK Clientless </br> - Sconosciuto - Poiché il parametro deviceType di un&#39;API Clientless è facoltativo, ci sono chiamate che non contengono alcun valore. </br> - qualsiasi altro valore inviato tramite l’API Clientless, ad esempio xbox, appletv, roku ecc. </br> |
| versione piattaforma | Versione dell’SDK senza client |
| tipo os | Sistema operativo in esecuzione sul dispositivo, alternativo (non attualmente utilizzato) |
| versione browser | Versione agente utente |
| tipo sdk | L’SDK client utilizzato (Flash, HTML5, nativo Android, iOS, Clientless, ecc.) |
| versione sdk | Versione dell’SDK del client di autenticazione Adobe Primetime |
| event | Nome dell’evento di autenticazione Adobe Primetime |
| motivo | Motivo degli errori, come segnalato dall’autenticazione Adobe Primetime |
| tipo sso | Il meccanismo SSO sottostante: platform/passive/adobe. Indica che il token di autorizzazione è stato emesso riutilizzando AuthN in un&#39;applicazione diversa |

## ESM per gli MVPD {#esm-for-mvpds}

### Gli MVPD possono monitorare le metriche seguenti:

| *Nome della metrica* | *Descrizione* |
|---|---|
| tentativi di authoring | Numero di flussi di autenticazione avviati |
| authoring | Numero di token di autenticazione ottenuti dai client |
| in sospeso | Numero di token di autenticazione generati correttamente (senza tenere conto del fatto che il client lo abbia effettivamente ottenuto) |
| errore di autenticazione | Numero di autenticazioni non riuscite eseguite tramite un sistema esterno. |
| tentativi di autenticazione | Numero di autorizzazioni tentate |
| authz riuscito | Numero di autorizzazioni riuscite |
| authz-failed | Numero di autorizzazioni negate da MVPD a livello di applicazione |
| authz rifiutato | Numero di tentativi di autorizzazione considerati dannosi da Adobe Service Provider e rifiutati a seguito di una prevenzione degli attacchi DoS |
| authz-latency | Numero totale di millisecondi trascorsi sull&#39;endpoint MVPD |

### Gli MVPD possono filtrare le metriche elencate sopra per le seguenti dimensioni:

| *Nome Dimension* | *Descrizione* |
|---|---|
| anno | L&#39;anno a 4 cifre |
| mese | Il mese dell&#39;anno (1-12) |
| giorno | Il giorno del mese (1-31) |
| ora | Ora del giorno |
| minuto | Il minuto dell&#39;ora |
| requestor-id | ID richiedente utilizzato per eseguire la richiesta di adesione |
| eap | Provider di autenticazione esterno quando il flusso di autenticazione viene eseguito tramite un sistema esterno. </br> I valori possono essere: </br> - N/D - l&#39;autenticazione è stata fornita da Primetime Authentication </br> - Apple - il sistema esterno che ha fornito l’autenticazione è Apple |
| cdt | La piattaforma dispositivo (alternativa), attualmente utilizzata per Clientless. </br>  I valori possono essere: </br> - N/D - l’evento non è nato da un SDK Clientless </br> - Sconosciuto - Poiché il parametro deviceType di un&#39;API Clientless è facoltativo, ci sono chiamate che non contengono alcun valore. </br> - qualsiasi altro valore inviato tramite l’API Clientless, ad esempio xbox, appletv, roku ecc. </br> |
| tipo sdk | L’SDK client utilizzato (Flash, HTML5, nativo Android, iOS, Clientless, ecc.) |


## Casi d&#39;uso {#use-cases}

Puoi utilizzare i dati ESM per i seguenti casi d’uso:

- **Monitoraggio** - I team di ops o di monitoraggio possono creare un dashboard o un grafico che richiama l’API ogni minuto. Utilizzando le informazioni visualizzate, è possibile rilevare un problema (con l&#39;autenticazione Primetime o con un MVPD) nel momento in cui viene visualizzato.  

- **Debug/Test di qualità** - Poiché i dati sono suddivisi anche per piattaforma, dispositivo, browser e sistema operativo, l’analisi dei pattern di utilizzo può individuare problemi su specifiche combinazioni (ad esempio, Safari su OSX).  

- **Analytics** - I dati forniti possono essere utilizzati per integrare/controllare i dati lato client raccolti tramite Adobe Analytics o un altro strumento di analisi.

<!--
## Related Information {#related-information}

- [ESM API](/help/authentication/entitlement-service-monitoring-api.md)
- [Degradation API Overview](/help/authentication/degradation-api-overview.md)
- [Server-side Metrics](/help/authentication/understanding-serverside-metrics.md)
-->