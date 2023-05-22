---
description: I problemi più comuni durante il test spesso coinvolgono gli autenticatori ExpressPlay, i protocolli di trasporto e i parametri di richiesta del servizio richiesti.
title: Risoluzione dei problemi di avvio rapido
exl-id: d8908f9c-98f4-4100-a003-d3b990105dee
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---

# Risoluzione dei problemi di avvio rapido{#troubleshooting-your-quick-start}

I problemi più comuni durante il test spesso coinvolgono gli autenticatori ExpressPlay, i protocolli di trasporto e i parametri di richiesta del servizio richiesti.

Se il [!DNL curl] richieste a ExpressPlay per la generazione di token non riuscite, il corpo della risposta conterrà un messaggio di errore che spiega il motivo dell’errore.

Se la generazione del token ha esito positivo, ma il contenuto non viene ancora riprodotto, controlla i registri di rimborso del token ExpressPlay per individuare eventuali errori, ad esempio &quot;Token scaduto&quot;.

Se la generazione del token ha avuto esito positivo e il rimborso non ha avuto alcun errore, ma il video non viene ancora riprodotto, controlla che il codice CEK corrisponda al contenuto e che il formato del contenuto corrisponda alle funzionalità del dispositivo di destinazione.

Inoltre:

* Verifica di utilizzare l’Autenticatore cliente corretto nelle richieste di servizio. È facile utilizzare accidentalmente l’autenticatore di produzione quando intendevi utilizzare l’autenticatore di test. Inoltre, assicurati di utilizzare *tuo* autenticatore. Ad esempio, durante il test potresti prendere in prestito i `curl` e dimentica di sostituire nell&#39;autenticatore con il proprio.

* Verifica di utilizzare il protocollo di trasporto corretto nelle richieste o nei manifesti ( `https://` rispetto a `https://`, o nel caso di FairPlay, `skd://` rispetto a `https://` rispetto a `https://`.

* Assicurarsi di includere tutti i parametri di query richiesti per la soluzione DRM in uso. È facile confondersi tra PlayReady e Widevine, ad esempio, perché entrambi funzionano con DASH, ma i parametri di richiesta e le configurazioni di packaging richiesti sono diversi.
* Verificare che l&#39;account ExpressPlay disponga di un numero sufficiente di token e che non sia stato esaurito.
* Verificare che la tripletta dei dati DRM inviati a TVSDK sia corretta: token ExpressPlay, URL del server licenze e tipo di DRM.
* Confermare che tutti i componenti si basano sullo stesso presupposto relativo all&#39;ambiente ExpressPlay in uso, in quanto sono presenti due ambienti, Test e Produzione.
* Tieni presente che i diversi browser in genere supportano un solo DRM per i contenuti DASH.
* A partire da TVSDK 2.4, è supportato solo il profilo di pacchetto DASH-LIVE. Il supporto DASH-OnDemand è incluso nella roadmap.
* Il supporto per AndroidTV PlayReady è intermittente a causa di limitazioni del produttore del dispositivo. Per fare degli esempi,

   * il dispositivo Razer Forge presenta problemi con il contenuto PlayReady
   * Amazon FireTV non può utilizzare contenuti DASH con traccia audio crittografata

* A partire da TVSDK 2.4, solo i dispositivi AndroidTV supportano in genere sia PlayReady che Widevine DRM. Tutti gli altri dispositivi Android in genere supportano solo Widevine.
* A partire da TVSDK 2.4, Android TVSDK attualmente richiede che la casella PSSH sia nel manifesto .mpd. Questo è contrario allo standard DASH, che specifica che la casella PSSH può essere ovunque, come nel contenuto stesso, e non solo nel .mpd.
