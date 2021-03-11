---
title: Contenuto del pacchetto
description: Contenuto del pacchetto
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---


# Contenuto del pacchetto{#packaging-content}

Quando si crea un pacchetto di contenuto per la consegna di chiavi remote, utilizzare un criterio che specifichi che è necessaria la consegna di chiavi remote. L&#39;URL del server chiavi deve essere incluso nel file M3U8 (file manifesto) per il contenuto HLS. L&#39;URL del server chiavi DRM di Primetime ha il formato seguente:

```
https://key-server-host:port/faxsks/tenant-name/key
```

Ad esempio, per il nome host del server chiavi [!DNL mykeyserver.com] in ascolto sulla porta 443 e un tenant denominato `tenant1`, l&#39;URL del server chiave da specificare nell&#39;M3U8 è:

```
https://mykeyserver.com:443/faxsks/tenant1/key
```

Lo stesso URL può essere utilizzato per client iOS e Xbox 360. Oppure, se il server è configurato con tenant separati per ogni tipo di client, è possibile utilizzare URL diversi.

Lo stesso contenuto può essere riprodotto su client che non richiedono un server chiave, purché l’URL del server licenze punti a un server licenze in esecuzione correttamente configurato.
