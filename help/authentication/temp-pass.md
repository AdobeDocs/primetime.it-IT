---
title: Passaggio temporaneo
description: Passaggio temporaneo
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2210'
ht-degree: 0%

---


# Passaggio temporaneo {#temp-pass}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Riepilogo delle funzioni {#tempass-featur-summary}

Temp Pass consente ai programmatori di offrire accesso temporaneo al loro contenuto protetto, per gli utenti che non hanno credenziali account con un MVPD.  Temp Pass include le seguenti funzionalità:

* È possibile configurare il passaggio temporaneo per fornire un accesso temporaneo a una serie di scenari, tra cui:
   * Un programmatore può offrire un&#39;anteprima giornaliera e breve (ad es. un&#39;anteprima di 10 minuti) di uno dei propri siti.
   * Un programmatore può offrire una presentazione singola e lunga (ad esempio, quattro ore) di un importante evento sportivo come le Olimpiadi, o NCAA March Madness.
   * Un programmatore può fornire una combinazione dei due scenari precedenti; ad esempio, un periodo di visualizzazione iniziale più lungo di un giorno, seguito da una serie di periodi brevi che ripetono quotidianamente per alcuni giorni successivi.
* I programmatori specificano la durata (Time-To-Live o TTL) del loro Temp Pass.
* Il passaggio temporaneo funziona per richiedente.  Ad esempio, NBC potrebbe impostare un Temp Pass di 4 ore per il richiedente &quot;NBCOlympics&quot;.
* I programmatori possono reimpostare tutti i token concessi a un particolare richiedente.  L&#39;&quot;MVPD temporaneo&quot; utilizzato per implementare il passaggio temporaneo deve essere configurato con l&#39;opzione &quot;Authentication Per Requestor&quot; abilitata.
* **L&#39;accesso Temp Pass è concesso ai singoli utenti su dispositivi specifici**. Dopo la scadenza dell&#39;accesso a Temp Pass per un utente, tale utente non sarà in grado di ottenere l&#39;accesso temporaneo sullo stesso dispositivo fino alla scadenza di tale utente [token di autorizzazione](/help/authentication/glossary.md#authz-token) è cancellato dal server di autenticazione di Adobe Primetime.


>[!NOTE]
>
>Temp Pass fa parte del pacchetto Premium Workflow. Per utilizzare questa funzionalità, contatta il tuo rappresentante commerciale Primetime .

## Dettagli delle funzioni {#tempass-featur-details}

* **Calcolo del tempo di visualizzazione** - Il tempo di validità di un passaggio Temp non è correlato al tempo impiegato dall&#39;utente per la visualizzazione del contenuto nell&#39;applicazione del programmatore.  Alla richiesta iniziale di autorizzazione dell&#39;utente tramite Temp Pass, viene calcolato un tempo di scadenza aggiungendo il tempo iniziale di richiesta corrente al TTL specificato dal programmatore. Questo tempo di scadenza è associato all&#39;ID dispositivo dell&#39;utente e al relativo ID programmatore e memorizzato nel database di autenticazione di Primetime. Ogni volta che l&#39;utente prova ad accedere al contenuto utilizzando Temp Pass dallo stesso dispositivo, l&#39;autenticazione Primetime confronterà il tempo di richiesta del server con il tempo di scadenza associato all&#39;ID dispositivo dell&#39;utente e al relativo ID. Se il tempo di richiesta del server è inferiore al tempo di scadenza, l’autorizzazione sarà concessa; in caso contrario, l&#39;autorizzazione verrà negata.
* **Parametri di configurazione** - I seguenti parametri Temp Pass possono essere specificati da un programmatore per creare una regola Temp Pass:
   * **TTL token** - Il tempo che un utente può osservare senza accedere a un MVPD. Questa ora è basata sull’orologio e scade se l’utente sta visualizzando o meno il contenuto.
   >[!NOTE]
   >A un requestor ID non può essere associata più di una regola Temp Pass .
