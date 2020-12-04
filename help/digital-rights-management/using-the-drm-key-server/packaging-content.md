---
seo-title: Creazione di pacchetti di contenuto
title: Creazione di pacchetti di contenuto
uuid: 366c8470-b7ef-4a39-83c2-151ba9be9a32
translation-type: tm+mt
source-git-commit: 1547eb3dd220fafc08df923f40504736c16a866c
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---


# Creazione di pacchetti di contenuto{#packaging-content}

Quando si crea il pacchetto per la consegna di chiavi remote, utilizzare un criterio che specifica che è necessaria la consegna di chiavi remote. L’URL del server delle chiavi deve essere incluso nel file M3U8 (file manifesto) per il contenuto HLS. L&#39;URL del server di chiavi DRM Primetime ha il formato seguente:

```
https://key-server-host:port/faxsks/tenant-name/key
```

Ad esempio, per il nome host del server chiavi [!DNL mykeyserver.com] in ascolto sulla porta 443 e un tenant denominato `tenant1`, l&#39;URL del server chiave da specificare in M3U8 è:

```
https://mykeyserver.com:443/faxsks/tenant1/key
```

Lo stesso URL può essere utilizzato per client iOS e Xbox 360. Oppure, se il server è configurato con tenant separati per ogni tipo di client, è possibile utilizzare URL diversi.

Lo stesso contenuto può essere riprodotto su client che non richiedono un server chiave, purché l&#39;URL del server licenze punti a un server licenze in esecuzione configurato correttamente.
