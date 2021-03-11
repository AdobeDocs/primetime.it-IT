---
title: Dati di configurazione del server globale
description: Dati di configurazione del server globale
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---


# Dati di configurazione del server globale{#global-server-configuration-data}

Oltre alla configurazione utilizzata dal server licenze, `HandlerConfiguration` memorizza le informazioni di configurazione che possono essere inviate al client per controllare il modo in cui vengono applicate le licenze. Questo viene fatto creando una classe `ServerConfigData` e chiamando `HandlerConfiguration.setServerConfigData()` (queste impostazioni si applicano solo alle licenze rilasciate da questo server licenze). La tolleranza del tempo indesiderato è una proprietà che può essere impostata dal server licenze per controllare il modo in cui il cliente applica le licenze. Per impostazione predefinita, gli utenti possono impostare l&#39;orologio della macchina indietro di 4 ore senza invalidare le licenze. Se un operatore del server di licenza desidera utilizzare un&#39;impostazione diversa, il nuovo valore può essere impostato nella classe `ServerConfigData` . Quando modifichi il valore di una di queste impostazioni, assicurati di incrementare il numero di versione chiamando `setVersion()`. I nuovi valori verranno inviati al client solo se la versione sul client è inferiore alla versione corrente `ServerConfigData`.
