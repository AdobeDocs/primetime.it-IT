---
description: Per riprodurre il contenuto DASH risultante dal pacchetto del contenuto, il client TVSDK dovrà ottenere la chiave di decrittografia del contenuto passata durante il processo di creazione del pacchetto nel flusso di lavoro di acquisizione della chiave. La chiave di decrittografia del contenuto client viene in genere distribuita al client da un server licenze Widevine/PlayReady in risposta a uno o più post HTTP/HTTPS dal client.
title: Panoramica del flusso di lavoro Richiesta chiave client
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# Flusso di lavoro per richiesta chiave client {#client-key-request-workflow-overview}

Per riprodurre il contenuto DASH risultante dal pacchetto del contenuto, il client TVSDK dovrà ottenere la chiave di decrittografia del contenuto passata durante il processo di creazione del pacchetto nel flusso di lavoro di acquisizione della chiave. La chiave di decrittografia del contenuto client viene in genere distribuita al client da un server licenze Widevine/PlayReady in risposta a uno o più post HTTP/HTTPS dal client.

Per acquisire la chiave di decrittografia del contenuto, il client PSDK deve effettuare le seguenti operazioni

* Prendi la casella PSH del contenuto, passala alla piattaforma e ottieni in risposta una richiesta chiave.
* Inviare la richiesta di chiave al server di licenze Widevine/PlayReady appropriato tramite HTTP POST.
* Passa la risposta del server alla piattaforma che estrarrà la chiave di decrittografia del contenuto client dalla risposta e la utilizzerà per la decrittografia del contenuto.

Per inviare il POST HTTP per la richiesta della chiave, il codice deve passare al client PSDK l’URL del server licenze insieme a tutti i dati aggiuntivi che devono essere allegati al post. La scelta dell&#39;URL e dei dati da trasmettere dipende dal provider di servizi Widevine/PlayReady con cui lavori. Ad esempio, se si utilizza ExpressPlay per fornire il servizio, si passa l&#39;URL appropriato del server di licenze ExpressPlay Widevine/PlayReady e si allega alla richiesta della chiave in uscita il token ExpressPlay associato alla chiave di crittografia del contenuto. È possibile ottenere l&#39;URL appropriato del server di licenze ExpressPlay Widevine/PlayReady dalla documentazione di ExpressPlay.
