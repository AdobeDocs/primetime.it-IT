---
title: Panoramica dell'SDK JavaScript
description: Panoramica dell'SDK JavaScript
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 0%

---


# Panoramica dell&#39;SDK JavaScript {#javascript-sdk-overview}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Introduzione

L&#39;Adobe consiglia vivamente di eseguire la migrazione all&#39;ultima versione di JS v4.x della libreria AccessEnabler.

L&#39;integrazione JavaScript di autenticazione Adobe Primetime offre ai programmatori una soluzione TV-Everywhere nel familiare ambiente di sviluppo delle applicazioni web JS. I componenti principali dell&#39;integrazione sono l&#39;applicazione di &quot;alto livello&quot; (interazione utente, presentazione video) e la libreria AccessEnabler di &quot;basso livello&quot; fornita dall&#39;Adobe che fornisce la voce ai flussi di adesione e gestisce la comunicazione con i server di autenticazione Adobe Primetime.

Il flusso generale di adesione all’autenticazione di Adobe Primetime è incluso in [Flusso di adesione del programmatore](/help/authentication/entitlement-flow.md), e la guida all&#39;integrazione JavaScript descrive l&#39;implementazione di . Le sezioni seguenti forniscono descrizioni ed esempi specifici dell&#39;integrazione di AccessEnabler JavaScript.

>[!IMPORTANT]
>
>Questo documento descrive l’implementazione per una soluzione web desktop. La libreria JavaScript non è supportata sulle piattaforme mobili (ad esempio, Safari su iOS, Chrome su Android). Utilizza i nostri SDK nativi se desideri eseguire il targeting di una piattaforma mobile (iOS, Android, Windows).

## Creazione della finestra di dialogo di selezione MVPD {#creating-the-mvpd-selection-dialog}

Affinché un utente possa accedere al proprio MVPD e diventare autenticato, la pagina o il lettore deve fornire all&#39;utente un modo per identificare il proprio MVPD. Per lo sviluppo viene fornita una versione predefinita di una finestra di dialogo di selezione MVPD. Per l&#39;utilizzo in produzione, è necessario implementare il proprio selettore MVPD. 

