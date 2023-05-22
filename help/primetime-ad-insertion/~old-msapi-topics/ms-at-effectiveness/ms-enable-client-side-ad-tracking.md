---
description: Puoi abilitare il tracciamento degli annunci lato client aggiungendo i parametri pttrackingmode e pttrackingversion alla richiesta URL Bootstrap.
title: Abilitare il tracciamento degli annunci lato client
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---


# Abilitare il tracciamento degli annunci lato client {#enable-client-side-ad-tracking}

Puoi abilitare il tracciamento degli annunci lato client aggiungendo il `pttrackingmode` e `pttrackingversion` parametri della richiesta URL Bootstrap.

Con il tracciamento degli annunci lato client abilitato, puoi anche recuperare i metadati di tracciamento degli annunci utilizzando l’URL dell’API di tracciamento. Per ulteriori dettagli, consulta [Parametri di query](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/notvsdk-csat-ms-interface.md).

Per eseguire il tracciamento degli annunci lato client, utilizza l’URL dell’API di tracciamento.

1. Aggiungi i seguenti parametri di query all’URL della richiesta del server manifesto:

   * `pttrackingmode=simple`
   * `pttrackingversion={format version}`

Ad esempio:

```URL
https://. . .?. . .&pttrackingmode=simple&pttrackingversion=v1
```
