---
title: Informazioni sulle metriche lato server
description: Informazioni sulle metriche lato server
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2187'
ht-degree: 0%

---

# Informazioni sulle metriche lato server {#understanding-server-side-metrics}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.


## Introduzione {#intro}

Questo documento descrive le metriche lato server di autenticazione Adobe Primetime generate dal servizio di monitoraggio del servizio di abilitazione (ESM). Non descrive gli stessi eventi dal punto di vista del lato client (ciò che i programmatori vedrebbero se avrebbero implementato un servizio di misurazione come Adobe Analytics sulla loro pagina/applicazione).  

## Riepilogo eventi {#events_summary}

Dal punto di vista del server di autenticazione di Adobe Primetime vengono generati i seguenti eventi:

* **Eventi generati nel flusso di autenticazione**(Accesso effettivo con MVPD)

   * Notifica di tentativo AuthN : viene generato quando l&#39;utente viene inviato al sito di accesso MVPD.
   * Notifica di AuthN Pending : se l’utente riesce ad accedere con il proprio MVPD, questo viene generato quando l’utente viene reindirizzato all’autenticazione Primetime.
   * Notifica di AuthN concesso - Viene generato quando l&#39;utente torna sul sito del programmatore e ha recuperato il token di autenticazione dall&#39;autenticazione Primetime. 
