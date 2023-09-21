---
title: API del rapporto
description: API del rapporto di Auditude
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1042'
ht-degree: 1%

---

# API del rapporto {#report-api}

L’interfaccia utente dispone di ruoli gestiti per i clienti e per il team di abilitazione (Adobe). I clienti possono accedere al portale e quindi creare e modificare le proprie configurazioni. Possono anche visualizzare i rapporti relativi alle impression degli annunci sull’interfaccia utente.

Le API lavorano dietro le quinte per facilitare la comunicazione tra clienti e amministratori e l’infrastruttura back-end.

Per esplorare [!DNL Primetime Ad Insertion] API vedi [Endpoint API Ad Insertion nell’interfaccia utente scaglionata](https://adconfigservice-va6.cloud.adobe.io/swagger-ui/index.html#/).

## Endpoint API {#report-api-endpoint}

### Produzione {#production}

`https://dai-primetime.adobe.io/report`

### Sandbox {#sandbox}

`https://dai-sandbox1-primetime.adobe.io/report`

## Parametri di query


| Nome | Significatività | Tipo di valore | Obbligatorio? | Valore predefinito | Vincoli | Esempio/ Valori di esempio validi |
|----------|-----------------------------------------------------------------------------------------------|----------------|----------------|---------------------|------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| endDate | Data di fine dei dati del rapporto | data | Y | NESSUNO | non più recente di ieri in UTC-8 | ######## |
| filtri | filtrare per una o più colonne | stringa | N | NESSUNO | ad_config_id , zone_id | ad_config_id=990,900;state=active |
|          |                                                                                               |                |                |                     | Quando i metadati sono impostati su &quot;true&quot; nella richiesta, è anche possibile filtrare per nome. |                                                                         |
|          |                                                                                               |                |                |                     |                                                                                    | Più chiavi di filtro sono separate da punto e virgola. |
|          |                                                                                               |                |                |                     |                                                                                    | Utilizza valori separati da virgole per fornire un elenco di valori per la chiave del filtro |
| groupBy | Raggruppa per ora (anno \| mese \| giorno) o ad_config_id. Adconfig è sinonimo di AdRule. | stringa | N | NESSUNO | y \| m \| d , ad_config_id | m , ad_config_id |
|          |                                                                                               |                |                |                     |                                                                                    |                                                                         |
|          |                                                                                               |                |                |                     |                                                                                    | Per groupBy in tempo fornire uno tra y o m oppure d |
|          |                                                                                               |                |                |                     |                                                                                    |                                                                         |



## Intestazioni {#headers}

| Nome | Tipo di valore | Obbligatorio | Valore di esempio | Significatività |
|-----------------------|----------------|---------------|-------------------------------------|------------------------------------|
| Accetta | stringa | Y | text/csv per CSV | Tipo di risposta previsto dall’API |
|                       |                |               | application/json oppure &quot;*/*&#39; per JSON |                                    |
| Token di autorizzazione | stringa | Y | xyz | token di autorizzazione |
| x-api-key | stringa | Y | xyz | Chiave API |
| x-gw-ims-org-id | stringa | Y | xyz12345 | ID organizzazione IMS dell’account |

* Puoi generare il token di autorizzazione (noto anche come token di accesso) seguendo i passaggi descritti nella guida per l’autenticazione JWT di Adobe.io.
  >>
  [!NOTE]
  >Il token di autorizzazione ha una scadenza di 24 ore; pertanto, se utilizzi l’API di rapporto con uno script ricorrente, accertati di generare il token di autorizzazione prima della scadenza oppure quando ricevi un errore Oauth che indica che il token non è valido.

* Per impostare i valori corretti nell’intestazione della richiesta e generare il token di autorizzazione (utilizzando l’autenticazione JWT) è necessario conoscere le seguenti configurazioni per il tuo account. Per ottenere questi valori, rivolgiti al team di supporto di Primetime.
ID account tecnico

   * ID organizzazione
   * Api_key
   * Segreto_client

## Output {#output}

Il risultato della query API dei rapporti per impostazione predefinita è in formato JSON che specifica le impression rispetto ai diversi valori delle dimensioni (parametro groupby) richieste. L’output di esempio è dato di seguito:

```JSON
[
    {
        "dates": "07-2020",
        "total_impressions": 213007041
    },
    {
        "dates": "08-2020",
        "total_impressions": 174711626
    },
    {
        "dates": "09-2020",
        "total_impressions": 102863153
    }
]
```

## Codici e stringhe di errore {#error-codes-strings}

### Formato risposta errore {#error-response-format}

Errore durante il rendering della macro &#39;code&#39;: valore non valido specificato per il parametro `com.atlassian.confluence.ext.code.render.InvalidValueException`

```Shell
{
"error_code": "<ERROR_CODE>",
"message": "<ERROR_MESSAGE>"
}
```

La tabella seguente elenca i codici di errore e i messaggi che l’API di report può restituire. Per gli errori relativi al livello di autorizzazione, fare riferimento al [documentazione relativa ai codici di errore](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#errors-and-troubleshooting) di Adobe.io.

| Codice di errore | Messaggio di errore |
|-----------------------|------------------------------------------|
| 4001007 | Dettagli utente non validi. |
| 4001008 | Tutte le zone non appartengono allo stesso account. |
| 5001010 | Errore interno. |
| 4001011 | Le date non vengono inviate nel formato richiesto. |
| 4001012 | Le date non rientrano nell&#39;intervallo consentito. |
| 4001013 | Parametro obbligatorio mancante. |
| 4001014 | L’elenco delle zone è vuoto per l’account. |
| 4001015 | Chiavi filtro non valide nella richiesta. |
| 4001016 | Opzione GroupBy non valida nella richiesta. |
| 4001017 | ID non valido fornito nella richiesta |

## Chiamate di esempio e risultati previsti {#sample-calls-expected-results}

Di seguito è riportato il comando curl per ottenere conteggi di impression mensili tra il 2020-07-01 e il 2021-06-30 utilizzando il token di accesso:

**Esempio di chiamata API di reporting**

```shell
curl --location --request GET 'https://dai-sandbox1-primetime.adobe.io/report?startDate=2020-07-01&endDate=2021-06-30&groupBy=m&unpaged=true' \
--header 'x-api-key: <API_KEY>' \
--header 'x-gw-ims-org-id: <ORG_ID>' \
--header 'Authorization: Bearer <ACCESS_TOKEN_STRING>' \
--header 'Accept: application/json'
```

| Chiamata di esempio/caso d’uso | Risultato previsto |
|---|---|
| Recupera rapporto con date di inizio e fine GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2021-01-01 intestazione : Accept = application/json. o */* | Json con i seguenti parametri con tutti gli annunci appartenenti a questo account total_impressions |
| Recupera report con GroupBy = d \| m \| y GET: [API_ENDPOINT]//report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;groupBy=d \| m \| y intestazione : Accept = application/json. o */* | Json con i seguenti parametri con tutti gli annunci appartenenti a questa data conto (gg-mm-aaaa \| mm-aaaa \| formato aaaa) total_impressions |
| Recupera report con GroupBy = ad_config_id GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;groupBy=ad_config_id intestazione : Accept = application/json. o */* | Json con i seguenti parametri con tutti gli annunci appartenenti a questo account ad_config_id total_impressions |
| Recupera report con GroupBy = d \| m \| y e ad_config_id GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;groupBy=d,ad_config_id intestazione : Accept = application/json. o */* | Json con i seguenti parametri con tutti gli annunci appartenenti a questo account ad_config_id date (mm-gg-aaaa \| mm-aaaa \| formato aaaa) total_impressions |
| Recupera report con metaData=true e groupBy=d \| m \| y GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;metaData=true&amp;groupBy=ad_config_id intestazione : Accept = application/json. o */* | Json con i seguenti parametri con tutti gli annunci appartenenti a questo account ad_config_id nome total_impressions |
| Recupera report con groupBy=d \| m \| y e ad_config_id GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;metaData=true&amp;groupBy=d \| m \| y,ad_config_id intestazione : Accept = application/json. o */* | Json con i seguenti parametri con tutti gli annunci appartenenti a questo account ad_config_id nome total_impressions date (formato mm-gg-aaaa \| mm-aaaa \| aaaaa) |
| Recupera il rapporto per ottenere tutte le righe per un determinato intervallo di date (con non impaginato = true) GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-31&amp;groupBy=d&amp;unpaged=true | 31 voci nell’array Json restituito |
| Recupera report con parametri di query pagina validi: GET [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-31&amp;page=0&amp;size=5&amp;groupBy=d | 5 voci nell’array restituito |
| Recupera report, con GET in formato CSV: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10 intestazione : Accept = text/csv | Viene restituita una stringa CSV con intestazione: total_impressions |
| Recupera report, con formato csv e groupBy = d \| m \| y GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10&amp;groupBy=d\|m\|y intestazione : Accept = text/csv | Viene restituita una stringa CSV con intestazione: total_impressions dates (mm-gg-aaaa \| mm-aaaa \| formato aaaa) |
| Recupera rapporto, con formato csv e metadati = true GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10&amp;metaData=true intestazione : Accept = text/csv | Viene restituita una stringa CSV con intestazione: total_impressions |
| Recupera report, con formato csv, metadati = true e groupBy = d \| m \| y GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10&amp;metaData=true&amp;groupBy=d\|m\|y intestazione : Accept = text/csv | Viene restituita una stringa CSV con intestazione: total_impressions dates (mm-gg-aaaa \| mm-aaaa \| formato aaaa) |


## Criterio di limitazione API del rapporto {#report-api-throttling-policy}

* Per ogni utente sono consentite 5 richieste API in una finestra di 5 secondi.
* Se un utente supera il limite, la risposta viene ritardata di 5 secondi.
* Se un utente effettua più di 10 chiamate entro una finestra di 5 secondi, inizierà a essere rifiutato con la risposta &quot;429 Troppe richieste&quot;.
