---
title: Accesso e disconnessione senza aggiornamento
description: Accesso e disconnessione senza aggiornamento
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1772'
ht-degree: 0%

---


# Accesso e disconnessione senza aggiornamento {#tefresh-less-login-and-logout}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Panoramica {#overview}

Per le applicazioni web, è necessario tenere conto di alcuni scenari possibili per l&#39;autenticazione e la disconnessione degli utenti.  Gli MVPD richiedono che gli utenti accedano alla pagina web dell&#39;MVPD per l&#39;autenticazione, con i seguenti fattori aggiuntivi in arrivo:

- Alcuni MVPD richiedono un reindirizzamento completo dal sito alla pagina di accesso
- Alcuni MVPD richiedono l&#39;apertura di un iFrame sul sito per visualizzare la pagina di login del MVPD
- Alcuni browser non gestiscono bene lo scenario iFrame, quindi per quei browser un&#39;alternativa migliore è quella di utilizzare una finestra a comparsa invece dell&#39;iFrame

Prima di Adobe Primetime authentication 2.7, tutti questi scenari per l&#39;autenticazione di un utente includevano un aggiornamento completo della pagina del programmatore.Per la versione 2.7 e successive, il team di autenticazione di Adobe Primetime ha migliorato questi flussi in modo che l&#39;utente non debba effettuare un aggiornamento della pagina sull&#39;app durante l&#39;accesso e la disconnessione.  


## Descrizione dettagliata {#detailed_description}

Cominciamo con un riepilogo dei flussi di autenticazione e logout originali, quindi seguiamolo con i flussi di autenticazione e logout migliorati. Nota che le prime quattro sezioni riguardano gli MVPD normali (non TempPass), mentre l&#39;ultima sezione descrive l&#39;implementazione speciale che deve essere applicata per TempPass:

- [Flusso di autenticazione originale](#orig_authn)
- [Flusso di disconnessione originale](#orig_logout)
- [Flusso di autenticazione migliorato](#improved_authn)
- [Flusso di disconnessione migliorato](#improved_logout)
- [Flusso TempPass](#improved_temppass)

</br>

## Flussi di autenticazione/disconnessione originali {#orig_authn}

**Autenticazione**

I client web di autenticazione Adobe Primetime hanno due modi di autenticazione, a seconda dei requisiti degli MVPD:

1. **Reindirizzamento a pagina intera -** Dopo che l&#39;utente seleziona un provider (configurato con reindirizzamento a pagina intera) dal selettore MVPD sul sito web del programmatore, `setSelectedProvider(<mvpd>)` viene richiamato su AccessEnabler e l&#39;utente viene reindirizzato alla pagina di accesso di MVPD. Dopo che l&#39;utente fornisce credenziali valide viene reindirizzato al sito web del programmatore. AccessEnabler viene inizializzato e il token di autenticazione viene recuperato dall&#39;autenticazione Adobe Primetime durante `setRequestor`.
1. **Finestra iFrame / Popup -** Dopo che l&#39;utente seleziona un provider (configurato con iFrame), `setSelectedProvider(<mvpd>)` viene richiamato in AccessEnabler. Questa azione attiverà la `createIFrame(width, height)` callback, notificando al programmatore di creare un iFrame (o popup - a seconda del browser/preferenze) con il nome `"mvpdframe"` e le dimensioni fornite. Dopo la creazione dell&#39;iFrame/popup, AccessEnabler carica la pagina di accesso di MVPD nell&#39;iFrame/popup. L&#39;utente fornisce credenziali valide e l&#39;iFrame/popup viene reindirizzato all&#39;autenticazione Adobe Primetime, che restituisce un frammento JS che chiude l&#39;iFrame/popup e ricarica la pagina padre (sito web programmatore). Analogamente al flusso 1, il token di autenticazione viene recuperato durante `setRequestor`. 

La `displayProviderDialog` callback (attivato da `getAuthentication`/`getAuthorization`) restituisce un elenco di MVPD e le relative impostazioni appropriate. La `iFrameRequired` la proprietà di un MVPD consente al programmatore di sapere se deve attivare il flusso 1 o il flusso 2. Tieni presente che il programmatore è tenuto a intraprendere azioni extra (creazione di un iFrame/popup) solo per il flusso 2.

**Annulla autenticazione**

C&#39;è anche la situazione in cui l&#39;utente annulla esplicitamente il flusso di autenticazione chiudendo la pagina di accesso. Ecco gli scenari e la soluzione proposta ai programmatori:

1. **Reindirizzamento a pagina intera -** Quando la pagina di accesso viene chiusa, l&#39;utente dovrà navigare nuovamente sul sito web del programmatore e avviare l&#39;intero flusso dall&#39;inizio. In questo scenario non è richiesta alcuna azione esplicita da parte del programmatore.
1. **iFrame -** Si consiglia al programmatore di ospitare l&#39;iFrame all&#39;interno di un `div` (o un componente simile dell’interfaccia utente) a cui è associato un pulsante Chiudi . Quando l&#39;utente preme il pulsante Chiudi, il programmatore distruggerà l&#39;iFrame insieme all&#39;interfaccia utente associata ed eseguirà `setSelectedProvider(null)`. Questa chiamata consente ad AccessEnabler di cancellare il proprio stato interno e consente all&#39;utente di avviare un flusso di autenticazione successivo. `setAuthenticationStatus` e `sendTrackingData(AUTHENTICATION_DETECTION...)` verrà attivato per segnalare un flusso di autenticazione non riuscito (entrambi attivati `getAuthentication` e `getAuthorization`).
1. **Popup -** Alcuni browser non sono in grado di rilevare con precisione l’evento di chiusura della finestra, pertanto è necessario adottare un approccio diverso (a differenza del flusso iFrame di cui sopra). L&#39;Adobe consiglia al programmatore di inizializzare un timer che verifichi periodicamente l&#39;esistenza della finestra a comparsa di accesso. Se la finestra non esiste, il programmatore può essere sicuro che l&#39;utente abbia annullato manualmente il flusso di accesso e il programmatore può procedere con la chiamata `setSelectedProvider(null)`. I callback attivati sono gli stessi del precedente flusso 2.

</br>

## Flusso di disconnessione originale {#orig_logout}

L&#39;API di logout di AccessEnabler cancella lo stato locale della libreria e carica l&#39;URL di logout di MVPD nella scheda/finestra corrente. Il browser passa all&#39;endpoint di logout dell&#39;MVPD e, una volta completato il processo, l&#39;utente viene reindirizzato al sito web del programmatore. L’unica azione necessaria per conto dell’utente consiste nel premere il pulsante/collegamento di disconnessione e avviare il flusso; non è richiesta alcuna interazione da parte dell’utente sull’endpoint di logout dell’MVPD.

**Flusso di autenticazione/disconnessione originale con aggiornamento pagina**

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/AE_with_refresh_web.png)

</br>

## Autenticazione migliorata (senza aggiornamento) {#improved_authn}

>[!NOTE]
>
>I migliori flussi di accesso e logout senza aggiornamento richiedono che il browser supporti le moderne tecnologie HTML5, inclusa la messaggistica web.

I flussi di autenticazione (accesso) e di logout descritti in precedenza forniscono un’esperienza utente simile ricaricando la pagina principale al termine di ogni flusso.  La funzione corrente ha lo scopo di migliorare l’esperienza utente fornendo accesso e disconnessione senza aggiornamento (in background). Il programmatore può abilitare/disabilitare l&#39;accesso in background e il logout passando due flag booleani (`backgroundLogin` e `backgroundLogout`) al `configInfo` del `setRequestor` API. Per impostazione predefinita, l’accesso/logout in background è disattivato (questo fornisce compatibilità con l’implementazione precedente).

**Esempio:**

```JSON
    var configInfo = {
        callSetConfig: true,
        backgroundLogin: true,
        backgroundLogout: true
    };
    accessEnabler.setRequestor(REQUESTOR_ID, null, configInfo);
```

**Autenticazione**

I punti seguenti descrivono la transizione tra i flussi di autenticazione originali e i flussi migliorati:

1. Il reindirizzamento a pagina intera viene sostituito da una nuova scheda del browser in cui viene eseguito l’accesso MVPD. Il programmatore è tenuto a creare una nuova scheda (tramite `window.open`) denominata `mvpdwindow` quando l&#39;utente seleziona un MVPD (con `iFrameRequired = false`). Il programmatore esegue quindi `setSelectedProvider(<mvpd>)`, che consente ad AccessEnabler di caricare l&#39;URL di accesso MVPD nella nuova scheda. Dopo che l&#39;utente fornisce credenziali valide, Adobe Primetime Authentication chiuderà la scheda e invierà un window.postMessage al sito web del programmatore che segnala ad AccessEnabler che il flusso di autenticazione è terminato. Vengono attivati i seguenti callback:

   - Se il flusso è stato avviato da `getAuthentication`: `setAuthenticationStatus` e `sendTrackingData(AUTHENTICATION_DETECTION...)` verrà attivato per segnalare l&#39;autenticazione riuscita/non riuscita.

   - Se il flusso è stato avviato da `getAuthorization`: `setToken/tokenRequestFailed` e `sendTrackingData(AUTHORIZATION_DETECTION...)` verrà attivato per segnalare l&#39;esito positivo o negativo dell&#39;autorizzazione.

1. Il flusso della finestra iFrame/popup rimane sostanzialmente invariato, con la differenza che dopo che l&#39;utente fornisce credenziali valide, la pagina padre non verrà ricaricata. L&#39;iFrame/popup si chiude automaticamente dopo l&#39;accesso e un `window.postMessage` viene inviato alla pagina padre, notificando ad AccessEnabler che il flusso è terminato. Gli stessi callback vengono attivati come nel flusso precedente, **più il seguente nuovo callback: `destroyIFrame`**. La `destroyIFrame` callback consente al programmatore di rimuovere eventuali componenti associati/ausiliari di iFrame, come le decorazioni dell&#39;interfaccia utente. L&#39;esistenza di questo callback non era necessaria nel vecchio flusso di autenticazione perché al termine dell&#39;accesso, l&#39;autenticazione Adobe Primetime ricaricava la pagina del programmatore, distruggendo così tutti i componenti dell&#39;interfaccia utente su di essa.

</br>     

>[!IMPORTANT]
> 
>È necessario caricare l&#39;iFrame di accesso MVPD o la finestra popup come elemento figlio diretto della pagina che contiene l&#39;istanza AccessEnabler. Se l&#39;iFrame di accesso MVPD o la finestra popup è nidificata due o più livelli sotto la pagina contenente l&#39;istanza AccessEnabler, il flusso potrebbe bloccarsi. Ad esempio, se avevi un iFrame situato tra la pagina principale e l’iFrame MVPD (Pagina =\> iFrame =\> MVPD iFrame), il flusso di accesso potrebbe non riuscire.

</br>

 **Annulla autenticazione**

Questi sono i flussi per annullare l’autenticazione:

1. **Scheda Browser -** Poiché la scheda è fondamentalmente una nuova finestra, l’acquisizione del relativo evento di chiusura ha le stesse limitazioni di cui allo scenario 3 dei vecchi flussi di autenticazione. Inoltre, l&#39;approccio del timer non è possibile in questo caso, perché non c&#39;è modo di distinguere tra una scheda che è stata chiusa manualmente dall&#39;utente e una scheda che è stata chiusa automaticamente alla fine del flusso di accesso. La soluzione è che AccessEnabler rimanga &#39;silenzioso&#39; (non vengono attivati callback) quando l&#39;utente annulla il flusso. Inoltre, il programmatore non è tenuto ad intraprendere alcuna azione specifica. L&#39;utente sarà in grado di avviare un altro flusso di autenticazione senza ricevere l&#39;errore &quot;Errore più richieste di autenticazione&quot; (questo errore è stato disabilitato in AccessEnabler per l&#39;accesso in background).

1. **iFrame -** Il programmatore può adottare l&#39;approccio discusso nello scenario 2 dai vecchi flussi di autenticazione (creare l&#39;interfaccia wrapper dall&#39;iFrame e il pulsante Chiudi associato che attiva `setSelectedProvider(null)`. Anche se questo approccio non è più un requisito importante (i flussi di autenticazione multipli sono consentiti per l’accesso in background, come discusso nello scenario 1 di cui sopra), è comunque consigliato dall’Adobe.

1. **Popup -** Questo è identico al flusso della scheda Browser qui sopra.

</br>

## Flusso di disconnessione migliorato {#improved_logout}

Il nuovo flusso di logout verrà eseguito in un iFrame nascosto, eliminando in tal modo il reindirizzamento a pagina intera.  Questo è possibile perché l&#39;utente non deve intraprendere azioni specifiche sulla pagina di logout dell&#39;MVPD.

Al termine del flusso di logout, reindirizzerà l’iFrame a un endpoint di autenticazione Adobe Primetime personalizzato. Servirà un frammento JS che esegue un `window.postMessage` all&#39;elemento padre, notificando ad AccessEnabler che la disconnessione è completa. Vengono attivati i seguenti callback: `setAuthenticationStatus()` e `sendTrackingData(AUTHENTICATION_DETECTION ...)`, segnalando che l’utente non è più autenticato. 

L&#39;illustrazione seguente mostra il flusso di aggiornamento che consente a un utente di accedere al proprio MVPD senza aggiornare la pagina principale dell&#39;applicazione:

**Miglioramento (senza aggiornamento) dell’autenticazione / Flusso di disconnessione**

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/AE_with_no_refresh_web.png)

</br>

## Flusso TempPass {#improved_temppas}

L&#39;accesso senza aggiornamento segue un approccio diverso per gli MVPD di tipo TempPass.

Poiché il flusso TempPass richiede che una finestra venga creata automaticamente e chiusa senza un&#39;esplicita interazione dell&#39;utente, potrebbe causare problemi ad alcuni browser (popup blocker). Pertanto, AccessEnabler implementa la fase di login dietro le quinte, senza richiedere un contenitore Web creato dal programmatore.

Di seguito sono riportati gli aspetti di cui il programmatore deve essere a conoscenza durante l&#39;implementazione di TempPass per l&#39;accesso e l&#39;logout senza aggiornamento:

- Prima di avviare l&#39;autenticazione, è necessario creare l&#39;iFrame o la finestra popup solo per gli MVPD non TempPass. Il programmatore può rilevare se un MVPD è TempPass o meno leggendo il `tempPass` dell&#39;oggetto MVPD (restituito da `setConfig()` / `displayProviderDialog()`).

- La `createIFrame()` il callback deve contenere un controllo per TempPass ed eseguirne la logica solo quando MVPD NON è TempPass.

- La `destroyIFrame()` il callback deve contenere un controllo per TempPass ed eseguirne la logica solo quando MVPD NON è TempPass.

- La `setAuthenticationStatus()` e `sendTrackingData()` i callback vengono richiamati al termine dell&#39;autenticazione (esattamente come nel flusso Refresh-less per gli MVPD normali).

>[!NOTE]
>
>Questo flusso è disponibile solo per l&#39;aggiornamento di TempPass. Per il flusso di aggiornamento, TempPass deve essere gestito esplicitamente (quando TempPass richiede iFrame / popup)

</br>

L&#39;esempio di codice seguente illustra come gestire una finestra MVPD sul sito web di un programmatore (sia per MVPD normali che per TempPass):

```javascript
    var aeHostname = "https://entitlement.auth.adobe.com";
    var mvpdWindow = null;
    var mvpd = <mvpd_object_from_displayProviderDialog>;
    var useIframeLogin = <boolean_depending_on_browser_or_Programmer_preferences>;
    var backgroundLogin = <boolean_depending_on_Programmer_preferences>;
     
    // Do not create any windows for refreshless and temp pass
    if (!(backgroundLogin && mvpd.tempPass)) {
        if (backgroundLogin && !mvpd.popup) {
            mvpdWindow = window.open(aeHostname, "mvpdwindow");
        } else if (mvpd.popup && !useIframeLogin) {
            var width = mvpd.width;
            var height = mvpd.height;
            // Center on screen
            var top = (document.all) ? window.screenTop : window.screenY + 100;
            var left = (document.all) ? window.screenLeft : window.screenX + window.innerWidth / 2 - width / 2;
        
            mvpdWindow = window.open(aeHostname, "mvpdframe",
                           "width=" + width + ",height=" + height + ",top=" + top + ",left=" + left);
            // Monitor the mvpd popup for close
            if (!backgroundLogin) {
                clearInterval(cancelTimer);
                cancelTimer = setInterval(function () {
                    if (mvpdWindow && mvpdWindow.closed) {
                        clearInterval(cancelTimer);
                        $('#mvpddiv').hide();
                        accessEnablerAPI.setSelectedProvider(null);
                    }
                }, 200);
            }
        }
    }
```

