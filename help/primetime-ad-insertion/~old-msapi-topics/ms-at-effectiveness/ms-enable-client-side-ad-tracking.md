---
description: Puoi abilitare il tracciamento degli annunci lato client aggiungendo i parametri pttrackingmode e pttrackingversion alla richiesta dell'URL Bootstrap.
title: Abilita tracciamento annunci lato client
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 2%

---


# Abilita tracciamento annunci lato client {#enable-client-side-ad-tracking}

Puoi abilitare il tracciamento degli annunci lato client aggiungendo i parametri `pttrackingmode` e `pttrackingversion` alla richiesta dell’URL Bootstrap.

Se è abilitato il tracciamento degli annunci lato client, puoi anche recuperare i metadati del tracciamento degli annunci utilizzando l’URL API di tracciamento. Per ulteriori dettagli, consulta [Parametri query](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/notvsdk-csat-ms-interface.md).

Per eseguire il tracciamento degli annunci lato client, utilizza l’URL API di tracciamento.

1. Aggiungi i seguenti parametri di query all&#39;URL della richiesta del server manifest:

   * `pttrackingmode=simple`
   * `pttrackingversion={format version}`

Ad esempio:

```URL
https://. . .?. . .&pttrackingmode=simple&pttrackingversion=v1
```
