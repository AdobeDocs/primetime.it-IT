---
title: Dati di configurazione server globale
description: Dati di configurazione server globale
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# Dati di configurazione server globale{#global-server-configuration-data}

Oltre alla configurazione utilizzata dal server licenze, `HandlerConfiguration` memorizza le informazioni di configurazione che possono essere inviate al client per controllare come vengono applicate le licenze. Ciò avviene tramite la creazione di un `ServerConfigData` classe e chiamata `HandlerConfiguration.setServerConfigData()`. Queste impostazioni si applicano solo alle licenze rilasciate da questo server licenze.

La tolleranza di clock windback è una proprietà che può essere impostata dal server licenze per controllare il modo in cui il client applica le licenze. Per impostazione predefinita, gli utenti possono impostare l&#39;orologio del computer indietro di 4 ore senza invalidare le licenze. Se un operatore del server licenze desidera utilizzare un&#39;impostazione diversa, il nuovo valore può essere impostato nel `ServerConfigData` classe. Quando modifichi il valore di una di queste impostazioni, accertati di incrementare il numero di versione chiamando `setVersion()`. I nuovi valori vengono inviati al client solo se la versione del client è precedente a quella corrente `ServerConfigData` versione.
