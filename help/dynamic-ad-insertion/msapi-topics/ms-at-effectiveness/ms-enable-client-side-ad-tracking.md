---
description: Potete abilitare il tracciamento degli annunci lato client aggiungendo i parametri pttrackingmode e pttrackingversion alla richiesta URL di Bootstrap.
seo-description: Potete abilitare il tracciamento degli annunci lato client aggiungendo i parametri pttrackingmode e pttrackingversion alla richiesta URL di Bootstrap.
seo-title: Abilita tracciamento annunci lato client
title: Abilita tracciamento annunci lato client
uuid: 0a825756-1d9a-43c5-bc22-9b366f39fdbb
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9

---


# Abilita tracciamento annunci lato client {#enable-client-side-ad-tracking}

Potete abilitare il tracciamento degli annunci lato client aggiungendo i parametri `pttrackingmode` e `pttrackingversion` alla richiesta URL di Bootstrap.

Con il tracciamento degli annunci lato client abilitato, potete anche recuperare i metadati di tracciamento degli annunci utilizzando l&#39;URL API di tracciamento. Per ulteriori dettagli, consultate Parametri [](../../msapi-topics/ms-at-effectiveness/notvsdk-csat-ms-interface.md)query.

Per eseguire il tracciamento degli annunci lato client, utilizzate l&#39;URL API di tracciamento.

1. Aggiungete i seguenti parametri di query all&#39;URL della richiesta del server manifesto:

   * `pttrackingmode=simple`
   * `pttrackingversion={format version}`

Ad esempio:

```
https://. . .?. . .&pttrackingmode=simple&pttrackingversion=v1
```
