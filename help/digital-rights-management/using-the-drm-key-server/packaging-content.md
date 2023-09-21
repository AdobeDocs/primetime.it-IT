---
title: Contenuto pacchetto
description: Contenuto pacchetto
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# Contenuto pacchetto{#packaging-content}

Quando si crea un pacchetto di contenuto per la consegna della chiave remota, utilizzare un criterio che specifichi che la consegna della chiave remota è obbligatoria. L&#39;URL del server chiavi deve essere incluso in M3U8 (file manifesto) per il contenuto HLS. L&#39;URL del server chiavi DRM Primetime ha il formato:

```
https://key-server-host:port/faxsks/tenant-name/key
```

Ad esempio, per Nome host server chiavi [!DNL mykeyserver.com] ascolto sulla porta 443 e un tenant denominato `tenant1`, l’URL del server chiave da specificare in M3U8 è:

```
https://mykeyserver.com:443/faxsks/tenant1/key
```

Lo stesso URL può essere utilizzato per i client iOS e Xbox 360. In alternativa, se il server è configurato con tenant separati per ciascun tipo di client, è possibile utilizzare URL diversi.

Lo stesso contenuto può essere riprodotto su client che non richiedono un server chiavi, purché l&#39;URL del server licenze punti a un server licenze in esecuzione configurato correttamente.
