---
description: È possibile trasmettere qualsiasi flusso da un'app mittente basata su TVSDK e riprodurre il flusso su Chromecast con Browser TVSDK.
seo-description: È possibile trasmettere qualsiasi flusso da un'app mittente basata su TVSDK e riprodurre il flusso su Chromecast con Browser TVSDK.
seo-title: App Google Cast per browser TVSDK
title: App Google Cast per browser TVSDK
uuid: 018143e2-143a-4f88-97c6-4b10a2083f9e
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---


# App Google Cast per browser TVSDK{#google-cast-app-for-browser-tvsdk}

È possibile trasmettere qualsiasi flusso da un&#39;app mittente basata su TVSDK e riprodurre il flusso su Chromecast con Browser TVSDK.

<!--<a id="section_87CE5D6D46F0439EB6E63A742D6DD9C8"></a>-->

Esistono due componenti di un&#39;app abilitata per Cast:

* L&#39;app mittente, che funge da telecomando.

   Le app di invio includono smartphone, personal computer e così via. L&#39;app può essere sviluppata utilizzando SDK nativi per iOS, Android e Chrome.
* L&#39;app di ricezione, che viene eseguita su Chromecast e riproduce il contenuto.

   >[!IMPORTANT]
   >
   >Questa app può essere solo un&#39;app HTML5.

Il mittente e il destinatario comunicano utilizzando gli SDK Cast per trasmettere i messaggi.

## Flusso di lavoro di base {#section_FAF680FF29DA4D24A50AC0A2B6402B58}

Di seguito viene fornita una panoramica del processo:

1. L&#39;app mittente stabilisce una connessione con l&#39;app ricevente.
1. L&#39;app mittente invia un messaggio per caricare il supporto nell&#39;app ricevente.
1. L&#39;app ricevente inizia la riproduzione.
1. L&#39;app mittente invia all&#39;app ricevente messaggi per il controllo della riproduzione quali riproduzione, pausa, ricerca, avanzamento rapido, riavvolgimento rapido, riavvolgimento, modifica del volume e così via.
1. L&#39;app ricevente reagisce a questi messaggi.

## Formato del messaggio {#section_1624159DD51D4C87B3E5803DEEBCB6B7}

È necessario definire i messaggi in modo che il mittente e il destinatario possano capire. Esempio di messaggio di ricerca:

```js
{ 
"type": "seek", 
"seekTo": 10000 
} 
```

Quando si inviano messaggi personalizzati, come il messaggio di ricerca tramite gli SDK Cast, è necessario uno spazio dei nomi di messaggio personalizzato. Di seguito è riportato un esempio in JavaScript:

```js
Custom Message Namespace 
var MSG_NAMESPACE = "urn:x-cast:com.adobe.primetime"; 
```

## Definizione di una connessione {#section_B4D40CABDD3E46FDBE7B5651DFF91653}

>[!IMPORTANT]
>
>Le API TVSDK del browser non sono coinvolte quando si stabilisce la connessione.

Per stabilire una connessione, il mittente e il destinatario devono completare le seguenti attività:

* Il mittente deve consultare la documentazione relativa alla piattaforma in [Sender App Development](https://developers.google.com/cast/docs/sender_apps).
* Il ricevitore utilizza le API del ricevitore Cast per stabilire una connessione con l&#39;app mittente. Ad esempio:

   ```js
   window.castReceiverManager = cast.receiver.CastReceiverManager.getInstance(); 
   
   window.castReceiverManager.onReady = function (event) { /*handle event*/ }; 
   window.castReceiverManager.onSenderConnected = function (event) { /*handle event*/ }; 
   window.castReceiverManager.onSenderDisconnected = function (event) { /*handle event*/ }; 
   
   var customMessageBus = window.castReceiverManager.getCastMessageBus(MSG_NAMESPACE); 
   customMessageBus.onMessage = function (event) { /*handle messages*/ }; 
   
   window.castReceiverManager.start(); 
   ```

## Gestione messaggi {#section_3E4814546F5946C9B3E7A1AE384B4FF8}

Per inviare messaggi al destinatario, consulta la documentazione relativa alla piattaforma del mittente.

>[!IMPORTANT]
>
>È necessario includere lo spazio dei nomi personalizzato `MSG_NAMESPACE` in tutti i messaggi.

Per l&#39;app ricevente, segui la documentazione relativa alle API del ricevitore cast.

**Esempio di messaggio mittente basato su Chrome**

```js
window.session.sendMessage(MSG_NAMESPACE, message, successCallback, errorCallback); //https://developers.google.com/cast/docs/reference/chrome/chrome.cast.Session#sendMessage
```

**Gestione degli eventi del mittente in base a Chrome**

Eseguire un binding dei gestori eventi con gli elementi dell&#39;interfaccia utente che invieranno messaggi quando vengono attivati gli eventi corrispondenti. Ad esempio, per un&#39;app mittente basata su Chrome, l&#39;evento di ricerca potrebbe essere inviato come segue:

```js
document.getElementById("#seekBar").addEventListener("click", seekEventHandler); 
   
function seekEventHandler(event) { 
    seekMessage = { type: "seek", seekTo: player.currentTime }; //player is an instance of AdobePSDK.MediaPlayer 
    window.session.sendMessage(MSG_NAMESPACE, seekMessage, successCallback, errorCallback); 
} 
```

**Gestione dei messaggi del ricevitore**

Dall&#39;app ricevente, ecco un esempio di come gestire il messaggio di ricerca:

```js
customMessageBus.onMessage = function (event) { 
    var message = JSON.parse(event.data); 
    switch (message.type) { 
        case "seek":  
            player.seek(parseInt(message.seekTo)); 
            break; 
        //code for handling other events 
        default:  
            break; 
    } 
}; 
```

