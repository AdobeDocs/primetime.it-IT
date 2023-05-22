---
description: Utilizza i parametri di query opzionali pttrackingmode, pttrackingversion e pttrackingposition per ottenere URL a cui inviare informazioni di tracciamento degli annunci sul video corrente. Le risposte variano a seconda della versione di tracciamento e del fatto che il flusso video sia live o on-demand (VOD).
title: API per l'interazione dei lettori con il server manifesto
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---


# API per l&#39;interazione dei lettori con il server manifesto {#api-for-players-to-interact-with-the-manifest-server}

Utilizzare l&#39;opzione `pttrackingmode`, `pttrackingversion`, e `pttrackingposition` parametri di query per ottenere URL a cui inviare informazioni di tracciamento degli annunci sul video corrente. Le risposte variano a seconda della versione di tracciamento e del fatto che il flusso video sia live o on-demand (VOD).

## Parametri di query {#query-parameters}

**pttrackingmode**

Esempio: `pttrackingmode=simple`
Se si specifica simple, le informazioni di tracciamento verranno comunicate al server manifest.
Specificalo su una richiesta per recuperare M3U8 prima di richiedere informazioni di tracciamento.Se non lo specifichi, il server manifesto restituisce le informazioni di tracciamento nei tag #EXT-X-MARKER.
Oppure, se specifichi un valore valido diverso da semplice, viene richiamato il tracciamento lato server.

**pttrackingversion**

Esempio: `pttrackingversion=v2`
Questo parametro indica al server manifesto il formato da utilizzare per restituire le informazioni di tracciamento (vedere [Formati di file](/help/primetime-ad-insertion/~old-msapi-topics/ms-list-file-formats/ms-api-file-formats.md)).
Specificalo in una richiesta per recuperare M3U8 prima di richiedere informazioni di tracciamento.Se non lo specifichi, o se non specifichi un valore non valido, il server manifesto utilizza v1.

**pttrackingposition**

Esempio: `pttrackingposition`
Questo parametro indica al server manifesto di restituire le informazioni di tracciamento del video come oggetto JSON o VMAP nel file M3U8. Il server manifesto ignora il valore specificato e invia tutte le informazioni di tracciamento di cui dispone per quella sessione. Se non viene passato alcun valore, il server di manifesto restituisce il file M3U8 richiesto.
