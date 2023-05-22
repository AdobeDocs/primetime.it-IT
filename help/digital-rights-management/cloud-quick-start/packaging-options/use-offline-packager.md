---
title: Utilizza il pacchetto offline di Primetime incluso
description: Utilizza il pacchetto offline di Primetime incluso
copied-description: true
exl-id: 6a1d0dc3-8906-4de5-8351-890c1cf31efd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Utilizza il pacchetto offline di Primetime incluso{#use-the-included-primetime-offline-packager}

Primetime Java Packager è preconfigurato con la maggior parte delle impostazioni necessarie per creare pacchetti di contenuti. Sono disponibili solo alcune aree da aggiornare per iniziare.

## Aggiorna proprietà packager {#section_99904D35E99944A28FF43D924E516CC2}

Contesto dell&#39;attività corrente

* Aggiorna le seguenti proprietà packager prima di utilizzare il file di configurazione per creare un pacchetto del contenuto:

### Proprietà file di configurazione XML fornite dall&#39;utente

| Nome proprietà | Descrizione |
|---|---|
| `policy_file` | percorso del file di criteri. Adobe fornisce diversi criteri preconfigurati tra cui scegliere. |
| `pkgr_pfx` | Percorso credenziali Packager. È necessario fornire le proprie credenziali Packager emesse dall&#39;Adobe ( [!DNL .pfx]) qui. |
| `pkgr_pfx_pwd` | Password credenziali Packager. È necessario specificare la password per le credenziali Packager rilasciate dall&#39;Adobe. |

## Creare un pacchetto utilizzando la riga di comando {#section_DFBE462679E34D62963BE201FD3321F9}

Prima di creare il pacchetto del contenuto, assicurati di aver fornito tutte le informazioni richieste nel file di configurazione.

* Per creare un pacchetto di contenuto con il file di configurazione, utilizza la sintassi seguente nella riga di comando:

```
java -jar OfflinePackager.jar -conf_path [configuration filename]
```

Vengono forniti file di configurazione di esempio per creare un pacchetto del contenuto in formato HLS o HDS, denominati [!DNL config_hds.xml] e [!DNL config.hls.xml].

Il contenuto HDS o HLS verrà inviato al [!DNL /output] nella directory del kit di protezione. Per poter essere riprodotti, tutti gli artefatti scritti in questa directory devono essere ospitati su un server web HTTP.
