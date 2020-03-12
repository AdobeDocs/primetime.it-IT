---
description: I problemi più comuni durante il test riguardano spesso gli autenticatori ExpressPlay, i protocolli di trasporto e i parametri di richiesta del servizio richiesti.
seo-description: I problemi più comuni durante il test riguardano spesso gli autenticatori ExpressPlay, i protocolli di trasporto e i parametri di richiesta del servizio richiesti.
seo-title: Risoluzione dei problemi di avvio rapido
title: Risoluzione dei problemi di avvio rapido
uuid: 42256aa0-2efc-4602-aefc-3bab2dc58ec0
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Risoluzione dei problemi di avvio rapido{#troubleshooting-your-quick-start}

I problemi più comuni durante il test riguardano spesso gli autenticatori ExpressPlay, i protocolli di trasporto e i parametri di richiesta del servizio richiesti.

Se le [!DNL curl] richieste di ExpressPlay per la generazione di token non vanno a buon fine, il corpo della risposta conterrà un messaggio di errore che spiega il motivo dell&#39;errore.

Se la generazione del token ha esito positivo, ma il contenuto continua a non essere riprodotto, controllate nei registri di redenzione del token ExpressPlay se sono presenti errori come &quot;token scaduto&quot;.

Se la generazione del token ha avuto esito positivo e la redenzione non ha avuto errori, ma il video non viene ancora riprodotto, verificate che CEK corrisponda al contenuto e che il formato del contenuto corrisponda alle capacità del dispositivo di destinazione.

Inoltre:

* Verifica di utilizzare l&#39;Autenticatore cliente corretto nelle richieste di assistenza. È facile utilizzare accidentalmente l&#39;autenticatore di produzione quando si intendeva utilizzare l&#39;autenticatore di prova. Inoltre, accertatevi di utilizzare *l&#39;autenticatore* . Ad esempio, durante il test potresti prendere in prestito il `curl` comando di qualcun altro e dimenticare di sostituire l&#39;autenticatore con il proprio.

* Controlla di utilizzare il protocollo di trasporto corretto nelle tue richieste o nei tuoi manifesti ( `https://` contro `https://`, o nel caso di FairPlay, `skd://` contro `https://` contro `https://`.

* Accertatevi di includere tutti i parametri di query richiesti per la soluzione DRM con cui state lavorando. È facile confondersi tra PlayReady e Widevine, ad esempio, perché entrambi lavorano con DASH, ma i parametri di richiesta e le configurazioni di imballaggio richiesti sono diversi.
* Confermate che il vostro account ExpressPlay disponga di crediti token sufficienti e che non sia stato esaurito.
* Confermate che il triplo dei dati DRM inviati al TVSDK sia corretto: Token ExpressPlay, URL del server licenze e tipo DRM.
* Verificate che tutti i componenti utilizzino lo stesso presupposto per l&#39;ambiente ExpressPlay in quanto esistono due ambienti, Test e Produzione.
* Tenere presente che browser diversi in genere supportano un solo DRM per il contenuto DASH.
* A partire da TVSDK 2.4, è supportato solo il profilo di creazione DASH-LIVE. (il supporto DASH-OnDemand è nella roadmap).
* Il supporto per AndroidTV PlayReady è intermittente a causa dei limiti del produttore del dispositivo. Per fornire esempi,

   * il dispositivo Razer Forge ha dei problemi con il contenuto PlayReady
   * Amazon FireTV non può utilizzare contenuto DASH con traccia audio crittografata

* A partire da TVSDK 2.4, solo i dispositivi AndroidTV in genere supportano entrambi i DRM PlayReady e Widevine. Tutti gli altri dispositivi Android in genere supportano solo Widevine.
* A partire da TVSDK 2.4, Android TVSDK attualmente richiede che la casella PSSH sia nel manifesto .mpd. Ciò è contrario allo standard DASH, che specifica che la casella PSSH può essere ovunque, come nel contenuto stesso, e non solo nel .mpd.