* **Autenticazione/autorizzazione** - Nel flusso di passaggio Temp, specificare l&#39;MVPD come &quot;Passo Temp&quot;.  L’autenticazione di Primetime non comunica con un MVPD effettivo nel flusso di passaggio Temp, pertanto l’MVPD &quot;Temp Pass&quot; autorizza qualsiasi risorsa. I programmatori possono specificare una risorsa accessibile tramite Temp Pass come per il resto delle risorse sul loro sito. La libreria Media Verifier può essere utilizzata come di consueto per verificare il token per contenuti multimediali brevi Temp Pass e per applicare il controllo delle risorse prima della riproduzione.
* **Tracciamento dei dati nel flusso di passaggio temporaneo** - Due punti relativi ai dati di tracciamento durante un flusso di adesione di Temp Pass:
   * L&#39;ID di tracciamento passato dall&#39;autenticazione Primetime al tuo **sendTrackingData()** callback è un hash dell&#39;ID dispositivo.
   * Poiché l’ID MVPD utilizzato nel flusso di passaggio temporaneo è &quot;Temp Pass&quot;, lo stesso ID MVPD viene passato a **sendTrackingData()**. La maggior parte dei programmatori preferirà trattare le metriche Temp Pass in modo diverso rispetto alle metriche MVPD effettive. Questo richiede un ulteriore lavoro nell’implementazione di Analytics.

L&#39;illustrazione seguente mostra il flusso del passaggio temporaneo:

![Flusso di passaggio temporaneo](assets/temp-pass-flow.png)

*Figura: Flusso di passaggio temporaneo*

## Implementare il passaggio temporaneo {#implement-tempass}

Sul lato dell&#39;autenticazione Primetime, Temp Pass è implementato con l&#39;aggiunta di uno pseudo-MVPD denominato &quot;TempPass&quot; alla configurazione server del programmatore partecipante.  Questo pseudo-MVPD agisce come un MVPD effettivo che concede temporaneamente l&#39;accesso al contenuto protetto del programmatore.

Dal lato del programmatore, Temp Pass è implementato come segue per i due scenari che gli MVPD usano per l&#39;autenticazione:

* **iFrame sulla pagina del programmatore**. Temp Pass funziona indipendentemente dal tipo di autenticazione di un MVPD, ma per lo scenario iFrame sono necessari passaggi aggiuntivi per annullare il flusso di autenticazione corrente e autenticarsi con Temp Pass. Questi passaggi vengono visualizzati nella [Accesso iFrame](/help/authentication/temp-pass.md) sotto.
* **Reindirizza alla pagina di accesso MVPD**. Nel caso più tradizionale in cui l&#39;interfaccia utente per attivare il Passo Temp viene presentata prima di avviare l&#39;autenticazione con un MVPD, non ci sono passi speciali da fare. Temp Pass dovrebbe essere trattato come un MVPD normale.

I seguenti punti si applicano a entrambi gli scenari di implementazione:

