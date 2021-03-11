---
title: Manager
description: I gestori di funzioni consentono di controllare le singole funzioni senza attraversare l’intero TVSDK alla ricerca di codice per una funzione che può essere dispersa in più posizioni.
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 2%

---


# Manager delle funzioni {#feature-managers}

I gestori di funzioni consentono di controllare le singole funzioni senza attraversare l’intero TVSDK alla ricerca di codice per una funzione che può essere dispersa in più posizioni. I gestori di funzioni condensano il codice in un’unica classe per funzione. I gestori di funzioni attendono i trigger dagli eventi TVSDK e quindi informano la classe che utilizza il gestore di funzioni per gestire il risultato. Il gestore di funzioni fornisce le informazioni richieste alla classe.

I gestori di funzioni eseguono le seguenti attività:

* **Attiva le funzioni TVSDK.**
Si tratta di chiamate di funzioni per attivare una funzione TVSDK. Ad esempio: 
`PlaybackManager.play()` viene chiamato quando l&#39;applicazione player deve avviare la riproduzione del video.

* **Ascolta gli eventi TVSDK.**
Il gestore di funzioni deve ascoltare gli eventi TVSDK per acquisire informazioni dal TVSDK. Ad esempio: 
`AdsManager` ascolta gli eventi TVSDK Ads da notificare all’avvio delle interruzioni pubblicitarie.

* **Invia gli eventi al gestore.**
Dopo che i gestori di funzioni ricevono ed elaborano gli eventi dal TVSDK, inviano una notifica al lato client per gestire l’evento. Ad esempio, dopo 
`AdsManager` riceve un evento di avvio ad break, comunica al frammento del lettore di riflettere questa modifica nell’interfaccia utente (disattiva la barra di scorrimento, mostra la sovrapposizione annuncio, ecc.).

L’implementazione di riferimento di Primetime include i seguenti gestori di funzioni:

| Gestione delle funzioni | File predefinito | Funzione |  |
|---|---|---|---|
| Riproduzione video | PlaybackManager | Riproduzione e controllo HLS, riproduzione e controllo DVR, controllo del buffer e gestione del bit rate multiplo. | Obbligatorio |
| Protezione dei contenuti DRM | DrmManager | Protezione dei contenuti. | Obbligatorio |
| Inserimento di annunci | AdsManager | Inserimento di annunci, tra cui interruzioni pubblicitarie dirette in Adobe Primetime e interruzioni pubblicitarie personalizzate. | Facoltativo |
| Sottotitoli codificati | CCManager | Sottotitoli codificati e sottotitoli VTT. | Facoltativo |
| Audio con associazione ritardata | AAManager | Audio di associazione tardiva. | Facoltativo |
| QoS | QosManager | Statistiche QoS. | Facoltativo |
| Diritto | EntitlementManager | Integrazione dell&#39;adesione all&#39;autenticazione di Primetime. | Facoltativo |

L&#39;implementazione di riferimento contiene le classi predefinite di base elencate sopra e le classi corrispondenti con il suffisso On. Le classi predefinite forniscono i comportamenti TVSDK predefiniti, mentre le classi con il suffisso On includono tutto il codice necessario per attivare la funzione TVSDK e ascoltare gli eventi TVSDK per tale funzione.

* Per le funzioni facoltative, il codice predefinito funziona come se la funzione fosse disattivata.
* Le classi con il suffisso On funzionano come se la funzione fosse attivata.