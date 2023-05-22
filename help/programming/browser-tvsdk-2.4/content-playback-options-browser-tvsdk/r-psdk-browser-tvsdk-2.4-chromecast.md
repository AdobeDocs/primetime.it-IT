---
description: Puoi eseguire il cast di qualsiasi flusso da un’app mittente basata su TVSDK e riprodurlo in Chromecast con il browser TVSDK.
title: App Google Cast per TVSDK browser
exl-id: 71077467-8040-4f04-a43b-cc963701c426
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# App Google Cast per TVSDK browser{#google-cast-app-for-browser-tvsdk}

Puoi eseguire il cast di qualsiasi flusso da un’app mittente basata su TVSDK e riprodurlo in Chromecast con il browser TVSDK.

<!--<a id="section_87CE5D6D46F0439EB6E63A742D6DD9C8"></a>-->

Esistono due componenti di un’app abilitata per Cast:

* L&#39;app mittente, che funge da telecomando.

   Le app del mittente includono smartphone, personal computer e così via. L’app può essere sviluppata utilizzando SDK nativi per iOS, Android e Chrome.
* L’app ricevente, che viene eseguita su Chromecast e riproduce il contenuto.

   >[!IMPORTANT]
   >
   >Questa app può essere solo un’app HTML5.

Il mittente e il destinatario comunicano utilizzando gli SDK Cast per trasmettere i messaggi.

## Flusso di lavoro di base {#section_FAF680FF29DA4D24A50AC0A2B6402B58}

Ecco una panoramica del processo:

1. L’app mittente stabilisce una connessione con l’app ricevente.
1. L’app mittente invia un messaggio per caricare il contenuto multimediale nell’app ricevente.
1. L&#39;app ricevitore inizia la riproduzione.
1. L’app del mittente invia all’app del ricevitore messaggi di controllo della riproduzione, come riproduzione, pausa, ricerca, avanzamento rapido, riavvolgimento rapido, riavvolgimento, modifica del volume e così via.
1. L’app ricevente reagisce a questi messaggi.

## Formato del messaggio {#section_1624159DD51D4C87B3E5803DEEBCB6B7}

È necessario definire i messaggi in modo che il mittente e il destinatario possano comprenderli. Di seguito è riportato un esempio di messaggio di ricerca:

```js
{ 
"type": "seek", 
"seekTo": 10000 
} 
```

Quando si inviano messaggi personalizzati, come il messaggio di ricerca tramite gli SDK Cast, è necessario uno spazio dei nomi del messaggio personalizzato. Ecco un esempio in JavaScript:

```js
Custom Message Namespace 
var MSG_NAMESPACE = "urn:x-cast:com.adobe.primetime"; 
```

## Stabilimento di una connessione {#section_B4D40CABDD3E46FDBE7B5651DFF91653}

>[!IMPORTANT]
>
>Le API TVSDK del browser non sono coinvolte quando si stabilisce la connessione.

Per stabilire una connessione, il mittente e il destinatario devono completare le seguenti attività:

* Il mittente deve rivedere la documentazione per la piattaforma all’indirizzo [Sviluppo app mittente](https://developers.google.com/cast/docs/sender_apps).
* Il ricevitore utilizza le API del ricevitore Cast per stabilire una connessione con l’app del mittente. Ad esempio:

   ```js
   window.castReceiverManager = cast.receiver.CastReceiverManager.getInstance(); 
   
   window.castReceiverManager.onReady = function (event) { /*handle event*/ }; 
   window.castReceiverManager.onSenderConnected = function (event) { /*handle event*/ }; 
   window.castReceiverManager.onSenderDisconnected = function (event) { /*handle event*/ }; 
   
   var customMessageBus = window.castReceiverManager.getCastMessageBus(MSG_NAMESPACE); 
   customMessageBus.onMessage = function (event) { /*handle messages*/ }; 
   
   window.castReceiverManager.start(); 
   ```

## Gestione dei messaggi {#section_3E4814546F5946C9B3E7A1AE384B4FF8}

Per inviare messaggi al destinatario, consulta la documentazione relativa alla piattaforma del mittente.

>[!IMPORTANT]
>
>Devi includere lo spazio dei nomi del messaggio personalizzato, `MSG_NAMESPACE` in tutti i messaggi.

Per l’app ricevente, segui la documentazione relativa alle API ricevitore cast.

**Esempio di messaggio mittente basato su Chrome**

```js
window.session.sendMessage(MSG_NAMESPACE, message, successCallback, errorCallback); //https://developers.google.com/cast/docs/reference/chrome/chrome.cast.Session#sendMessage
```

**Gestione degli eventi dei mittenti basati su Chrome**

Associa i gestori eventi agli elementi dell’interfaccia utente che invieranno messaggi quando vengono attivati gli eventi corrispondenti. Ad esempio, per un’app mittente basata su Chrome, l’evento di ricerca potrebbe essere inviato nel modo seguente:

```js
document.getElementById("#seekBar").addEventListener("click", seekEventHandler); 
   
function seekEventHandler(event) { 
    seekMessage = { type: "seek", seekTo: player.currentTime }; //player is an instance of AdobePSDK.MediaPlayer 
    window.session.sendMessage(MSG_NAMESPACE, seekMessage, successCallback, errorCallback); 
} 
```

**Gestione dei messaggi del ricevente**

Dall’app ricevente, ecco un esempio di come gestire il messaggio di ricerca:

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
