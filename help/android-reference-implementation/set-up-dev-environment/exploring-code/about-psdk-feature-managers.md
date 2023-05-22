---
title: Feature manager
description: I gestori di funzioni consentono di controllare singole funzioni senza attraversare l’intero TVSDK alla ricerca di codice per una funzione che potrebbe essere dispersa in più posizioni.
exl-id: dbf2dc8b-6067-4d94-9c3c-553452b7ffd9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# Feature manager {#feature-managers}

I gestori di funzioni consentono di controllare singole funzioni senza attraversare l’intero TVSDK alla ricerca di codice per una funzione che potrebbe essere dispersa in più posizioni. I gestori di feature condensano il codice in una classe per feature. I gestori di funzionalità attendono i trigger dagli eventi TVSDK e quindi informano la classe che utilizza il gestore di funzionalità per gestire il risultato. Il gestore delle feature fornisce le informazioni richieste alla classe.

I gestori di funzionalità eseguono i seguenti task:

* **Attiva le funzioni di TVSDK.**
Si tratta di chiamate di funzione per attivare una funzione TVSDK. Ad esempio: 
`PlaybackManager.play()` viene chiamato quando l’applicazione del lettore deve avviare la riproduzione del video.

* **Ascolta gli eventi TVSDK.**
Il gestore delle funzioni deve ascoltare gli eventi TVSDK per acquisire informazioni da TVSDK. Ad esempio: 
`AdsManager` ascolta gli eventi TVSDK Ads per ricevere notifiche all’avvio delle interruzioni pubblicitarie.

* **Invia eventi al gestore.**
Dopo aver ricevuto ed elaborato gli eventi da TVSDK, i gestori delle funzioni inviano una notifica al lato client per gestire l’evento. Ad esempio, dopo 
`AdsManager` riceve un evento di inizio dell’interruzione pubblicitaria, che indica al frammento del lettore di riflettere questa modifica nell’interfaccia utente (disabilita la barra di scorrimento, mostra la sovrapposizione pubblicitaria, ecc.).

L’implementazione di riferimento di Primetime include i seguenti gestori di funzioni:

| Gestione delle funzioni | File predefinito | Funzionalità |  |
|---|---|---|---|
| Riproduzione video | PlaybackManager | Riproduzione e controllo HLS, riproduzione e controllo DVR, controllo buffer e gestione velocità multi-bit. | Obbligatorio |
| Protezione dei contenuti DRM | DrmManager | Protezione dei contenuti. | Obbligatorio |
| Inserimento di annunci | AdsManager | Inserimento di annunci, inclusa l’interruzione pubblicitaria diretta e l’interruzione pubblicitaria personalizzata per Adobe Primetime ad decisioning. | Facoltativo |
| Sottotitoli | CCManager | Sottotitoli e sottotitoli VTT. | Facoltativo |
| Audio di associazione tardiva | AAManager | Audio di associazione tardiva. | Facoltativo |
| QoS | QosManager | Statistiche QoS. | Facoltativo |
| Diritto | GestioneDiritti | Integrazione dei diritti di autenticazione Primetime. | Facoltativo |

L’implementazione di riferimento contiene le classi predefinite di base elencate sopra e le classi corrispondenti con il suffisso On. Le classi predefinite forniscono i comportamenti TVSDK predefiniti, mentre le classi con il suffisso On includono tutto il codice necessario per attivare la funzione TVSDK e ascoltare gli eventi TVSDK per tale funzione.

* Per le funzioni facoltative, il codice predefinito funziona come se la funzione fosse disattivata.
* Le classi con il suffisso On funzionano come se la funzione fosse attivata.
