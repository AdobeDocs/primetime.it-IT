---
description: Per riprodurre il contenuto DASH derivante dalla creazione di pacchetti di contenuti, il client TVSDK dovrà ottenere la chiave di decrittazione del contenuto passata durante il processo di creazione del pacchetto nel flusso di lavoro di acquisizione chiave. La chiave di decrittazione del contenuto client viene in genere consegnata al client da un server di licenze Widevine/PlayReady in risposta a uno o più post HTTP/HTTPS dal client.
seo-description: Per riprodurre il contenuto DASH derivante dalla creazione di pacchetti di contenuti, il client TVSDK dovrà ottenere la chiave di decrittazione del contenuto passata durante il processo di creazione del pacchetto nel flusso di lavoro di acquisizione chiave. La chiave di decrittazione del contenuto client viene in genere consegnata al client da un server di licenze Widevine/PlayReady in risposta a uno o più post HTTP/HTTPS dal client.
seo-title: Panoramica del flusso di lavoro della richiesta di chiave client
title: Panoramica del flusso di lavoro della richiesta di chiave client
uuid: 2f01f0ae-adbf-42fa-a908-4b5b9410a26d
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c

---


# Flusso di lavoro richiesta chiave client {#client-key-request-workflow-overview}

Per riprodurre il contenuto DASH derivante dalla creazione di pacchetti di contenuti, il client TVSDK dovrà ottenere la chiave di decrittazione del contenuto passata durante il processo di creazione del pacchetto nel flusso di lavoro di acquisizione chiave. La chiave di decrittazione del contenuto client viene in genere consegnata al client da un server di licenze Widevine/PlayReady in risposta a uno o più post HTTP/HTTPS dal client.

Per acquisire la chiave di decrittazione del contenuto, il client PSDK deve effettuare le seguenti operazioni

* Acquisite la casella pssh del contenuto, assegnatelo alla piattaforma e ottenete in risposta a una richiesta chiave.
* Inviate la richiesta di chiave al server di licenze Widevine/PlayReady appropriato tramite HTTP POST.
* Passate la risposta del server alla piattaforma che estrarrà la chiave di decrittazione del contenuto client dalla risposta e utilizzatela per la decrittazione del contenuto.

Per inviare il POST HTTP per la richiesta di chiave, il codice deve trasmettere al client PSDK l&#39;URL del server licenze insieme a tutti i dati aggiuntivi che devono essere allegati al post. La scelta di URL e dati da trasmettere dipende dal provider di servizi Widevine/PlayReady con cui lavorate. Ad esempio, se utilizzate ExpressPlay per fornire il servizio, trasmettete l&#39;URL del server licenze ExpressPlay Widevine/PlayReady appropriato e allegate alla richiesta della chiave in uscita il token ExpressPlay associato alla chiave di crittografia del contenuto. È possibile ottenere l&#39;URL appropriato del server di licenze ExpressPlay Widevine/PlayReady dalla documentazione ExpressPlay.