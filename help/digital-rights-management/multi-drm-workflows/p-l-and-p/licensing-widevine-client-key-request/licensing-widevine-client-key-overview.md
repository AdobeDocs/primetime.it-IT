---
description: Per riprodurre il contenuto DASH risultante dalla creazione di pacchetti di contenuti, il client TVSDK dovrà ottenere la chiave di decrittografia del contenuto passata durante il processo di creazione del pacchetto nel flusso di lavoro di acquisizione chiave. La chiave di decrittografia del contenuto client viene generalmente consegnata al client da un server di licenza Widevine/PlayReady in risposta a uno o più post HTTP/HTTPS dal client.
title: Panoramica del flusso di lavoro della richiesta di chiave client
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---


# Flusso di lavoro di richiesta della chiave client {#client-key-request-workflow-overview}

Per riprodurre il contenuto DASH risultante dalla creazione di pacchetti di contenuti, il client TVSDK dovrà ottenere la chiave di decrittografia del contenuto passata durante il processo di creazione del pacchetto nel flusso di lavoro di acquisizione chiave. La chiave di decrittografia del contenuto client viene generalmente consegnata al client da un server di licenza Widevine/PlayReady in risposta a uno o più post HTTP/HTTPS dal client.

Per acquisire la chiave di decrittografia del contenuto, il client PSDK deve effettuare le seguenti operazioni

* Prendi la casella pssh del contenuto, assegnalo alla piattaforma e ottieni in risposta a una richiesta chiave.
* Invia la richiesta di chiave al server di licenza Widevine/PlayReady appropriato tramite un HTTP POST.
* Passa la risposta del server alla piattaforma che estrarrà la chiave di decrittografia del contenuto client dalla risposta e la utilizzerà per la decrittografia del contenuto.

Per inviare il POST HTTP per la richiesta di chiave, il codice deve trasmettere al client PSDK l&#39;URL del server di licenza, insieme a tutti i dati aggiuntivi che devono essere allegati al post. La scelta dell&#39;URL e dei dati da trasmettere dipende dal provider di servizi Widevine/PlayReady con cui lavori. Ad esempio, se utilizzi ExpressPlay per fornire il servizio, passi l’URL del server di licenza ExpressPlay Widevine/PlayReady appropriato e allega alla richiesta della chiave in uscita il token ExpressPlay associato alla chiave di crittografia del contenuto. Puoi ottenere l&#39;URL appropriato del server di licenza ExpressPlay Widevine/PlayReady dalla documentazione ExpressPlay.