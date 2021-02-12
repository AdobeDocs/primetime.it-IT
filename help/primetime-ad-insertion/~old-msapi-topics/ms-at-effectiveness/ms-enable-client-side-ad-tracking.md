---
description: Potete abilitare il tracciamento degli annunci lato client aggiungendo i parametri pttrackingmode e pttrackingversion alla richiesta dell'URL di Bootstrap.
seo-description: Potete abilitare il tracciamento degli annunci lato client aggiungendo i parametri pttrackingmode e pttrackingversion alla richiesta dell'URL di Bootstrap.
seo-title: Abilita tracciamento annunci lato client
title: Abilita tracciamento annunci lato client
uuid: 0a825756-1d9a-43c5-bc22-9b366f39fdbb
translation-type: tm+mt
source-git-commit: e1e33d3ac0aad44859cd49566331524da72ac7e4
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 1%

---


# Abilita tracciamento annunci lato client {#enable-client-side-ad-tracking}

Potete abilitare il tracciamento degli annunci lato client aggiungendo i parametri `pttrackingmode` e `pttrackingversion` alla richiesta dell&#39;URL di Bootstrap.

Con il tracciamento degli annunci lato client abilitato, potete anche recuperare i metadati di tracciamento degli annunci utilizzando l&#39;URL API di tracciamento. Per ulteriori dettagli, vedere [Parametri query](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/notvsdk-csat-ms-interface.md).

Per eseguire il tracciamento degli annunci lato client, utilizzate l&#39;URL API di tracciamento.

1. Aggiungete i seguenti parametri di query all&#39;URL della richiesta del server manifesto:

   * `pttrackingmode=simple`
   * `pttrackingversion={format version}`

Ad esempio:

```URL
https://. . .?. . .&pttrackingmode=simple&pttrackingversion=v1
```