Se sai già chi è il fornitore del cliente, puoi [impostare l&#39;MVPD a livello di programmazione](/help/authentication/home.md), senza l’interazione dell’utente. La tecnica è la stessa, ma bypassa il passaggio di richiamare la finestra di dialogo Selettore provider e chiedere al cliente di selezionare il proprio MVPD.

## Visualizzazione del provider di servizi {#displaying-the-service-provider}

L&#39;esempio di codice seguente illustra come individuare e visualizzare il provider di servizi per il cliente corrente:

 **HTML** - Questa pagina aggiunge una sezione alla pagina che visualizza il provider scelto dal cliente, se ha già effettuato l&#39;accesso:

```HTML
    <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" 
            "http://www.w3.org/TR/html4/loose.dtd"> 
    <html>
    <head>
        <title>Get the distributor that is used for the authentication</title>
        <script type="text/javascript" src="libs/jquery-1.4.4.min.js"></script>
        <script type="text/javascript" src="libs/swfobject.js"></script>
        <script type="text/javascript" src="scripts/sample6.js"></script>
    </head>
    <body>
        <div id="alternative">
        <a href="http://www.adobe.com/go/getflashplayer"> 
            <img src="http://www.adobe.com/images/shared/download_buttons/get_flash_player.gif" 
                 alt="Get Adobe Flash player"/> </a>
        </div> 
        <div id="user_authenticated">Please wait while we verify your authentication status</div> 
        <div id="control">
        <button id="sign_in" style="display:none;">Sign in</button>
        <button id="sign_out" style="display:none;">Sign out</button>
        </div> 
        <div id="distributor"></div> 
        <div id="provider_selector" style="display:none;">
        <select id="provider_list"></select>
        <button id="login">Login</button>
        <button id="cancel">Cancel</button>
        </div> 
        <div id="video_player">This is a video player showing an image as a preview.  You are not yet authorized to see this content.  Make sure that you first sign in.
        </div> 
        <div id="get_authorization">
        <button id="request_access" style="display:none;">Request access</button>
        </div> 
    </body>
    </html>
```
 

**JavaScript** Questo file JavaScript esegue una query su Access Enabler per il provider corrente se l&#39;utente ha già effettuato l&#39;accesso e visualizza il risultato nella sezione della pagina riservata. Inoltre, implementa una finestra di dialogo del selettore MVPD:

```JS
    $(function() {
        embedAE();
    }); 
    function embedAE() {
        var flashvars = {};
        var params = {
            bgcolor: "#869ca7",
            quality: "high",
            allowscriptaccess: "always"
        };
        var attributes = {
            id: "ae_swf",
            align: "middle",
            name: "ae_swf"
        };
        swfobject.embedSWF(
                "https://entitlement.auth-staging.adobe.com/entitlement/AccessEnabler.swf",      
                "alternative", "1", "1", "10.1.53", "", flashvars, params, attributes);
    } 
    function getAE() {
        return document.getElementById("ae_swf");
    } 
    function swfLoaded() {
        var swf = getAE();
        initBindings();
        // don't load the default provider-selection dialog 
        swf.setProviderDialogURL("none");
        // identify yourself 
        swf.setRequestor("sample_requestor_Id");
        swf.checkAuthentication();
    } 
    // Define the button actions for the provider dialog
    function initBindings() {
        var provider_selector = $('#provider_selector');
        var sign_in = $('#sign_in');
        var sign_out = $('#sign_out');
        var login = $('#login');
        var cancel = $('#cancel');
        var request_access = $('#request_access'); 
        sign_out.click(function() {
            getAE().logout();
        });
        sign_in.click(function() {
            getAE().getAuthentication();
        }); 
        login.click(function() {
            var selected_mvpd_id = $("#provider_list option:selected").val();
            getAE().setSelectedProvider(selected_mvpd_id);
        }); 
        cancel.click(function() {
            getAE().setSelectedProvider(null);
            provider_selector.hide();
        }); 
        request_access.click(function(){
            getAE().getAuthorization("sample_requestor_Id");
        });
    }
    // Called if user is already authenticated; queries AE to find the current user's MVPD, 
    // Adds the result to the UI 
    function setDistributor() {
        var distributor = $("#distributor");
        var selectedProvider = getAE().getSelectedProvider();
        distributor.replaceWith('<div id="distributor">' +
                                'Courtesy of ' +
                                selectedProvider.MVPD +
                                '</div>');
    } 
    // Adjust the contents of the provider dialog, based on authentication status 
    // Adds the call to check and display the current distributor, if the user is already
    // logged in. 
    function setAuthenticationStatus(isAuthenticated, errorCode) {
        var user_authenticated = $("#user_authenticated");
        var video_player = $("#video_player");
        var sign_in = $('#sign_in');
        var sign_out = $('#sign_out');
        var request_access = $('#request_access'); 
        if (isAuthenticated == 1) {
            setDistributor();
            user_authenticated.replaceWith('<div id="user_authenticated">
                                           You are authenticated - if you wish you can sign out
                                           </div>');
            sign_out.show();
            sign_in.hide();
            video_player.replaceWith('<div id="video_player">Now you can ask for access.</div>');
            request_access.show();
        } else {
            user_authenticated.replaceWith('<div id="user_authenticated">
                                           You are not authenticated please sign in
                                           </div>');
            sign_in.show();
            sign_out.hide();
        }
    } 
    // Allow user to choose a provider 
    function displayProviderDialog(providers) {
        var provider_list = $("#provider_list");
        var options = provider_list.attr('options');
        for (var index in providers) {
            options[index] = new Option(providers[index].displayName,
                                        providers[index].ID);
        }
        //select the first one by default 
        if (!$("#provider_list option:selected").length)
            $("#provider_list option[0]").attr('selected', 'selected'); 
        $('#provider_selector').show();
    } 
    // Handle the authorization response by sending token to video player 
    function setToken(requested_resource_id, token) {
        var video_player = $("#video_player");
        var request_access = $("#request_access");
        video_player.replaceWith('<div id="video_player">Now you are authorized to ' +
                                 requested_resource_id +
                                 ' content with ' + token + ' . </div>');
    }
```

## Disconnessione {#logout}

Chiamata `logout()` per avviare il processo di logout. Questo metodo non accetta argomenti. Disconnette l&#39;utente corrente, cancella tutte le informazioni di autenticazione e autorizzazione per quell&#39;utente ed elimina tutti i token AuthN e AuthZ dal sistema locale.

Ci sono alcuni casi in cui il lettore non è responsabile della gestione degli accessi utente:

 

- **Quando l&#39;accesso viene avviato da un sito non integrato con l&#39;autenticazione Adobe Primetime.** In questo caso, l’MVPD può richiamare il servizio Single Logout di autenticazione Adobe Primetime tramite un reindirizzamento del browser. (La chiamata di SLO tramite una chiamata backchannel non è attualmente supportata.)

>[!NOTE]
>
>Se l’utente lascia il computer inattivo abbastanza a lungo da far scadere i token, può comunque tornare alla sessione e avviare correttamente l’logout. L’autenticazione Adobe Primetime assicura che tutti i token vengano eliminati e notifica all’MVPD di eliminare anche la loro sessione.

Il seguente codice JavaScript illustra la disconnessione (deautenticazione) di un utente attualmente autenticato:

```JS
    [...]
    /*
     * @param isAuthenticated authentication status: 1 - Authenticated, 0 - not authenticated 
     * @param errorCode Any error that occurred when determining the authentication status.
     * An empty string if no error occurred.
     */
    function setAuthenticationStatus(isAuthenticated, errorCode) {
        if (isAuthenticated == 1 ) {
            /* User is authenticated – we can logout / deauthenticate */
            accessEnablerObject.logout();
            /* Logs out the current user, clearing all authentication
             * and authorization information for that user. Deletes
             * all authN and authZ tokens from the user's system.
             */
        } else {
            /*
             * User is NOT authenticated – we do not need to logout;
             * Show the log-in image/button/message
             */
        }
    }
```

<!--
**Related Information**

- [JavaScript SDK Cookbook](/help/authentication/javascript-sdk-cookbook.md)
- [JavaScript SDK API Reference](/help/authentication/javascript-sdk-api-reference.md)
- [JavaScript Code Samples](#javascript-code-samples)
- [Understanding Tokens](#understanding_tokens)
-->