* Nel selettore MVPD dovrebbe essere visualizzato &quot;Temp Pass&quot; solo per gli utenti che non hanno ancora richiesto un&#39;autorizzazione Temp Pass. Il blocco della visualizzazione per le richieste successive può essere ottenuto mantenendo un flag sui cookie. Questo funzionerà purché l’utente non cancelli la cache del browser. Se gli utenti cancellano le cache del browser, nel selettore viene visualizzato di nuovo &quot;Temp Pass&quot; e l&#39;utente potrà richiederlo nuovamente. L&#39;accesso sarà concesso solo se il tempo &quot;Temp Pass&quot; non è ancora scaduto.
* Quando un utente richiede l&#39;accesso tramite Temp Pass, il server di autenticazione Primetime non eseguirà la consueta richiesta di Security Assertion Markup Language (SAML) durante il processo di autenticazione. Al contrario, l’endpoint di autenticazione restituisce il successo ogni volta che viene richiamato mentre i token sono validi per il dispositivo.
* Quando scade un passaggio Temp, il relativo utente non verrà più autenticato, perché nel passaggio Temp passa il token di autenticazione e il token di autorizzazione hanno la stessa data di scadenza. Per spiegare agli utenti che il loro Temp Pass è scaduto, i programmatori devono recuperare il MVPD selezionato subito dopo aver chiamato `setRequestor()`, quindi chiama `checkAuthentication()` come al solito. In `setAuthenticationStatus()` callback è possibile eseguire un controllo per determinare se lo stato di autenticazione è 0, in modo che se l&#39;MVPD selezionato era &quot;TempPass&quot; sia possibile presentare agli utenti un messaggio che indica che la loro sessione Temp Pass è scaduta.
* Se un utente elimina il token Temp Pass prima della scadenza, i successivi controlli di adesione genereranno un token che avrà un TTL uguale al tempo rimanente.
* Se dopo la scadenza l&#39;utente elimina il token Temp Pass , i successivi controlli di adesione restituiranno &quot;utente non autorizzato&quot;.