* **Flusso di autorizzazione** (Solo un controllo per l&#39;autorizzazione con un MVPD)\
   *Prerequisito:* Token AuthN valido
   * Notifica del tentativo di AuthZ
   * Notifica di AuthZ concessa
* **Richiesta di riproduzione riuscita**\
   *Prerequisito:* Token AuthN e AuthZ validi
   * Notifica di un controllo con autenticazione Adobe Primetime 
   * Una richiesta di riproduzione richiede sia un&#39;autenticazione concessa sia un&#39;autorizzazione concessa


Il numero di utenti univoci viene trattato in dettaglio nella sezione [Utenti univoci](#unique-users) di seguito. Come panoramica, poiché le risposte di autenticazione e autorizzazione concesse sono solitamente memorizzate nella cache, si applicano le seguenti formule:

* Numero di tentativi AuthN \> Numero di tentativi AuthN concessi
* Numero di tentativi AuthZ \> Numero di tentativi AuthZ concessi
* Numero di tentativi AuthZ \> Numero di tentativi AuthN concessi (di solito)
* Numero di richieste Play riuscite \> Numero di richieste AuthZ concesse


### Esempio {#example}

L’esempio seguente mostra le metriche lato server per un mese per un marchio:

| Metrica | MVPD 1 | MVPD 2 | ... | MVPD n | Totale | | — | — | — | - | — | — | | Autenticazione riuscita | 1125 | 2892 | | 2203 | SUM(MVP1+...MVPD n) | | Autorizzazioni riuscite | 2527 | 5603 | | 5904 | SUM(MVP1+...MVPD n) | | Richieste di riproduzione riuscite | 4201 | 10518 | | 10737 | SUM(MVP1+...MVPD n) | | Utenti unici | 1375 | 2400 | | 2890 | SOMMA di tutti gli utenti per tutti gli MVPD deduplicati\* | | Autenticazioni tentate | 2147 | 3887 | | 3108 | SUM(MVP1+...MVPD n) | | Autorizzazioni tentate | 2889 | 6139 | | 6039 | SUM(MVP1+...MVPD n) |

</br>

La deduplicazione in questo caso non dovrebbe avere alcun effetto, in quanto i diversi utenti MVPD non dovrebbero ricevere lo stesso ID utente. Quando si esegue una somma per due marchi diversi ma lo stesso MVPD, l&#39;effetto di deduplicazione dovrebbe essere molto più grande.

## Trigger eventi {#event_triggers}

### Nuovo utente - Flusso completo {#new-user-full-flow}

Il grafico seguente descrive gli eventi e i passaggi per un utente senza token di autenticazione (un nuovo utente o un token di autenticazione è scaduto):



![](assets/ae-flow-with-events.png)



Il flusso prevede round-trip agli MVPD per autenticazione (#5 to \#7) e autorizzazione (\#11).



Al termine del flusso, i token di autenticazione e autorizzazione vengono memorizzati nella cache del dispositivo dell’utente. I valori TTL (Time-to-Live) per i token di autenticazione sono compresi tra 6 ore e 90 giorni. Una scadenza del token AuthN forza automaticamente una scadenza del token AuthZ. Il valore TTL per il token di autorizzazione è in genere 24 ore.

| Eventi lato server attivati | <ul><li>Tentativo di autenticazione, autenticazione in sospeso, autenticazione concessa</li><li>Tentativo di autorizzazione, Autorizzazione concessa</li><li>Richiesta Play riuscita</li></ul> |
|---|---|


### Utente di ritorno - Token AuthZ e AuthN memorizzati nella cache

Per gli utenti con token AuthZ e AuthN validi memorizzati nella cache, si verificano i seguenti passaggi:


![](assets/ae-flow-tokens-cached-web.png)



Questa azione viene attivata automaticamente quando si chiama `getAuthorization()`e include solo controlli con l’autenticazione Adobe Primetime. Il MVPD non è coinvolto in questo flusso.


| Eventi lato server attivati | * Richiesta Play riuscita |
|---|---|


### Utente di ritorno - Token AuthN memorizzati nella cache, token AuthZ scaduto

Per gli utenti che hanno ancora token AuthN validi, si verificano i seguenti passaggi:

![](assets/ae-flow-authn-token-cached.png)


Questo flusso comporta un andata e ritorno al MVPD.


| Eventi lato server attivati | <ul><li>Tentativo di autorizzazione, autorizzazione OK</li><li>Richiesta Play riuscita</li> |
|---|---|

## Eventi di autenticazione {#authn_events}

### Tentativo di autenticazione {#authentication-attempt}

Come illustrato nel diagramma precedente, gli eventi di autenticazione vengono attivati solo quando l&#39;utente effettua un round trip al MVPD; gli eventi di autenticazione non includono le autenticazioni dei token memorizzate nella cache.

L’evento di tentativo di autenticazione viene attivato dopo che l’utente ha fatto clic su un particolare MVPD dal selettore.

* Il primo evento sul lato MVPD che è vicino a questo è il caricamento della pagina
* L&#39;autenticazione Adobe Primetime non conta i tentativi ripetuti dell&#39;utente di accedere alla pagina MVPD (password errata, riprova)
* più tentativi sono conteggiati come un tentativo
* Alcuni MVPD eseguono anche l&#39;autorizzazione nel passaggio Autenticazione e l&#39;utente non viene reindirizzato se l&#39;autorizzazione non riesce.

### Autenticazione in sospeso {#authentication-pending}

Questo evento si verifica quando il processo di reindirizzamento all&#39;autenticazione Adobe Primetime è stato avviato.

### Autenticazione concessa {#authentication-granted}

L&#39;utente è un utente noto dell&#39;MVPD, tipicamente con un abbonamento a Pay TV, ma a volte con solo accesso a Internet. Un&#39;autenticazione corretta può verificarsi perché l&#39;utente ha immesso esplicitamente credenziali valide con il proprio MVPD, o perché in precedenza aveva inserito credenziali valide e aveva selezionato &quot;Ricorda utente&quot; (e la sessione precedente non era scaduta).

L’MVPD invia quindi l’autenticazione Adobe Primetime una risposta positiva alla richiesta di autenticazione e l’autenticazione Adobe Primetime crea un *Token AuthN*.

* L&#39;autenticazione viene solitamente memorizzata nella cache per un lungo periodo di tempo (un mese o più). Per questo motivo, gli eventi di autenticazione non saranno più presenti finché il token non scade e il flusso non viene riavviato.
* L’accesso proveniente da un altro sito o app tramite Single Sign-On non attiverà gli eventi di autenticazione.

 

### Autenticazione composita {#comcast-authentication}

Comcast ha un flusso AuthN diverso rispetto agli altri MVPD.

Le seguenti caratteristiche descrivono le differenze:

* **Comportamento dei cookie di sessione**: Questo causa la rimozione completa di tutti i token di autenticazione dopo che l’utente ha chiuso il browser. Questa funzione è presente solo sul web. Lo scopo principale è quello di garantire che la sessione Comcast non sia persistente su computer non sicuri/condivisi. L&#39;impatto è che ci saranno più tentativi di autenticazione / flussi concessi che per il resto degli MVPD.

* **AuthN per requestorID**: Comcast non consente di memorizzare nella cache lo stato AuthN da un requestor ID a un altro. Per questo motivo, ogni sito/app deve andare a Comcast per ottenere un token di autenticazione. Oltre a considerazioni sull’esperienza, l’impatto, come sopra, è che verranno generati più tentativi di autenticazione/eventi concessi.

* **Autenticazione passiva**: Per migliorare l’esperienza utente ma mantenere comunque la funzionalità AuthN per requestorID, in un iFrame nascosto si verifica un flusso di autenticazione passiva. L’utente non vedrà nulla, ma gli eventi verranno comunque attivati come prima.

Se l&#39;utente fa clic su &quot;Ricorda utente&quot; nella pagina di accesso Comcast, le successive visite a questa pagina (in un periodo di 2 settimane) saranno solo un rapido reindirizzamento indietro. In caso contrario, gli utenti dovranno eseguire l’autenticazione sulla pagina.

### Autenticazione non riuscita {#unsuccessful-authentication}

Un’autenticazione non riuscita non è un evento per sé nell’autenticazione Adobe Primetime, ma può essere calcolata come differenza tra tentativi e successi.

Nella versione di maggio 2013, l’autenticazione Adobe Primetime aggiungerà codici di errore per le autenticazioni non riuscite a causa di errori di sistema o di rete, inclusi gli errori DRM (binding token non riuscito) e gli errori LSO (nessuno spazio per scrivere il token, ecc.).

### Tasso di conversione autenticazione {#authenitication-conversion-rate}

Una metrica interessante che i programmatori possono monitorare è il tasso di conversione di autenticazione, calcolato come (richieste AuthN / AuthN concesse)%.

Alcune note sulle metriche:

* Poiché si tratta di una metrica basata su eventi, non riflette in realtà il tasso di conversione dell’utente univoco - se un utente tenta otto volte e riesce la nona volta - questo si rifletterà molto male nel tasso di conversione di cui sopra.
* Nell’autenticazione Adobe Primetime (lato server) non è ancora possibile calcolare una conversione di autenticazione basata univoca.
* Se nel sito o nell’app sono presenti nuovi tentativi automatici di autenticazione, anche la metrica riportata sopra risulterà distorta.

## Eventi di autorizzazione {#authorization_events}

### Tentativo di autorizzazione {#authorization_attempt}

Oltre a ottenere un token di autenticazione, gli utenti devono anche ottenere un token di autorizzazione prima di riprodurre il contenuto. Questo di solito accade dopo l’autenticazione, o se il token di autorizzazione scade. Poiché questo controllo viene eseguito sul lato server (dai server di autenticazione Adobe Primetime ai server MVPD), l’utente non è tenuto a eseguire alcuna operazione.

### Autorizzazione concessa {#authorization-granted}

Una &quot;autorizzazione concessa&quot; segnala che la sottoscrizione dell&#39;utente autenticato include la programmazione richiesta.

Si noti che non tutti gli MVPD supportano una fase di autorizzazione separata; per alcuni l&#39;autenticazione è equiparata all&#39;autorizzazione. L’MVPD invia l’autenticazione Adobe Primetime una risposta corretta alla richiesta AuthZ del canale posteriore, mentre l’autenticazione Adobe Primetime crea un token AuthZ.

* Il token AuthZ viene memorizzato nella cache per un periodo di tempo, in genere 24 ore Durante questo periodo non verrà attivato alcun evento AuthZ.
* Alcuni MVPD funzionano con le autorizzazioni a livello di risorsa, altri con le autorizzazioni a livello di canale; - a seconda di quale viene utilizzato, vengono attivati più o meno eventi AuthZ. Anche per l’autorizzazione a livello di canale, la memorizzazione in cache è attiva, quindi se la stessa risorsa viene richiesta in meno di 24 ore, non verrà attivato alcun evento.

### Autorizzazione negata {#authorization-denied}

Se un&#39;autorizzazione viene negata, l&#39;utente autenticato non dispone di un abbonamento confermato alla programmazione richiesta. La causa più probabile è che il canale non fa parte del pacchetto di abbonamento dell&#39;utente, ma questo può anche riflettere un utente che ha solo accesso a Internet dall&#39;MVPD.

Per alcuni MVPD, gli utenti sono autenticati correttamente anche se hanno solo un abbonamento a Internet dal MVPD (nessun abbonamento a pay TV). In questo caso, anche se il canale per il quale l&#39;utente richiede l&#39;autorizzazione è incluso nel pacchetto di base, l&#39;autorizzazione verrà negata.

Alcuni MVPD offrono messaggi di errore personalizzati per le negazioni di AuthZ che possono includere offerte per aggiornare il loro pacchetto.


### Tasso di conversione autorizzazione {#authorization-conversion-rate}

Il tasso di conversione di autenticazione può essere calcolato come (richieste AuthZ / AuthZ concesse)%.

### Richiesta di riproduzione riuscita {#successful-play-request}

Un utente autenticato e autorizzato può visualizzare contenuto protetto.

Quando una richiesta di riproduzione ha esito positivo, Adobe Primetime Authentication genera un Media Token di breve durata affermando che l&#39;utente ha il diritto di visualizzare il video richiesto. Il programmatore utilizza questo token multimediale per un&#39;ulteriore convalida del potenziale visualizzatore. I token multimediali vengono tracciati come richieste di riproduzione riuscite.

* L&#39;autenticazione Adobe Primetime *not* controlla se la riproduzione del video è effettivamente iniziata dopo la generazione del token multimediale. Ad esempio, se esiste una restrizione geografica del contenuto, la transazione continua a conteggiare come una richiesta di riproduzione corretta, anche se il flusso non inizia in realtà.
* Poiché i token AuthN e AuthZ memorizzano nella cache la risposta MVPD per un periodo di tempo, l’evento di richiesta di riproduzione riuscito è l’evento più frequente nelle metriche.

## Utenti univoci {#unique-users}

### Definizione {#definition}

Dopo un’autenticazione riuscita, l’autenticazione Adobe Primetime tiene traccia dell’esistenza di un utente univoco, in base al valore restituito dall’ID utente MVPD.  Questo valore si basa sulle informazioni di accesso dell’utente, ma non contiene informazioni identificabili in modo personalizzabile.

Questo valore viene passato anche al sito/app nel callback sendTrackingData .

Questo valore può essere persistente tra i dispositivi (l&#39;MVPD produce lo stesso valore per un determinato utente, indipendentemente da dove avviene l&#39;accesso) o transitorio (per ogni accesso, viene generato un nuovo valore, che l&#39;MVPD mappa nel suo back-end. In genere i valori forniti dagli MVPD all’autenticazione Adobe Primetime sono costanti nelle sessioni e nei dispositivi, ma, come rilevato, la persistenza non è né garantita né convalidata.

Questo valore viene utilizzato come metodo di calcolo per gli utenti univoci. Il valore riportato (per ID/intervallo/MVPD del richiedente) viene deduplicato per il particolare intervallo. Quindi la somma degli utenti univoci al giorno è solitamente diversa dal valore mensile, con il valore mensile con il valore più basso.

Questo numero include tutti gli eventi dall&#39;autenticazione Adobe Primetime, meno i tentativi di autenticazione (che non hanno un ID utente) ma include le autorizzazioni tentate (e possibilmente non riuscite).

### Esempi {#examples}

#### Giorno 1 {#day1}

L&#39;utente XYZ va sul sito per guardare un video.

Eventi attivati:

* Tentativo di autenticazione (non ancora un utente univoco)
* AuthN concesso
   * a questo punto identifichiamo in modo univoco l&#39;utente in base a ciò che restituisce l&#39;MVPD - così il conteggio giornaliero degli utenti univoci viene aumentato di 1
   * il token AuthN viene memorizzato nella cache per 30 giorni
* Tentativo di AuthZ / evento concesso
   * Token AuthZ memorizzato nella cache per 1 giorno
* Evento di richiesta di riproduzione riuscito

#### Giorno 1 (successivo) {#day1-later-on}

L&#39;utente XYZ guarda un altro video.

Eventi attivati:

* Evento di richiesta di riproduzione riuscito (gli altri sono memorizzati nella cache)
* Nessun aumento di univoci giornaliere o mensili

#### Giorno 3 {#day3}

L&#39;utente XYZ guarda un altro video.

Eventi attivati:

* Tentativo di AuthZ / evento concesso
   * Dal 1 giorno 1 la memorizzazione in cache dal giorno 1 è scaduta
* Evento di richiesta di riproduzione riuscito (gli altri sono memorizzati nella cache)
* Gli utenti unici giornalieri sono aumentati di 1 unità al mese e gli unici sono ancora 1

#### Giorno 31 {#day31}

L&#39;utente XYZ guarda un altro video.

Come nel giorno 1, dal momento che la memorizzazione in cache di AuthN è scaduta.

Se lo stesso utente dovesse non riuscire ad autorizzare, il conteggio mensile degli utenti univoci verrebbe comunque aumentato di 1 perché ci sono due eventi che contengono l&#39;ID utente: l&#39;autenticazione concessa e il tentativo di autorizzazione.

### Single Sign-On (SSO) {#single-sign-on-sso}

In alcuni casi, il numero di utenti univoci può essere maggiore del numero di autenticazioni riuscite. Questo è solitamente il caso in cui molti utenti arrivano tramite SSO da altri siti/app e hanno solo bisogno di ottenere l&#39;autorizzazione sul sito/app corrente.

### Confronto tra utenti univoci lato client e lato server {#comparing-client-side-and-server-side-unique-users}

Se il valore ID utente da `sendTrackingData()` viene utilizzato sul lato client per contare gli utenti univoci e i numeri lato client e lato server devono corrispondere.

Se le differenze sono importanti, i motivi che seguono di solito sono la differenza:

* I video giocano a pezzi unici rispetto a tutti gli eventi unici. Come accennato, l’autenticazione di Adobe Primetime conta utenti univoci per tutti gli eventi eccetto i tentativi di AuthN. Ciò significa che se l’utente si autentica solo (sulla pagina) ma non visualizza un video, viene comunque attivato un aumento univoco del conteggio degli utenti.

* Conteggio degli utenti che non hanno ottenuto l’autorizzazione - L’autenticazione Adobe Primetime conta anche questi utenti nel numero riportato.

<!--
## Related Information {#related-information}

- [Entitlement Service Monitoring API](/help/authentication/entitlement-service-monitoring-api.md)

-->