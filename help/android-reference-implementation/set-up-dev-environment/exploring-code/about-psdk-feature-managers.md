---
seo-title: Feature manager
title: Feature manager
uuid: 3d78544e-4819-4122-bfd3-01522a067aa9
description: I Feature Manager consentono di controllare le singole funzioni senza attraversare l’intero TVSDK alla ricerca di codice per una funzione che potrebbe essere distribuita in più posizioni.
seo-description: I Feature Manager consentono di controllare le singole funzioni senza attraversare l’intero TVSDK alla ricerca di codice per una funzione che potrebbe essere distribuita in più posizioni.
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 2%

---


# Manager delle funzioni {#feature-managers}

I Feature Manager consentono di controllare le singole funzioni senza attraversare l’intero TVSDK alla ricerca di codice per una funzione che potrebbe essere distribuita in più posizioni. I Feature Manager condensano il codice in un&#39;unica classe per funzione. I manager delle funzioni attendono attivatori dagli eventi TVSDK e quindi informano la classe che utilizza il manager delle funzioni per gestire il risultato. Il manager della funzione fornisce le informazioni richieste alla classe.

I manager delle funzioni eseguono le seguenti operazioni:

* **Attiva le funzionalità TVSDK.**
Si tratta di chiamate di funzioni per attivare una funzione TVSDK. Ad esempio: 
`PlaybackManager.play()` viene chiamato quando l’applicazione del lettore deve avviare la riproduzione video.

* **Ascolta gli eventi TVSDK.**
Il manager delle funzioni deve ascoltare gli eventi TVSDK per acquisire informazioni da TVSDK. Ad esempio: 
`AdsManager` ascolta gli eventi TVSDK Ads per ricevere una notifica all&#39;avvio delle interruzioni pubblicitarie.

* **Invia gli eventi al gestore.**
Una volta ricevuti ed elaborati gli eventi dal TVSDK, i manager delle funzioni inviano una notifica al lato client per gestire l&#39;evento. Ad esempio, dopo 
`AdsManager` riceve un evento di inizio dell’interruzione dell’annuncio e indica al frammento del lettore di riflettere questa modifica nell’interfaccia utente (disattivate la barra di scorrimento, visualizzate la sovrapposizione dell’annuncio, ecc.).

L&#39;implementazione di riferimento Primetime include i seguenti manager di funzioni:

| Gestione funzioni | File predefinito | Feature |  |
|---|---|---|---|
| Riproduzione video | PlaybackManager | Riproduzione e controllo HLS, riproduzione e controllo DVR, controllo buffer e gestione del bit rate multi-bit. | Obbligatorio |
| Protezione dei contenuti DRM | DrmManager | Protezione dei contenuti. | Obbligatorio |
| Inserimento annunci | AdsManager | Inserimento di annunci, inclusi  Adobe Primetime e decisione di annunci diretti e interruzione di annunci personalizzata. | Facoltativo |
| Sottotitoli codificati | CCManager | Sottotitoli codificati e sottotitoli VTT. | Facoltativo |
| Connessione audio ritardata | AAManager | Associazione audio tardiva. | Facoltativo |
| QoS | QosManager | Statistiche QoS. | Facoltativo |
| Adesione | EntitlementManager | Integrazione dell&#39;adesione con l&#39;autenticazione Primetime. | Facoltativo |

L&#39;implementazione del riferimento contiene le classi predefinite di base, elencate sopra, e le classi corrispondenti con il suffisso On. Le classi predefinite forniscono i comportamenti TVSDK predefiniti, mentre le classi con il suffisso On includono tutto il codice richiesto per attivare la funzione TVSDK e ascoltare gli eventi TVSDK per tale funzione.

* Per le funzioni facoltative, il codice predefinito funziona come se la funzione fosse disattivata.
* Le classi con il suffisso On funzionano come se la funzione fosse attivata.