---
description: I problemi comuni durante i test spesso coinvolgono gli autenticatori ExpressPlay, i protocolli di trasporto e i parametri richiesti per la richiesta del servizio.
title: Risoluzione dei problemi di avvio rapido
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---


# Risoluzione dei problemi di avvio rapido{#troubleshooting-your-quick-start}

I problemi comuni durante i test spesso coinvolgono gli autenticatori ExpressPlay, i protocolli di trasporto e i parametri richiesti per la richiesta del servizio.

Se le richieste [!DNL curl] di ExpressPlay per la generazione del token non riescono, il corpo della risposta conterrà un messaggio di errore che spiega il motivo dell’errore.

Se la generazione del token ha esito positivo, ma il contenuto continua a non essere riprodotto, controlla nei registri di rimborso del token ExpressPlay se sono presenti errori come &quot;Token scaduto&quot;.

Se la generazione del token è riuscita e il riscatto non ha avuto alcun errore, ma il video non viene ancora riprodotto, verifica che la CEK corrisponda al contenuto e che il formato del contenuto corrisponda alle funzionalità del dispositivo di destinazione.

Inoltre:

* Verifica di utilizzare l&#39;Autenticatore cliente corretto nelle richieste di servizio. È facile utilizzare accidentalmente l&#39;autenticatore di produzione quando si intendeva utilizzare l&#39;autenticatore di test. Inoltre, assicurati di utilizzare *il tuo* autenticatore. Ad esempio, durante il test potresti prendere in prestito il comando `curl` di qualcun altro e dimenticare di scambiare nell&#39;autenticatore per il proprio.

* Verifica di utilizzare il protocollo di trasporto appropriato nelle richieste o nei manifesti ( `https://` rispetto a `https://` oppure nel caso di FairPlay, `skd://` rispetto a `https://` rispetto a `https://`.

* Assicurati di includere tutti i parametri di query richiesti per la soluzione DRM con cui stai lavorando. È facile confondersi tra PlayReady e Widevine, ad esempio, perché entrambi lavorano con DASH, ma i parametri di richiesta e le configurazioni di packaging richiesti sono diversi.
* Conferma che il tuo account ExpressPlay disponga di crediti token sufficienti e che non sia stato esaurito.
* Verifica che il triplo dei dati DRM inviati al TVSDK sia corretto: Token ExpressPlay, URL del server di licenza e tipo DRM.
* Conferma che tutti i componenti stiano presupponendo lo stesso ambiente ExpressPlay in uso in presenza di due ambienti, Test e Produzione.
* Tieni presente che in genere i diversi browser supportano un solo DRM per il contenuto DASH.
* A partire da TVSDK 2.4, è supportato solo il profilo di packaging DASH-LIVE. (Il supporto DASH-OnDemand è nella roadmap di .)
* Il supporto per AndroidTV PlayReady è intermittente a causa di limitazioni del produttore del dispositivo. Per fornire esempi,

   * il dispositivo Razer Forge ha problemi con il contenuto PlayReady
   * Amazon FireTV non può utilizzare contenuto DASH con traccia audio crittografata

* A partire da TVSDK 2.4, solo i dispositivi AndroidTV supportano in genere i DRM PlayReady e Widevine. Tutti gli altri dispositivi Android in genere supportano solo Widevine.
* A partire da TVSDK 2.4, Android TVSDK attualmente richiede che la casella PSSH sia nel manifesto .mpd. Ciò è contrario allo standard DASH, che specifica che la casella PSSH può essere ovunque, come nel contenuto stesso, e non solo nel .mpd.

