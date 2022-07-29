---
title: API rapporto
description: API del rapporto di audit
exl-id: 50eb4869-3765-4591-8c41-794b29d50044
source-git-commit: 628544e38616715e83e0274ba26cf93302ce0e61
workflow-type: tm+mt
source-wordcount: '1042'
ht-degree: 1%

---

# API rapporto {#report-api}

Interfaccia utente dispone di ruoli gestiti per i clienti e per il team di abilitazione (Adobe). I clienti possono accedere al portale e quindi creare e modificare le proprie configurazioni. Possono inoltre visualizzare i rapporti relativi alle impression degli annunci sull’interfaccia utente.

Le API lavorano dietro le quinte per facilitare la comunicazione tra clienti e amministratori con l’infrastruttura back-end.

Per esplorare [!DNL Primetime Ad Insertion] API vedi [Endpoint API di Ad Insertion nell’interfaccia utente swaggered](https://adconfigservice-va6.cloud.adobe.io/swagger-ui/index.html#/).

## Endpoint API {#report-api-endpoint}

### Produzione {#production}

`https://dai-primetime.adobe.io/report`

### Sandbox {#sandbox}

`https://dai-sandbox1-primetime.adobe.io/report`

## Parametri query


| Nome | Significato | Tipo di valore | Obbligatorio? | Valore predefinito | Vincoli | Esempio/Valori di esempio validi |
|----------|-----------------------------------------------------------------------------------------------|----------------|----------------|---------------------|------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| endDate | Data di fine dei dati del rapporto | date | Y | NESSUNO | non più recente di ieri in UTC-8 | ########## |
| filtri | filtrare su una o più colonne | string | N | NESSUNO | ad_config_id , zone_id | ad_config_id=990,900;state=active |
|  |  |  |  |  | Quando metaData è impostato su &quot;true&quot; nella richiesta, puoi anche filtrare per nome. |  |
|  |  |  |  |  |  | Le chiavi filtro multiple sono separate da punto e virgola. |
|  |  |  |  |  |  | Utilizza valori separati da virgole per fornire un elenco di valori per la chiave filtro |
| groupBy | Raggruppa per ora ( anno \| mese \| giorno) o ad_config_id. Adconfig è sinonimo di AdRule. | string | N | NESSUNO | y \| m \| d , ad_config_id | m , ad_config_id |
|  |  |  |  |  |  |  |
|  |  |  |  |  |  | Per il gruppoPer in tempo specificare uno tra y o m o d |
|  |  |  |  |  |  |  |



## Intestazioni {#headers}

| Nome | Tipo di valore | Obbligatorio | Valore di esempio | Significato |
|-----------------------|----------------|---------------|-------------------------------------|------------------------------------|
| Accetta | string | Y | text/csv per CSV | Tipo di risposta previsto dall’API |
|  |  |  | application/json o &#39;*/*&#39; per JSON |  |
| Token di autorizzazione | string | Y | xyz | token di autorizzazione |
| x-api-key | string | Y | xyz | Chiave API |
| x-gw-ims-org-id | string | Y | xyz12345 | ID organizzazione IMS del tuo account |

* Puoi generare il token di autorizzazione (noto anche come token di accesso) seguendo i passaggi descritti nella pagina di aiuto per l’autenticazione JWT di Adobe.io.
   >[!NOTE]
   >Il token di autorizzazione ha una scadenza di 24 ore, quindi se utilizzi l’API dei rapporti utilizzando uno script ricorrente, assicurati di generare il token di autenticazione prima della sua scadenza o quando ottieni un errore Oauth riguardo alla non validità del token.

* Per impostare i valori corretti nell’intestazione della richiesta e generare il token di autorizzazione (utilizzando l’autenticazione JWT) dovrai conoscere le configurazioni seguenti per il tuo account. Contatta il team di supporto Primetime per ottenere questi valori.
ID account tecnico

   * ID organizzazione
   * Api_key
   * Segreto_client

## Uscita {#output}

Il risultato della query API del rapporto per impostazione predefinita è in formato JSON che specifica le impression rispetto ai diversi valori delle dimensioni richieste (raggruppper param). Di seguito è riportato l&#39;output del campione:

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

### Formato della risposta di errore {#error-response-format}

Errore durante il rendering del codice della macro: Valore non valido specificato per il parametro `com.atlassian.confluence.ext.code.render.InvalidValueException`

```Shell
{
"error_code": "<ERROR_CODE>",
"message": "<ERROR_MESSAGE>"
}
```

Nella tabella seguente sono elencati i codici di errore e i messaggi che l’API per report può restituire. Per gli errori relativi al livello di autorizzazione, fai riferimento alla [documentazione del codice di errore](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#errors-and-troubleshooting) di Adobe.io.

| Codice di errore | Messaggio di errore |
|-----------------------|------------------------------------------|
| 4001007 | Dettagli utente non validi. |
| 4001008 | Tutte le aree non provengono dallo stesso account. |
| 5001010 | Errore interno. |
| 4001011 | Le date non vengono inviate nel formato richiesto. |
| 4001012 | Le date sono fuori intervallo. |
| 4001013 | Parametro obbligatorio mancante. |
| 4001014 | L&#39;elenco delle aree è vuoto per l&#39;account. |
| 4001015 | Chiavi filtro non valide nella richiesta. |
| 4001016 | Opzione GroupBy non valida nella richiesta. |
| 4001017 | ID non valido fornito nella richiesta |

## Chiamate di esempio e risultati previsti {#sample-calls-expected-results}

Di seguito è riportato il comando curl per ottenere i conteggi mensili delle impression tra 2020-07-01 e 2021-06-30 utilizzando il token di accesso:

**Esempio di chiamata API di reporting**

```shell
curl --location --request GET 'https://dai-sandbox1-primetime.adobe.io/report?startDate=2020-07-01&endDate=2021-06-30&groupBy=m&unpaged=true' \
--header 'x-api-key: <API_KEY>' \
--header 'x-gw-ims-org-id: <ORG_ID>' \
--header 'Authorization: Bearer <ACCESS_TOKEN_STRING>' \
--header 'Accept: application/json'
```

| Caso di utilizzo/chiamata di esempio | Risultato previsto |
|---|---|
| Recupera rapporto con date di inizio e fine GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2021-01-01 intestazione : Accept = application/json. o */* | Json con i seguenti parametri con tutti gli annunci appartenenti a questo account total_impression |
| Recupera report con GroupBy = d \| m \| y GET: [API_ENDPOINT]//report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;groupBy=d \| m \| y header : Accept = application/json. o */* | Json con i seguenti parametri con tutti gli annunci appartenenti a questo account date (mm-gg-aaaa \| mm-aaaa \| formato aaaa) total_impression |
| Recupera rapporto con GroupBy = ad_config_id GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;groupBy=ad_config_id intestazione : Accept = application/json. o */* | Json con i seguenti parametri con tutti gli annunci appartenenti a questo account ad_config_id total_impression |
| Recupera rapporto con GroupBy = d \| m \| y e ad_config_id GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;groupBy=d,ad_config_id header : Accept = application/json. o */* | Json con i seguenti parametri con tutti gli annunci appartenenti a questo account date ad_config_id (mm-gg-aaaa \| mm-aaaa \| formato aaaa) total_impression |
| Recupera report con metaData=true e groupBy=d \| m \| y GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;metaData=true&amp;groupBy=ad_config_id intestazione : Accept = application/json. o */* | Json con i seguenti parametri con tutti gli annunci appartenenti a questo account ad_config_id name total_impression |
| Recupera rapporto con groupBy=d \| m \| y e ad_config_id GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;metaData=true&amp;groupBy=d \| m \| y,ad_config_id header : Accept = application/json. o */* | Json con i seguenti parametri con tutti gli annunci appartenenti a questo account ad_config_id nome totale_impressioni date (mm-gg-aaaa \| mm-aaaa \| formato aaaa) |
| Recupera rapporto per ottenere tutte le righe per un dato intervallo di date (con non pagato = true) GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-31&amp;groupBy=d&amp;unpaged=true | 31 voci nell&#39;array Json restituito |
| Recupera rapporto con parametri di query di pagina validi GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-31&amp;page=0&amp;size=5&amp;groupBy=d | 5 voci nell&#39;array restituito |
| Recupera rapporto con formato csv: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10 intestazione : Accept = text/csv | Viene restituita una stringa CSV con intestazione: total_impression |
| Recupera rapporto, in formato CSV e groupBy = d \| m \| y GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10&amp;groupBy=d\|m\|y intestazione : Accept = text/csv | Viene restituita una stringa CSV con intestazione: date_impressioni totali (mm-gg-aaaa \| mm-aaaa \| formato aaaa) |
| Recupera rapporto, in formato CSV e metadati = true GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10&amp;metaData=true header : Accept = text/csv | Viene restituita una stringa CSV con intestazione: total_impression |
| Recupera rapporto, con formato CSV , metadati = true e groupBy = d \| m \| y GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10&amp;metaData=true&amp;groupBy=d\|m\|y intestazione : Accept = text/csv | Viene restituita una stringa CSV con intestazione: date_impressioni totali (mm-gg-aaaa \| mm-aaaa \| formato aaaa) |


## Criteri di limitazione API per i rapporti {#report-api-throttling-policy}

* 5 Le richieste API sono consentite in una finestra di 5 secondi per ogni utente.
* Se un utente supera il limite, la risposta viene ritardata di 5 secondi.
* Se un utente effettua più di 10 chiamate entro una finestra di 5 secondi, inizierà a essere rifiutato con la risposta &quot;429 Troppe richieste&quot;.