Vedi i campioni in [Codice di esempio](/help/authentication/temp-pass.md#tempass-sample-code) di seguito sono riportati alcuni esempi su come codificare i dettagli di implementazione descritti in questa sezione.

## Codice di esempio {#tempass-sample-code}

Le sezioni seguenti mostrano come chiamare l&#39;API di autenticazione Primetime per implementare il flusso Temp Pass:

* [Esempio di accesso iFrame](/help/authentication/temp-pass.md#iframe-login-sample)
* [Esempio di accesso automatico](/help/authentication/temp-pass.md#auto-login-sample)

### Esempio di accesso iFrame {#iframe-login-sample}

Questo esempio mostra come implementare Temp Pass per il caso in cui gli MVPD supportano l&#39;integrazione iFrame:

```HTML
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"
        "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
    <title>Temp Pass Sample</title>
    <script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.min.js"></script>
    <script type="text/javascript" src="https://raw.github.com/carhartl/jquery-cookie/master/jquery.cookie.js"></script>
    <script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/swfobject/2.2/swfobject.js"></script>
 
    <script type="text/javascript">
        var ae, ifrm, providersMenu, previousSelectedProvider;
        var tempassSelected = false;
 
        $(document).ready(function() {
            ifrm = $('#ifrm');
            swfobject.embedSWF("http://entitlement.auth.adobe.com/entitlement/AccessEnablerDebug.swf"
                    , "ae", "1", "1", "11.0.0", "expressinstall.swf", {}
                    , {wmode: "transparent", allowScriptAccess: "always"}
                    , {id: "accessEnabler", name: "accessEnabler"});
        });
 
        function swfLoaded() {
            ae = $('#accessEnabler')[0];
            ae.setProviderDialogURL("none");
            ae.setRequestor("sample_requestor_Id");
            previousSelectedProvider = ae.getSelectedProvider(); 
            ae.checkAuthentication();
        }
 
        function createIFrame() {
            providersMenu.hide();
 
            // If the user already used TempPass once, hide the button
            if ($.cookie("TPSelected") == "1"){
                $('#tempassBtn').hide();
            }
            ifrm.show();
        }
 
        function displayProviderDialog(providers) {
            if (tempassSelected) {
                // Remember in a cookie that the user selected temp pass
                $.cookie("TPSelected", "1", {expires: 366, path: '/'});
 
                // Authenticate with temp pass
                ae.setSelectedProvider("TempPass");
            } else {
                $('#loginBtn').hide();
                providersMenu = $('<select></select>');
 
                providersMenu.change(function(event){
                    ae.setSelectedProvider(event.target.value);
                });
 
                $.each(providers, function(k, v) {
                    // Add the MVPDs to the menu while making
                    //   sure that the Temp Pass entry is skipped
                    if(v.ID != "TempPass") {
                        providersMenu.append($('<option></option>', {value:v.ID}).text(v.displayName));                       
                    }
                });
                $('body').append(providersMenu);
            }
        }
 
        function setAuthenticationStatus(status, code) {
            loginBtn = $('#loginBtn');
            logoutBtn = $('#logoutBtn');
            console.log(previousSelectedProvider);
 
            if (status == 1) {
                $('#selectedProvider').text("Authenticated with " + ae.getSelectedProvider().MVPD + "   ");
                loginBtn.hide();
                logoutBtn.show();
 
                // Get authorization
                ae.getAuthorization("sample_requestor_Id");
            } else {
                // If selected provider is TempPass but the user is not authenticated,
                //   infer that the TempPass period has expired, so reset the MVPD selection
                if (previousSelectedProvider && previousSelectedProvider.MVPD == "TempPass") {
                    previousSelectedProvider = null;
                    ae.setSelectedProvider(null);
                    alert("Your Temp Pass has expired, please login with your regular cable provider!");
                }
                loginBtn.show();
                logoutBtn.hide();
            }
        }
 
        function selectTempPass() {
            ifrm.hide();
 
            // Signal the fact that the user selected temp pass
            tempassSelected = true;
 
            // Cancel the current authentication flow
            ae.setSelectedProvider(null);
 
            // Retry authentication
            ae.getAuthentication();
 
        }
    </script>
</head>
<body>
    <button id="loginBtn" style="display: none" onclick="ae.getAuthentication();">Login</button>
    <label id="selectedProvider" for="logoutBtn"></label><button id="logoutBtn"
           style="display: none" onclick="ae.logout()">Logout</button>
    <div id="ifrm"
         style="display: none; position: absolute; top: 50px; left:50px; width: 400px; height: 400px; border: 2px solid red;">
        <button id="tempassBtn"
           onclick="selectTempPass();"
             style="float:left">Don't know your credentials? Click here to get a Temp Pass.
        </button>
        <button onclick="window.location.reload()" style="float:right">X</button>
        <br />
        <hr />
        <iframe src="about:blank" id="mvpdframe" name="mvpdframe" width="90%" height="90%" frameborder="0"></iframe>
    </div>
    <br/>
    <div id="ae" style="display: none">
        <p>Loading Access Enabler...</p>
    </div>
</body>
</html>
```

#### Casi di utilizzo dell’accesso iFrame {#iframe-login-use-cases}

**Per richiedere un passaggio temporaneo per la prima volta:**

1. Un utente accede alla pagina del programmatore e fa clic sul collegamento di accesso.
1. Si apre il selettore MVPD e l&#39;utente sceglie un MVPD dall&#39;elenco.
1. Viene visualizzato l’iFrame di autenticazione. Questo iFrame contiene un collegamento &quot;Temp Pass&quot;.
1. L&#39;utente fa clic su &quot;Passaggio temporaneo&quot;, quindi il programmatore aggiunge un flag a un cookie per impedire all&#39;utente di visualizzare il collegamento &quot;Passaggio temporaneo&quot; nelle visite successive alla pagina.
1. La richiesta di autenticazione Temp Pass raggiunge i server di autenticazione Primetime e genera un token di autenticazione. Il TTL è uguale al periodo di tempo impostato dal programmatore per il passaggio Temp.
1. La richiesta di autorizzazione Temp Pass raggiunge i server di autenticazione Primetime.
1. I server di autenticazione Primetime estraggono gli ID dispositivo e richiedente dalla richiesta e li memorizzano nel database insieme alla data di scadenza. Il tempo di scadenza è calcolato come segue: tempo di richiesta iniziale di Temp Pass più il TTL (specificato dal programmatore).
1. I server di autenticazione Primetime generano un token di autorizzazione.
1. L’utente accede al contenuto protetto.

**Per richiedere di nuovo un Passaggio Temp dopo che un utente che restituisce Passo Temp ha eliminato i cookie del browser:**

1. L&#39;utente accede alla pagina del programmatore e fa clic sul collegamento di accesso.
1. Si apre il selettore MVPD e l&#39;utente sceglie un MVPD dall&#39;elenco.
1. Viene visualizzato l’iFrame di autenticazione. Questo iFrame contiene un collegamento &quot;Temp Pass&quot; (l&#39;utente ha eliminato il cookie originale, in modo che il programmatore non sappia se l&#39;utente ha già fatto clic sul collegamento &quot;Temp Pass&quot; prima).
1. L&#39;utente fa nuovamente clic su &quot;Temp Pass&quot;, in modo che il programmatore aggiunga nuovamente un flag a un cookie, per impedire all&#39;utente di vedere il link &quot;Temp Pass&quot; nelle visite successive alla pagina.
1. La richiesta di autenticazione Temp Pass raggiunge i server di autenticazione Primetime, che generano un token di autenticazione. Il TTL rappresenta ora il tempo rimanente per il passaggio temporaneo (la differenza tra l’ora corrente e la data di scadenza associata all’ID dispositivo).
1. La richiesta di autorizzazione Temp Pass raggiunge i server di autenticazione Primetime.
1. I server di autenticazione di Primetime estraggono gli ID dispositivo e richiedente dalla richiesta e li utilizzano per recuperare il tempo di scadenza dal database di autenticazione di Primetime. L’ora corrente viene confrontata con la data di scadenza.
1. Se il passaggio temporaneo dell&#39;utente non è scaduto, i server di autenticazione Primetime generano un token di autorizzazione.
1. Se il passaggio temporaneo dell&#39;utente non è scaduto, l&#39;utente sarà in grado di accedere al contenuto protetto.

### Esempio di accesso automatico {#auto-login-sample}

Nell&#39;esempio seguente viene illustrato un caso in cui un utente accede automaticamente a TempPass quando visita un sito. L&#39;utente può scegliere di effettuare l&#39;accesso con un MVPD normale in qualsiasi momento e viene avvisato se TempPass è scaduto:

```HTML
<html>
<head>
    <title>Temp Pass Sample</title>
    <script type="text/javascript"
             src="https://ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.min.js"></script>
    <script type="text/javascript"
             src="https://raw.github.com/carhartl/jquery-cookie/master/jquery.cookie.js"></script>
    <script type="text/javascript"
             src="http://ajax.googleapis.com/ajax/libs/swfobject/2.2/swfobject.js"></script>
 
    <script type="text/javascript">
        var REQUESTOR = "REF";
        var RESOURCE = "sample_requestor_Id";
        var selectedProvider = null;
        var mvpds;
        var hasTempPassMVPD = false;
 
        // Used to cache the mvpd picker
        var picker;
 
        $(document).ready(function() {
            swfobject.embedSWF("http://entitlement.auth.adobe.com/entitlement/AccessEnablerDebug.swf"
                    , "ae", "1", "1", "11.0.0", "expressinstall.swf", {}
                    , {allowScriptAccess: "always"}
                    , {id: "accessEnabler", name: "accessEnabler"});
        });
 
        function swfLoaded(){
            console.log("AccessEnabler loaded");
            ae = $('#accessEnabler')[0];
 
            // Make sure the default picker is disabled
            ae.setProviderDialogURL("none");
 
            ae.setRequestor(REQUESTOR);
            ae.checkAuthentication();
        }
 
        /**
         * Callback received as a result of setRequestor()
         *
         * @param xml object holding the configuration for the current REQUESTOR
         * including the MVPD list
         */
        function setConfig(config) {
            // Save the mvpd list
            var mvpdList = $.parseXML(config);
            mvpds = $(mvpdList).find('mvpd');
 
            // Create the picker only once and cache it
            if(!picker) {
                picker = $('<div id="mvpdPicker"/>');
 
                var providersMenu = $('<select id="mvpdList" multiple></select>');
 
                $.each(mvpds, function(k, v) {
                    var mvpdID = $(v).find("id").text();
                    var mvpdName = $(v).find("displayName").text();
 
                    // Add the mvpd's to the menu while making
                    //   sure that the Temp Pass entry is skipped
                    if (mvpdID != "TempPass") {
                        providersMenu.append($('<option></option>', {value:mvpdID}).text(mvpdName));
                    } else {
                        hasTempPassMVPD = true;
                    }
                });
                picker.append(providersMenu);
                picker.append($('<br/>'));
                picker.append($('<input type="button" onclick="login()" value="login" />'));
                picker.append($('<input type="button" onclick="cancelPicker()" value="cancel" />'));                  
            }
 
            if (!hasTempPassMVPD) {
                $('#selectedProvider').html("FATAL ERROR: TempPass is not integrated with '" +
                  REQUESTOR + "'<br />This sample is valid only for sites integrated with TempPass !!!");             
            }
        }
 
        /**
         * Callback triggered for iFramed MVPD's
         */
        function createIFrame() {
            $('#mvpdPicker').remove();
            $('#ifrm').show();
        }
 
        /**
         * Hides the MVPD picker
         * when the user clicks "Cancel"
         */
        function cancelPicker() {
            $('#video').show();
            $('#mvpdPicker').remove();
            $('#loginBtn').show();
        }
 
        /**
         * Pops up the MVPD picker
         */
        function showPicker() {
            $('#video').hide();
            $('#loginBtn').hide();
            $('body').append(picker);
        }
 
        function logout() {
            $.removeCookie('tempPassUsed');
            ae.logout();
        }
 
        /**
         * Performs login with the selected MVPD
         */
        function login() {
            selectedProvider = $('#mvpdList').val()[0];
 
            // Make sure we clear out previously
            // selected. This is a must if we want to force
            // login with a real MVPD while still logged in with
            // TempPass, without doing an ae.logout()
            ae.setSelectedProvider(null);
            ae.getAuthentication();
        }

        /**
         * Callback triggered by AccessEnabler. This is usually
         * triggered in order to display the MVPD picker, but
         * since we already constructed, cached, and displayed the
         * picker, and the user already picked the MVPD, we don't need
         * to do anything here but state management
         */
        function displayProviderDialog() {
            // If the selected MVPD is TempPass
            // store this fact in a cookie,
            // otherwise clear it
            if (selectedProvider != 'TempPass') {
                $.removeCookie('tempPassUsed');
            } else {
                $.cookie("tempPassUsed", 1);
            }
 
            // Since the picker was already shown
            // and the user picked an MVPD,
            // just proceed to login
            ae.setSelectedProvider(selectedProvider);
        }
 
        function setAuthenticationStatus(status, code) {
            if (!hasTempPassMVPD) {
                $('#selectedProvider').html("FATAL ERROR: TempPass is not integrated with '" +
                  REQUESTOR + "'<br />This sample is valid only for sites integrated with TempPass !!!");
            } else if(status == 1) {
                selectedProvider = ae.getSelectedProvider().MVPD;
                $('#selectedProvider').text("Authenticated with " + selectedProvider + "   ");
 
                // If authenticated with TempPass
                // allow the user to login with
                // a real MVPD
                if (selectedProvider == "TempPass") {
                    $('#loginBtn').show();
                    $('#logoutBtn').hide();
                } else {
                    $('#loginBtn').hide();
                    $('#logoutBtn').show();
                }
 
                // Get authorization
                // Note: This is mandatory in order to "start" the temp pass countdown
                ae.checkAuthorization(RESOURCE);
            } else if(code != "Provider not Selected Error") {
                // Auto-authenticate with TempPass only if we infer
                // that TempPass has not expired, otherwise we
                // inform the user that TempPass has expired
                if ($.cookie('tempPassUsed') == 1) {
                   $('#selectedProvider').text("Your Temp Pass has expired, please log in with your cable provider!");
                   $('#logoutBtn').show();
                   showPicker();
                } else {
                    selectedProvider = 'TempPass';
                    ae.getAuthentication();
                }
            }
        }
 
        /**
         * Displays the picker as a result
         * of user action
         */
        function loginClicked() {
            $('#loginBtn').hide();
            showPicker();
        }
 
        /**
         * Callback triggered in case of authorization success
         */
        function setToken(token) {
            console.log(token);
            $('#video').html('<img src=">');
        }
 
        /**
         * Callback triggered in case of authz failure
         */
        function tokenRequestFailed(resource, status, message) {
            console.log(resource);
            $('#video').html('<p style="color: red">' + status + ': ' + message + '</p>');
        }
 
    </script>
</head>
<body>
    <button id="loginBtn" style="display: none" onclick="loginClicked()">Login</button>
    <label id="selectedProvider" for="logoutBtn"></label><button id="logoutBtn"
        style="display: none" onclick="logout()">Logout</button>
    <div id="ifrm"
         style="display: none; position: absolute; top: 50px; left:50px;
         width: 400px; height: 400px; border: 2px solid red;">
        <button onclick="window.location.reload()" style="float:right">Close this window</button>
        <br /><hr />
        <iframe src="about:blank" id="mvpdframe" name="mvpdframe" width="80%" height="80%" frameborder="0"></iframe>  
    </div>
    <br/>
 
    <div id="video"></div>
    <div id="ae" style="display: none"><p>Loading Access Enabler...</p></div>
</body>
</html>
```

## Utilizzare più passaggi temp {#use-mult-tempass}

Alcuni eventi richiedono un accesso graduale e gratuito ai contenuti, ad esempio un intervallo iniziale di accesso libero (ad esempio, 4 ore), seguito da accessi gratuiti giornalieri (ad esempio, 10 minuti ogni giorno successivo).  Affinché un programmatore possa implementare questo scenario, deve organizzarlo con il contatto Adobe per configurare due MVPD temporanei per il programmatore.

Per questo scenario di esempio (una sessione gratuita iniziale di 4 ore, seguita da sessioni gratuite giornaliere di 10 minuti) l&#39;Adobe configura un MVPD chiamato TempPass1 con un Time-To-Live (TTL) di 4 ore e un TempPass2 con un TTL di 10 minuti per il periodo successivo.  Entrambi sono associati all&#39;ID del richiedente del programmatore.

### Implementazione del programmatore {#mult-tempass-prog-impl}

Dopo che Adobe configura le due istanze TempPass, i due MVPD aggiuntivi (TempPass1 e TempPass2) verranno visualizzati nell&#39;elenco MVPD del programmatore.  Per implementare più passaggi temp, il programmatore deve adottare le seguenti misure:

1. Nella visita iniziale dell&#39;utente al sito, effettua automaticamente l&#39;accesso con TempPass1. È possibile utilizzare l&#39;esempio di Autologin di cui sopra come punto di partenza per questa attività.
1. Quando rilevi che TempPass1 è scaduto, archivia il fatto (in un cookie/archiviazione locale) e presenta l&#39;utente con il tuo selettore MVPD standard. **Assicurati di filtrare TempPass1 e TempPass2 da tale elenco**.
1. In ogni giorno successivo, se TempPass1 è scaduto, inserisci automaticamente l&#39;utente con TempPass2.
1. Quando TempPass2 è scaduto, memorizzare il fatto (in un cookie/archiviazione locale) per il giorno, e presentare l&#39;utente con il tuo selettore MVPD standard. Di nuovo, assicurati di filtrare TempPass1 e TempPass2 da tale elenco.
1. Ad ogni nuovo giorno, alle 00:00, reimposta tutti i passaggi temporanei per TempPass2, utilizzando [Ripristina API web TempPass](/help/authentication/temp-pass.md#reset-all-tempass).

>[!NOTE]
>**Nota di programmazione:** Primetime Authentication non dispone di un meccanismo integrato per arrestare lo streaming gratuito dopo che i 10 minuti sono passati.  Spetta ai programmatori limitare l&#39;accesso una volta che TempPass2 scade. A tal fine, i programmatori possono implementare nei propri siti/app una chiamata &quot;checkAuthorization&quot; ogni X minuti, dove X è il periodo di tempo che il programmatore determina per le proprie app.

## Reimposta tutte le passate temporanee {#reset-all-tempass}

Alcune regole aziendali richiedono l’eliminazione regolare di Temp Pass o una reimpostazione ad hoc di tutte le Passate Temp rilasciate per un particolare ID Richiedente e un ID MVPD. Questa funzione supporta casi d’uso come i seguenti:

* Passo Temp giornaliero di 10 minuti (il Passo Temp deve essere ripristinato all&#39;inizio della giornata)
* Un Temp Pass disponibile per tutti gli utenti durante le ultime notizie. (È necessario reimpostare il Passo Temp per tutti i dispositivi non appena iniziano le notizie di interruzione.)
* Lo scenario con più passaggi temporanei che fornisce una combinazione di un periodo di visualizzazione iniziale di una certa lunghezza, seguito da periodi giornalieri successivi di un&#39;altra lunghezza.

Per ripristinare tutte le passate Temp, l&#39;autenticazione Primetime fornisce ai programmatori un *pubblico* API web:

```url
DELETE https://mgmt.auth.adobe.com/reset-tempass/v2/reset
```

>[!NOTE]
>L&#39;URL precedente sostituisce l&#39;API di reimpostazione precedente. La precedente API di ripristino (v1) non è più supportata.

* **Protocollo:** HTTPS
* **Host:**
   * Versione - mgmt.auth.adobe.com
   * Prequal - mgmt-prequal.auth.adobe.com
* **Percorso:** /reset-tempass/v2/reset
* **Parametri query:** `device_id=all&requestor_id=REQUESTOR_ID&mvpd_id=TEMPPASS_MVPD_ID`
* **Intestazioni:** ApiKey - 1232293681726481
* **Risposta:**
   * Completato - HTTP 204
   * Errore:
      * HTTP 400 per una richiesta errata
      * HTTP 401 se ApiKey non è stato specificato
      * HTTP 403 se ApiKey non è valido

Ad esempio:

```curl
$ curl -H "Authorization: Bearer <access_token_here>" -X DELETE -v "https://mgmt.auth.adobe.com/reset-tempass/v2.1/reset?device_id=all&requestor_id=AdobeBEAST&mvpd_id=TempPass"
```

## Client supportati {#supp-clients}

Supporto per lo strumento Passo Temp e Reimposta per piattaforma:

| Client di autenticazione Adobe Primetime | Passaggio Temp | Ripristina strumento |
|:--------------------------------------:|:---------:|:----------:|
| JS AccessEnabler | SÌ | SÌ |
| iOS client nativo | SÌ | SÌ |
| tvOS client nativo | SÌ | SÌ |
| Android client nativo | SÌ | SÌ |
| FireTV client nativo | SÌ | SÌ |
| API senza client | SÌ | SÌ |

## Limitazioni e problemi noti {#limitations}

Questa sezione descrive le limitazioni applicabili all&#39;implementazione corrente di Temp Pass.

**SDK JavaScript**: supporta la funzionalità reset temp pass dalla versione **3.X e versioni successive**.

<!--For Customers migrating from the 2.X JavaScript AccessEnabler to the 3.X JavaScript AccessEnabler, see [AccessEnabler JS 2.x to JS 3.x migration guide](https://tve.helpdocsonline.com/accessenabler-js-to-js-migration-guide).-->