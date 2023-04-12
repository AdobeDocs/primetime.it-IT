---
title: API di monitoraggio del servizio di adesione
description: API di monitoraggio del servizio di adesione
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2026'
ht-degree: 0%

---


# API di monitoraggio del servizio di adesione {#entitlement-service-monitoring-api}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Panoramica API {#api-overview}

Il monitoraggio del servizio di adesione (ESM) è implementato come WOLAP (basato su Web) [Elaborazione analitica online](https://en.wikipedia.org/wiki/Online_analytical_processing){target=_blank}). ESM è un’API Web generica per la generazione di rapporti aziendali supportata da un data warehouse. Funge da linguaggio di query HTTP che consente di eseguire completamente il RESTretrò delle operazioni OLAP tipiche.

>[!NOTE]
>
>L’API ESM non è generalmente disponibile. Per domande sulla disponibilità, contatta il tuo rappresentante Adobe.

L&#39;API ESM fornisce una visualizzazione gerarchica dei cubi OLAP sottostanti. Ogni risorsa ([dimension](#esm_dimensions) nella gerarchia delle dimensioni, mappata come segmento del percorso URL) genera rapporti con (aggregato) [metriche](#esm_metrics) per la selezione corrente. Ciascuna risorsa fa riferimento alla relativa risorsa principale (per il rollup) e alle relative risorse secondarie (per il drill-down). L’applicazione di suddivisioni e barre viene ottenuta tramite parametri di stringa di query che fissano dimensioni a valori o intervalli specifici.

L’API REST fornisce i dati disponibili entro un intervallo di tempo specificato nella richiesta (in base ai valori predefiniti se non ne sono forniti), in base al percorso della dimensione, ai filtri forniti e alle metriche selezionate. L’intervallo di tempo non viene applicato ai rapporti che non contengono dimensioni di ora (anno, mese, giorno, ora, minuto, secondo).

Il percorso principale dell’URL dell’endpoint restituirà le metriche aggregate complessive all’interno di un singolo record, insieme ai collegamenti alle opzioni di drill-down disponibili. La versione API viene mappata come segmento finale del percorso URI dell’endpoint. Ad esempio: `https://mgmt.auth.adobe.com/*v2*` significa che i client accederanno alla versione 2 di WOLAP.

I percorsi URL disponibili sono individuabili tramite i collegamenti contenuti nella risposta. Vengono mantenuti percorsi URL validi per mappare un percorso all’interno della struttura di drill-down sottostante che contiene metriche (pre) aggregate. Un percorso nel modulo `/dimension1/dimension2/dimension3` riflette una pre-aggregazione di queste tre dimensioni (l&#39;equivalente di un SQL `clause GROUP` DA `dimension1`, `dimension2`, `dimension3`). Se tale pre-aggregazione non esiste e il sistema non è in grado di calcolarla al volo, l’API restituirà una risposta 404 Not Found (Non trovato).

## Struttura a discesa {#drill-down-tree}

I seguenti alberi a discesa illustrano le dimensioni (risorse) disponibili in ESM 2.0 per [Programmatori] (#esm_Dimensions) e [MVPD](#esm_dimensions_mvpd).


### Dimension disponibili per i programmatori {#progr-dimensions}

![](assets/esm-progr-dimensions.png)

### Dimension disponibili per gli MVPD {#mvpd-dimensions}

![](assets/esm-mvpd-dimensions.png)

Una GET al `https://mgmt.auth.adobe.com/v2` L’endpoint API restituisce una rappresentazione contenente:

* Collegamenti ai percorsi di drill-down principali disponibili:

   * `<link rel="drill-down" href="/v2/dimensionA"/>`

   * `<link rel="drill-down" href="/v2/dimensionB"/>`

* Riepilogo (valori aggregati) di tutte le metriche (nell’intervallo predefinito, poiché non sono forniti parametri della stringa di query, vedi di seguito).


Seguendo un percorso di drill-down (passo dopo passo):
`/dimensionA/year/month/day/dimensionX` recupera la risposta seguente:

* Collegamenti a &quot;`dimensionY`&quot; e &quot;`dimensionZ`&quot; opzioni drill-down

* Un rapporto contenente aggregati giornalieri per ciascun valore di `dimensionX`


### Filtri

Ad eccezione delle dimensioni data/ora, qualsiasi dimensione disponibile per la proiezione corrente (percorso dimensione) può essere filtrata utilizzando il suo nome come parametro della stringa query.

Sono disponibili le seguenti opzioni di filtro:

* **Uguale** i filtri vengono forniti impostando il nome della dimensione su un particolare valore nella stringa query.

* **IN** è possibile specificare i filtri aggiungendo lo stesso parametro nome-dimensione più volte con valori diversi: dimension=value1\&amp;dimension=value2

* **Non è uguale a** i filtri devono utilizzare &#39;\!&#39; simbolo dopo il nome della dimensione con conseguente &#39;\!= &quot;operatore&quot;: dimension\!=value

* **NON IN** i filtri richiedono &#39;\!=&#39; da utilizzare più volte, una volta per ogni valore del set: dimension\!=value1\&amp;dimension\!=valore2&amp;..

È inoltre disponibile un utilizzo speciale per i nomi delle dimensioni nella stringa di query: Se il nome della dimensione viene utilizzato come parametro della stringa di query senza valore, questo indica all’API di restituire una proiezione che include tale dimensione nel rapporto.

### Esempio di query ESM

| *URL* | *Equivalente SQL* |
|---|---|
| /dimension1/dimension2/dimension3?dimension1=value1 | SELECT * dalla proiezione WHERE dimension1 = &#39;value1&#39; </br> GROUP BY dimension1, dimension2, dimension3 |
| /dimension1/dimension2/dimension3?dimension1=valore1&amp;dimensione1=valore2 | SELECT * dalla proiezione WHERE dimension1 IN (&#39;value1&#39;, &#39;value2&#39;) </br> GROUP BY dimension1, dimension2, dimension3 |
| /dimension1/dimension2/dimension3?dimension1!=value1 | SELECT * dalla proiezione WHERE dimension1 &lt;> &#39;value1&#39; | </br> GROUP BY dimension1, dimension2, dimension3 |
| /dimension1/dimension2/dimension3?dimension1!=valore1&amp;dimensione2!=value2 | SELECT * dalla proiezione WHERE dimension1 NOT IN (&#39;value1&#39;, &#39;value2&#39;) | </br> GROUP BY dimension1, dimension2, dimension3 |
| Presupponendo che non ci sia un percorso diretto: /dimension1/dimension3 </br> ma c&#39;è un percorso: /dimension1/dimension2/dimension3 </br> </br> /dimension1?dimension3 | SELECT * dalla proiezione GROUP BY dimension1, dimension3 |

>[!NOTE]
>
>Nessuna di queste tecniche di filtro funzionerà per `date/time` dimensioni. L’unico modo per filtrare `date/time` le dimensioni sono impostate `start` e `end` i parametri della stringa di interrogazione (descritti di seguito) ai valori richiesti.

I seguenti parametri della stringa di query hanno significati riservati per l’API (e quindi non possono essere utilizzati come nomi di dimensione, altrimenti per una dimensione di questo tipo non sarebbe possibile alcun filtro).

### Parametri stringa di query riservate API ESM

| Parametro | Facoltativo | Descrizione | Valore predefinito | Esempio |
| --- | ---- | --- | ---- | --- |
| access_token | Sì | Se la protezione OAuth IMS è abilitata, il token IMS può essere passato come token portatore di autorizzazione standard o come parametro della stringa di query. | Nessuno | access_token=XXXXXX |
| nome-dimensione | Sì | Qualsiasi nome di dimensione - contenuto nel percorso URL corrente o in un qualsiasi sottopercorso valido; il valore viene trattato come un filtro uguale a. Se non viene fornito alcun valore, verrà forzata l’inclusione nell’output della dimensione specificata anche se non è inclusa o adiacente al percorso corrente | Nessuno | someDimension=someValue&amp;someOtherDimension |
| end | Sì | Ora di fine del rapporto in millisecondi | Ora corrente del server | end=2012-07-30 |
| format | Sì | Utilizzato per la negoziazione dei contenuti (con lo stesso effetto ma con precedenza inferiore rispetto al percorso &quot;estensione&quot; - vedi di seguito). | Nessuno: la negoziazione dei contenuti proverà le altre strategie | format=json |
| limite | Sì | Numero massimo di righe da restituire | Valore predefinito segnalato dal server nel collegamento automatico se nella richiesta non è specificato alcun limite | limit=1500 |
| metriche | Sì | Elenco separato da virgole dei nomi delle metriche da restituire; dovrebbe essere utilizzato sia per filtrare un sottoinsieme delle metriche disponibili (per ridurre la dimensione del payload) sia per far sì che l’API restituisca una proiezione contenente le metriche richieste (anziché la proiezione ottimale predefinita). | Tutte le metriche disponibili per la proiezione corrente verranno restituite nel caso in cui questo parametro non venga fornito. | metriche=m1,m2 |
| start | Sì | Ora di inizio del rapporto come ISO8601; il server compilerà la parte rimanente se viene fornito solo un prefisso: Ad esempio, start=2012 si tradurrà in start=2012-01-01:00:00:00 | Segnalati dal server nel collegamento automatico; il server cerca di fornire valori predefiniti ragionevoli in base alla granularità temporale selezionata | start=2012-07-15 |

L’unico metodo HTTP disponibile al momento è GET. Il supporto per i metodi OPTIONS / HEAD può essere fornito nelle versioni future.

## Codici di stato dell’API ESM {#esm-api-status-codes}

| Codice di stato | Frase del motivo | Descrizione |
|---|---|---|
| 200 | OK | La risposta conterrà i collegamenti &quot;roll-up&quot; e &quot;drill-down&quot; (se applicabile). Il report verrà rappresentato come un attributo della risorsa: un elemento/proprietà &quot;report&quot; nidificato. |
| 400 | Richiesta non valida | Il corpo della risposta conterrà un messaggio di testo che spiega cosa non va nella richiesta. </br> </br> Lo stato di 400 Bad Request è accompagnato da un testo che spiega la risposta nel corpo (tipo di supporto normale/testuale), che fornisce informazioni utili relative all’errore del client. Oltre ai semplici scenari quali formati di data non validi o filtri applicati a dimensioni non esistenti, il sistema rifiuterà anche di rispondere a query che richiedono la restituzione o l&#39;aggregazione al volo di un volume massiccio di dati. |
| 401 | Non autorizzato | Causato da una richiesta che non contiene le intestazioni OAuth appropriate per autenticare l’utente |
| 403 | Proibito | Indica che la richiesta non è consentita nel contesto di sicurezza corrente; questo si verifica quando l&#39;utente è autenticato ma non autorizzato ad accedere alle informazioni richieste |
| 404 | Non trovato | Si verifica nel caso in cui venga fornito un percorso URL non valido con la richiesta. Questo non dovrebbe mai verificarsi se il cliente segue i collegamenti &quot;drill-down&quot;/&quot;roll-up&quot; forniti con 200 risposte |
| 405 | Metodo non consentito | Indica che nella richiesta è stato utilizzato un metodo non supportato. Anche se al momento è supportato solo il metodo GET, le versioni future potrebbero consentire ad HEAD o OPTIONS |
| 406 | Non accettabile | Segnala che il client ha richiesto un tipo di supporto non supportato |
| 500 | Errore interno del server | &quot;Questo non dovrebbe mai accadere&quot; |
| 503 | Servizio non disponibile | Segnala un errore all&#39;interno dell&#39;applicazione o delle sue dipendenze |

## Formati di dati {#data-formats}

I dati sono disponibili nei seguenti formati:

* JSON (predefinito)
* XML
* CSV
* HTML (a scopo dimostrativo)

I client possono utilizzare le seguenti strategie di negoziazione dei contenuti (la precedenza è data dalla posizione nell’elenco - prima cose):

1. Un&#39;&quot;estensione file&quot; aggiunta all&#39;ultimo segmento del percorso URL: Ad esempio, `/esm/v2/media-company/year/month/day.xml`. Se l&#39;URL contiene una stringa di interrogazione, l&#39;estensione deve precedere il punto interrogativo: `/esm/v2/media-company/year/month/day.csv?mvpd= SomeMVPD`
1. Parametro della stringa di query del formato: Ad esempio, `/esm/report?format=json`
1. Intestazione standard di HTTP Accept: Ad esempio, `Accept: application/xml`

Sia l’&quot;estensione&quot; che il parametro di query supportano i seguenti valori:

* xml
* json
* csv
* html

Se nessuna delle strategie specifica alcun tipo di supporto, l’API produrrà contenuto JSON per impostazione predefinita.

## Lingua dell&#39;applicazione ipertesto {#hypertext-application-language}

Per JSON e XML, il payload verrà codificato come HAL, come descritto di seguito:  <http://stateless.co/hal_specification.html>.

Il rapporto effettivo (un tag/proprietà nidificato denominato &quot;report&quot;) sarà costituito dall&#39;elenco effettivo di record contenenti tutte le dimensioni e le metriche selezionate/applicabili con i relativi valori, codificati come segue:

### JSON

```JSON
 "report": [
  {
    "dimension1": "d1",
    ...
    "metric1": "m1",
    ...
  }, {
    ...
  }
]
```

### XML

```XML
 <report>
  <record dimension1="d1" ... metric1="m1" ... />
  ...
</report
```

Per i formati XML e JSON, l’ordine dei campi (dimensioni e metriche) all’interno di un record non è specificato, ma è coerente (l’ordine sarà lo stesso in tutti i record). Tuttavia, i clienti non devono fare affidamento su un ordine particolare dei campi all&#39;interno di un record.

Il collegamento della risorsa (l&#39;attributo &quot;self&quot; in JSON e l&#39;attributo della risorsa &quot;href&quot; in XML) contiene il percorso corrente e la stringa di query utilizzata per il rapporto in linea. La stringa di query rivelerà tutti i parametri impliciti ed espliciti, in modo che il payload indichi esplicitamente l’intervallo di tempo utilizzato, gli eventuali filtri impliciti e così via. Il resto dei collegamenti all’interno della risorsa conterrà tutti i segmenti disponibili che possono essere seguiti per espandere i dati correnti. Viene inoltre fornito un collegamento per il roll-up, che indicherà il percorso principale (se presente). La `href` il valore per i collegamenti drill-down/roll-up contiene solo il percorso URL (non include la stringa di query, quindi deve essere aggiunto dal client se necessario). Non tutti i parametri della stringa di query utilizzati (o impliciti) dalla risorsa corrente saranno applicabili per i collegamenti &quot;roll-up&quot; o &quot;drill-down&quot; (ad esempio, i filtri potrebbero non essere applicabili alle risorse secondarie o super).

Esempio (supponendo che sia presente una singola metrica denominata `clients` e esiste una pre-aggregazione per `year/month/day/...`):

* https://mgmt.auth.adobe.com/esm/v2/year/month.xml

```XML
   <resource href="/esm/v2/year/month?start=2012-07-20T00:00:00&end=2012-08-20T14:35:21">
   <links>
   <link rel="roll-up" href="/esm/v2/year"/>
   <link rel="drill-down" href="/esm/v2/year/month/day"/>
   </links>
   <report>
   <record month="6" year="2012" clients="205"/>
   <record month="7" year="2012" clients="466"/>
   </report>
   </resource>
```

* https://mgmt.auth.adobe.com/esm/v2/year/month.json 

   ```JSON
       {
         "_links" : {
           "self" : {
             "href" : "/esm/v2/year/month?start=2012-07-20T00:00:00&end=2012-08-20T14:35:21"
           },
           "roll-up" : {
             "href" : "/esm/v2/year"
           },
           "drill-down" : {
             "href" : "/esm/v2/year/month/day"
           }
         },
         "report" : [ {
           "month" : "6",
           "year" : "2012",
           "clients" : "205"
         }, {
           "month" : "7",
           "year" : "2012",
           "clients" : "466"
         } ]
       }
   ```

### CSV

Nel formato dati CSV non vengono forniti collegamenti o altri metadati (ad eccezione della riga di intestazione) in linea; i metadati di selezione verranno invece forniti nel nome file, che seguirà questo pattern:

```CSV
    esm__<start-date>_<end-date>_<filter-values,...>.csv
```

Il CSV conterrà una riga di intestazione e quindi i dati del rapporto come righe successive. La riga di intestazione conterrà tutte le dimensioni seguite da tutte le metriche. L’ordinamento dei dati del rapporto si rifletterà nell’ordine delle dimensioni. Pertanto, se i dati sono ordinati per `D1` e poi `D2`, l’intestazione CSV si presenterà così: `D1, D2, ...metrics...`.

L’ordine dei campi nella riga di intestazione riflette l’ordinamento dei dati della tabella.


Esempio: https://mgmt.auth.adobe.com/v2/year/month.csv produrrà un file denominato `report__2012-07-20_2012-08-20_1000.csv` con il seguente contenuto:


| Anno | Mese | Client |
| ---- | :---: | ------- |
| 2012 | 6 | 580 |
| 2012 | 7 | 231 |

## Freschezza dei dati {#data-freshness}

Le risposte HTTP riuscite contengono un `Last-Modified` intestazione che indica l’ora dell’ultimo aggiornamento del rapporto nel corpo. L’assenza di un’intestazione Last-Modified indica che i dati del report vengono calcolati in tempo reale.

Di solito, i dati a grana grossa vengono aggiornati con una frequenza inferiore a quelli a grana fine (ad esempio, i valori al minuto o i valori orari) possono essere più aggiornati dei valori giornalieri, specialmente per le metriche che non possono essere calcolate in base a granularità minori, come i conteggi univoci).

Le versioni future di ESM possono consentire ai client di eseguire GET condizionali fornendo l&#39;intestazione standard &quot;If-Modified-Since&quot;.

## Compressione GZIP {#gzip-compression}

Adobe consiglia vivamente di abilitare il supporto gzip nei client che recuperano i report ESM. In questo modo si ridurrà notevolmente la dimensione della risposta, che a sua volta riduce il tempo di risposta. (Il rapporto di compressione per i dati ESM è compreso nell’intervallo 20-30.)

Per abilitare la compressione gzip nel client, imposta la `Accept-Encoding:` come segue:

* Accept-Encoding: gzip, deflazione


<!--
## Related Information {#related-information}

- [ESM Overview](/help/authentication/entitlement-service-monitoring-overview.md)
- [Degradation API Overview](/help/authentication/degradation-api-overview.md)
- [Understanding Server-side Metrics](/help/authentication/understanding-serverside-metrics.md)
-->