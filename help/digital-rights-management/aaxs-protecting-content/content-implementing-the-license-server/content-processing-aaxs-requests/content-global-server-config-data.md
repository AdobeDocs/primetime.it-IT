---
seo-title: Dati di configurazione del server globale
title: Dati di configurazione del server globale
uuid: f6d6cb01-2645-4cd2-83ec-0272323a67cd
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---


# Dati di configurazione del server globale{#global-server-configuration-data}

Oltre alla configurazione utilizzata dal server licenze, `HandlerConfiguration` memorizza le informazioni di configurazione che possono essere inviate al client per controllare come vengono applicate le licenze. A questo scopo, è necessario creare una classe `ServerConfigData` e chiamare `HandlerConfiguration.setServerConfigData()` (queste impostazioni si applicano solo alle licenze rilasciate da questo server licenze). La tolleranza per il windback dell&#39;orologio è una proprietà che può essere impostata dal server licenze per controllare il modo in cui il client applica le licenze. Per impostazione predefinita, gli utenti possono impostare l&#39;orologio del computer indietro di 4 ore senza invalidare le licenze. Se un operatore del server licenze desidera utilizzare un&#39;impostazione diversa, il nuovo valore può essere impostato nella classe `ServerConfigData`. Quando modificate il valore di una di queste impostazioni, accertatevi di incrementare il numero di versione chiamando `setVersion()`. I nuovi valori saranno inviati al client solo se la versione sul client è inferiore alla versione corrente `ServerConfigData`.
