---
description: Utilizzate i parametri di query opzionali pttrackingmode, pttrackingversion e pttrackingposition per ottenere gli URL a cui inviare le informazioni di tracciamento annunci sul video corrente. Le risposte variano in base alla versione di tracciamento e se il flusso video è live o on demand (VOD).
seo-description: Utilizzate i parametri di query opzionali pttrackingmode, pttrackingversion e pttrackingposition per ottenere gli URL a cui inviare le informazioni di tracciamento annunci sul video corrente. Le risposte variano in base alla versione di tracciamento e se il flusso video è live o on demand (VOD).
seo-title: API per l'interazione dei lettori con il server manifesto
title: API per l'interazione dei lettori con il server manifesto
uuid: ab7a19e7-6c28-4960-a56b-3b33c525e6b3
translation-type: tm+mt
source-git-commit: e1e33d3ac0aad44859cd49566331524da72ac7e4
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---


# API per l&#39;interazione dei lettori con il server manifesto {#api-for-players-to-interact-with-the-manifest-server}

Utilizzate i parametri di query opzionali `pttrackingmode`, `pttrackingversion` e `pttrackingposition` per ottenere gli URL a cui inviare le informazioni di tracciamento annunci sul video corrente. Le risposte variano in base alla versione di tracciamento e se il flusso video è live o on demand (VOD).

## Parametri query {#query-parameters}

**pttrackingmode**

Esempio: `pttrackingmode=simple`
Specificando semplicemente, indica al server del manifesto che si desidera tenere traccia delle informazioni.
Specificatelo su una richiesta per recuperare l&#39;M3U8 prima di richiedere le informazioni di tracciamento. Quando non lo specificate, il server di manifesto restituisce le informazioni di tracciamento nei tag #EXT-X-MARKER.
Oppure, se specificate un valore valido diverso dal semplice tracciamento lato server, viene richiamato.

**pttrackingversion**

Esempio: `pttrackingversion=v2`
Questo parametro indica al server di manifesto il formato da utilizzare per restituire le informazioni di tracciamento (vedere [Formati di file](/help/primetime-ad-insertion/~old-msapi-topics/ms-list-file-formats/ms-api-file-formats.md)).
Specificatelo su una richiesta per recuperare l&#39;M3U8 prima di richiedere le informazioni di tracciamento. Se non lo specificate o non specificate un valore non valido, il server manifesto utilizza v1.

**pttrackingposition**

Esempio: `pttrackingposition`
Questo parametro indica al server di manifesto di restituire le informazioni di tracciamento del video come oggetto JSON o VMAP nel file M3U8. Il server di manifesto ignora il valore specificato e invia tutte le informazioni di tracciamento di cui dispone per quella sessione. Se non viene passato alcun valore, il server manifesto restituisce il file M3U8 richiesto.
