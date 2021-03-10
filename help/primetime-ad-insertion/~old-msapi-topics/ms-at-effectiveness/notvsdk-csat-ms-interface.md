---
description: Utilizza i parametri di query opzionali pttrackingmode, pttrackingversion e pttrackingposition per ottenere gli URL a cui inviare le informazioni di tracciamento degli annunci sul video corrente. Le risposte variano a seconda della versione di tracciamento e se il flusso video è live o on demand (VOD).
title: API per consentire ai lettori di interagire con il server manifest
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---


# API per consentire ai lettori di interagire con il server manifesto {#api-for-players-to-interact-with-the-manifest-server}

Utilizza i parametri di query `pttrackingmode`, `pttrackingversion` e `pttrackingposition` facoltativi per ottenere gli URL a cui inviare le informazioni di tracciamento degli annunci sul video corrente. Le risposte variano a seconda della versione di tracciamento e se il flusso video è live o on demand (VOD).

## Parametri query {#query-parameters}

**pttrackingmode**

Esempio: `pttrackingmode=simple`
Se si specifica un valore semplice, indica al server manifesto che si desidera tenere traccia delle informazioni.
Specificalo su una richiesta per recuperare l&#39;M3U8 prima di richiedere le informazioni di tracciamento.Quando non lo specifichi, il server manifest restituisce le informazioni di tracciamento nei tag #EXT-X-MARKER.
Oppure, se si specifica un valore valido diverso da semplice, viene richiamato il tracciamento lato server.

**pttrackingversion**

Esempio: `pttrackingversion=v2`
Questo parametro indica al server manifesto il formato da utilizzare per restituire le informazioni di tracciamento (vedere [Formati di file](/help/primetime-ad-insertion/~old-msapi-topics/ms-list-file-formats/ms-api-file-formats.md)).
Specifica su una richiesta di recuperare l&#39;M3U8 prima di richiedere le informazioni di tracciamento.Se non lo specifichi o non specifichi un valore non valido, il server manifesto utilizza v1.

**pttrackingposition**

Esempio: `pttrackingposition`
Questo parametro comunica al server manifesto di restituire le informazioni di tracciamento del video come oggetto JSON o VMAP nel file M3U8.Il server manifesto ignora il valore specificato e invia tutte le informazioni di tracciamento di cui dispone per quella sessione. Se non viene passato alcun valore, il server manifesto restituisce il file M3U8 richiesto.
