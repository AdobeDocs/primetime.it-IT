---
title: Come migrare la pagina di accesso MVPD da iFrame a Popup
description: Come migrare la pagina di accesso MVPD da iFrame a Popup
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 0%

---


# Come migrare la pagina di accesso MVPD da iFrame a Popup {#migr-mvpd-login-iframe-popup}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Popup e iFrame {#popup-vs-iframe}

Alcuni utenti hanno riscontrato problemi relativi ai cookie di terze parti con l&#39;implementazione iFrame di una pagina di accesso MVPD.
<!--These issues are described in the tech notes linked below:

* [Adobe Primetime authentication and Safari login issues](https://tve.helpdocsonline.com/adobe-pass)
* [MVPD iFrame login and 3rd party cookies](https://tve.helpdocsonline.com/mvpd)-->

Il team di autenticazione di Adobe Primetime **consiglia di implementare la finestra popup / nuova pagina di accesso alla finestra** invece della versione iFrame su Firefox e Safari.  Tuttavia, se si sta implementando una pagina di accesso per Internet Explorer, è possibile che si verifichino problemi con l&#39;implementazione popup. I problemi di IE sono causati dal fatto che, dopo che l&#39;utente si autentica con il proprio MVPD nella finestra a comparsa, l&#39;autenticazione di Adobe Primetime forza un reindirizzamento della pagina padre, che è visto come un popup blocker da Internet Explorer. Il team di autenticazione di Adobe Primetime **consiglia di implementare l&#39;accesso iFrame per Internet Explorer**.

Il codice di esempio presentato in questa nota tecnica utilizza un&#39;implementazione ibrida sia di iFrame che di popup - apertura di un iFrame su Internet Explorer e una finestra a comparsa sugli altri browser.

Poiché esiste già un’implementazione iFrame, la prima parte della nota tecnica presenta il codice per l’implementazione iFrame e la seconda presenta le modifiche per adattarsi all’implementazione popup come impostazione predefinita.


## Selettore MVPD con pagina di accesso in un iFrame {#mvpd-pickr-iframe}

Gli esempi di codice precedenti mostravano una pagina HTML contenente &lt;div> tag in cui deve essere creato l’iFrame insieme al pulsante Chiudi iFrame:

```HTML
<body> 
    <div id="mvpddiv">
        <div style="background: red">
            <input type="button" id="btnCloseIframe" value="X" onclick="closeIframeAction();">
        </div>
        <br/>
        <!-- We use the "about:blank" value so that when the iFrame loads
             we do not see the the parent page. -->
        <iframe id="mvpdframe" name="mvpdframe" src="about:blank"></iframe>
    </div> 
</body>
```

Associato **JavaScript** codice:

```JavaScript
/*
 * Callback indicating that the AccessEnabler swf has initialized
 */
function swfLoaded() {
    // AccessEnabler is loaded so we can use the API function it provides
    accessEnablerObject.setRequestor(requestorID); 
    accessEnablerObject.checkAuthentication();
} 
/*
* The code the correctly closes the opened IFrame and does not leave the
* AccessEnabler in an undefined state.
*/
function closeIframeAction () {
    accessEnablerObject.setSelectedProvider(null);
    /* We use the "about:blank" value so that when the iFrame loads
     * we do not see the the previous MVPD.
     */
    document.getElementById('mvpdframe').src="about:blank";
    document.getElementById('mvpddiv').style.visibility="hidden";
    document.getElementById('mvpddiv').style.display="none";
}
/*
* Some of the supported MVPDs require their login pages to be displayed within an iFrame.
* In your HTML page, you must include the following <div> tag: "<div id="mvpddiv"></div>".
* Called when the selected MVPD requires an iFrame in which to display its authentication UI.
*/
function createIFrame(inWidth, inHeight) {
     // Create the iFrame to the specified width and height for the auth page
    ifrm = document.createElement("IFRAME");
    ifrm.name = "mvpdframe";
    ...
    document.getElementById('mvpddiv').appendChild(ifrm);
    ...
    // Force the name into the DOM since it is still not refreshed, for IE
    window.frames["mvpdframe"].name = "mvpdframe";
}
/*
 * The custom non-Flash MVPD selector dialog will be implemented in this function.
 */
function displayProviderDialog(providers) {
    /* This is an example how previously the MVPD picker was build and will be replaced. */
}
/* 
* Sending the user selected MVPD of the custom dialog is achieved
* by calling the API function setSelectedProvider(providerID:String).
*/
function setSelectedProvider(providerID) {
    accessEnablerObject.setSelectedProvider(providerID);
}
```


## Selezione MVPD con pagina di login in una finestra popup {#mvpd-pickr-popup}

Poiché non utilizzeremo un **iFrame** inoltre, il codice HTML non conterrà l’iFrame o il pulsante per chiudere l’iFrame. Il div che in precedenza conteneva l’iFrame - **mvpddiv** - saranno conservati e utilizzati per i seguenti scopi:

* per notificare all&#39;utente che la pagina di accesso MVPD è già aperta se l&#39;elemento attivo popup è perso
* per fornire un collegamento per riattivare la finestra a comparsa

```HTML
<body onload="javascript:loadAccessEnabler();"> 
   <div id="aeHolder">
       <div name="contentAccessEnabler" id="contentAccessEnabler"></div>
   </div>
   <div id="mvpddiv">
      <p>
      <strong>No login window?</strong>
      <br/>
      <a href="javascript:mvpdWindow.focus();">Click here to open it.</a>
      <br/>
      Still not working? Check popup blockers!
      </p>
   </div> 
 
   <div id="picker" style="display:none">
      Choose MVPD: <br/>
      <select id="mvpdList" multiple></select>
      <br/>
         <a id="authenticateButton" onclick="javascript:authenticate();">Authenticate</a>
   </div>
</body>
```

L’elenco degli MVPD verrà visualizzato nel div denominato **picker** come selezione **-mvpdList**.

Verrà utilizzato un nuovo callback API - **setConfig(configXML)**. Il callback viene attivato dopo aver chiamato la funzione setRequestor(requestorID) . Questo callback restituisce l’elenco degli MVPD integrati con il requestorID precedentemente impostato. Nel metodo di callback, il codice XML in entrata verrà analizzato e l&#39;elenco degli MVPD nella cache. Viene anche creato il selettore MVPD ma non viene visualizzato.

```JavaScript
var mvpdList;  // The list of cached MVPDs
var mvpdWindow;  // The reference to the popup with the MVPD login page
var cancelTimer = 0;
/* Callback indicating that the AccessEnabler swf has initialized */
function swfLoaded() {
   accessEnablerObject = $('#AccessEnabler').get(0);
   // Using a custom implementation of the MVPD picker
   accessEnablerObject.setProviderDialogURL('none');
   accessEnablerObject.setRequestor(requestorID); 
}

function setConfig(configXML) {
   mvpdList = [];
   $.each($($.parseXML(configXML)).find('mvpd'), function (idx, item) {
      var mvpdId = $(item).find('id').text();
      mvpdList[mvpdId] = {
         displayName: $(item).find('displayName').text(),
         logo: $(item).find('logoUrl').text(),
         popup: $(item).find('iFrameRequired').text() == "true",
         width: $(item).find('iFrameWidth').text(),
         height: $(item).find('iFrameHeight').text()
      };

      $('#mvpdList').append($('<option value="' + mvpdId + '" title="' + mvpdId + '">' + mvpdList[mvpdId].displayName + '</option>'));
   });
   accessEnablerObject.getAuthentication();
}
```

Dopo la chiamata della funzione getAuthentication() o getAuthorization() , viene attivato il callback displayProviderDialog() . Normalmente, all&#39;interno di questo callback, l&#39;elenco MVPD sarebbe stato costruito e visualizzato. Poiché il selettore MVPD è già stato costruito, l&#39;unica cosa da fare è visualizzarlo all&#39;utente.

```JavaScript
/*
 * The custom non-Flash MVPD selector dialog will be implemented in this function.
 */
function displayProviderDialog(providers) {
   $('#picker').show();
}
```

Dopo che l’utente ha selezionato un MVPD dal selettore, è necessario creare il popup. Alcuni browser possono bloccare il popup se viene creato con about:blank o con una pagina che si trova su un altro dominio - quindi si consiglia di aprirlo con il nome host da cui viene caricato AccessEnabler.

Nell’implementazione iFrame, il ripristino del flusso di autenticazione veniva eseguito dal pulsante btnCloseIframe e dalla funzione JavaScript closeIframeAction() , ma ora la decorazione dell’iFrame non è più possibile. Quindi, lo stesso comportamento si ottiene guardando per quando la finestra a comparsa è chiusa (dall&#39;utente o finendo il flusso di autenticazione). È stato aggiunto uno snippet di codice che aiuta anche nel caso in cui l&#39;utente perda lo stato attivo della finestra a comparsa:

```HTML
"<a href="javascript:mvpdWindow.focus();">Click here to open it.</a>".
```

Nel callback createIFrame() il **mvpddiv** verrà visualizzato div.

```JavaScript
function createIFrame(width, height) {
   $('#mvpddiv').show();
   if (useIframeLoginStyle) {
      ...
   }
}

/* Function called when user has selected the MVPD from the picker */
function authenticate() {
   var selectedMvpd = $('#mvpdList').val()[0];
   if (mvpdList[selectedMvpd].popup) {
      mvpdWindow = window.open("http://entitlement.auth-staging.adobe.com", "mvpdframe", "width=" + mvpdList[selectedMvpd].width + ",height=" + mvpdList[selectedMvpd].height, true);
      if (!mvpdWindow) {
         // Message to user that popup blocker is not allowing the authentication process to start
      }
      //watch the mvpd popup for close
      clearInterval(cancelTimer);
      cancelTimer = setInterval(checkClosed, 200);
   }
   accessEnablerObject.setSelectedProvider(selectedMvpd);
}

function checkClosed() {
   try {
      if (mvpdWindow && mvpdWindow["closed"]) {
         clearInterval(cancelTimer);
         accessEnablerObject.setSelectedProvider(null);
         accessEnablerObject.getAuthentication();
         $('#mvpddiv').hide();
      }
   } catch (error) {
      console.log(error);
   }
}
```

>[!IMPORTANT]
>
>* Il codice di esempio contiene una variabile hardcoded per il requestorID utilizzato - &#39;REF&#39; che deve essere sostituita da un vero e proprio requestor id programmatore.
>* Il codice di esempio viene eseguito correttamente solo da un dominio inserito nella whitelist associato all’id richiedente utilizzato.
>* Poiché l’intero codice è disponibile per il download, il codice presentato in questa nota tecnica è stato troncato. Per un campione completo, vedi **Esempio di iFrame JS vs Popup**.
>* Le librerie JavaScript esterne sono state collegate da [Servizi in hosting Google](https://developers.google.com/speed/libraries/).

