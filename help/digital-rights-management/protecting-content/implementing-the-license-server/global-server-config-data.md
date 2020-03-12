---
seo-title: Dati di configurazione del server globale
title: Dati di configurazione del server globale
uuid: a1557b3e-9a08-4623-a62d-8ebc308eae15
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Dati di configurazione del server globale{#global-server-configuration-data}

Oltre alla configurazione utilizzata dal server licenze, `HandlerConfiguration` memorizza le informazioni di configurazione che possono essere inviate al client per controllare come vengono applicate le licenze. Questa operazione viene eseguita creando una `ServerConfigData` classe e chiamando `HandlerConfiguration.setServerConfigData()`. Queste impostazioni si applicano solo alle licenze rilasciate da questo server licenze.

La tolleranza per il windback dell&#39;orologio è una proprietà che può essere impostata dal server licenze per controllare il modo in cui il client applica le licenze. Per impostazione predefinita, gli utenti possono impostare l&#39;orologio del computer indietro di 4 ore senza invalidare le licenze. Se un operatore del server licenze desidera utilizzare un&#39;impostazione diversa, il nuovo valore può essere impostato nella `ServerConfigData` classe. Quando modificate il valore di una di queste impostazioni, accertatevi di incrementare il numero di versione chiamando `setVersion()`. I nuovi valori vengono inviati al client solo se la versione sul client è precedente alla `ServerConfigData` versione corrente.
