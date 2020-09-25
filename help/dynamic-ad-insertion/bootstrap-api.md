---
title: Bootstrap API
description: null
translation-type: tm+mt
source-git-commit: aa43834fea161c537c448b7616c9bd8f779d1a74
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---


# Bootstrap API {#bootstrap-api}

Parametri richiestiGenerazione di un programma di avvio automatico

## Descrizione parametro {#parameter-description}

| parameter | description | format |
|---|---|---|
| pabimode | Abilita l&#39;inserimento [](ad-insertion-live-linear-stream.md#partial-ad-break-support) parziale di interruzioni pubblicitarie per i flussi live. Valori possibili:true per abilitare l&#39;opzione di disattivazione (impostazione predefinita disattivata) | HLS/DASH |
| ptadwindow | Durata (in secondi) della finestra di lookback e di decisione — quanto tempo indietro Primetime  Ad Insertion cercherà segnali pubblicitari quando un utente DVR partecipa allo streaming. Un valore pari a zero disattiverà il mid-roll e le decisioni nel manifesto iniziale, con la ripresa delle decisioni solo dopo il primo aggiornamento. Questo parametro è utile per disabilitare l&#39;inserimento di annunci nelle sessioni che possono durare solo pochi secondi (ovvero il capovolgimento del canale). Valori possibili:stringa numerica da 0 a 1800 (predefinito 1800) | Solo HLS |
| ptassetid | ID univoco del contenuto assegnato e gestito dall&#39;editore.  Obbligatorio se utilizzato in combinazione con Akamai Ad Scaler. | HLS/DASH |
| ptcdn | Elenco di uno o più CDN per l’hosting di risorse transcodificate. Per ulteriori informazioni, consultate [Supporto](multi-cdn-support.md)per più CDN. Valori possibili: akamai, livello3, llnw (reti a luci ridotte), comcastPer impostazione predefinita, vengono utilizzati CDN  Ad Insertion Primetime | HLS/DASH |
| ptcueformat | Il formato specificato dei tag da eseguire per la decisione degli annunci (ad esempio, scte35). Valori possibili: dpissimple, dpiscte35, elemental Per i formati di cue personalizzati, contattare il rappresentante tecnico per il valore da utilizzare per il caso d&#39;uso | HLS/DASH |
| ptfailover | Segnala al server manifesto di identificare i flussi primari e di failover specificati nella playlist principale e di trattarli come set disgiunti. Questo semplifica il failover e impedisce gli errori di temporizzazione. (solo per i dispositivi Apple HLS). Per ulteriori informazioni, vedere [Facilitazione della commutazione del lettore HLS](hls-switching-to-failover.md) | Solo HLS |
| ptmulticall | Se abilitata, viene effettuata una richiesta di annuncio separata per ogni valore trovato in una risorsa VOD.  Per impostazione predefinita, Primetime  Ad Insertion tenterà di raccogliere tutte le informazioni valide e di inviarle al server di annunci in una sola richiesta. Valori possibili:true per abilitare l&#39;opzione di disattivazione (impostazione predefinita disattivata) | HLS/DASH |
| pttagds | Abilita l&#39;inserimento di tag EXT-X-DISCONTINUITY-SEQUENCE nelle intestazioni HLS.Valori possibili:true per abilitare la disattivazione (impostazione predefinita disattivata) | Solo HLS |
| pitimeline | Una stringa contenente la timeline desiderata per la posizione e il contenuto degli annunci, che esclude e interrompe il flusso di contenuti. [ Vedere Formato timeline VOD ] | HLS/DASH |
| pattoken | Abilita schemi di protezione token di autorizzazione per frammenti di contenuto/segmenti per CDN Valori possibili: akamai, llnw (limelight), ctl (centurylink) (la token predefinita è disabilitata) | HLS/DASH |
| pttrackingmode | Abilita schemi di tracciamento annunci:valori possibili:semplice per gli annunci pubblicitari client-side per gli annunci server-side semplice per il monitoraggio degli annunci client-server per il monitoraggio ibrido degli annunci client/server (per impostazione predefinita, non viene eseguito il tracciamento degli annunci) | HLS/DASH |
| pttrackingversion |  |  |
| ptadtimeout (come in 20.9.2) |  |  |
| ptparallelstream (come in 20.9.3) |  |  |
