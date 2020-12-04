---
seo-title: Utilizzare il pacchetto offline Primetime incluso
title: Utilizzare il pacchetto offline Primetime incluso
uuid: 16b535a9-81b5-43bc-9e42-a64eb6649d9a
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# Utilizzate il pacchetto offline Primetime incluso{#use-the-included-primetime-offline-packager}

Primetime Java Packager viene preconfigurato con la maggior parte delle impostazioni necessarie per creare pacchetti di contenuto. Per iniziare, è necessario aggiornare solo alcune aree.

## Aggiorna proprietà pacchetto {#section_99904D35E99944A28FF43D924E516CC2}

Contesto per l&#39;attività corrente

* Aggiornate le seguenti proprietà del packager prima di usare il file di configurazione per creare il pacchetto del contenuto:

### Proprietà del file di configurazione XML fornito dall&#39;utente

| Nome proprietà | Descrizione |
|---|---|
| `policy_file` | percorso del file dei criteri.  Adobe fornisce diversi criteri preconfigurati tra cui scegliere. |
| `pkgr_pfx` | Percorso credenziali Packager. È necessario fornire  credenziale del packager emesso dal Adobe ( [!DNL .pfx]) qui. |
| `pkgr_pfx_pwd` | Password credenziali Packager. È necessario fornire la password alla credenziale  packager emessa dal Adobe. |

## Pacchetto che utilizza la riga di comando {#section_DFBE462679E34D62963BE201FD3321F9}

Prima di creare pacchetti di contenuto, accertatevi di disporre di tutte le informazioni necessarie fornite nel file di configurazione.

* Per creare pacchetti di contenuto con il file di configurazione, utilizzate la seguente sintassi sulla riga di comando:

```
java -jar OfflinePackager.jar -conf_path [configuration filename]
```

Vengono forniti file di configurazione di esempio per il pacchetto del contenuto in formato HLS o HDS, denominati [!DNL config_hds.xml] e [!DNL config.hls.xml].

Il contenuto HDS o HLS verrà trasmesso nella cartella [!DNL /output] nella directory del kit di protezione. Per poter essere riprodotti, tutti gli artifact scritti in questa directory devono essere ospitati su un server Web HTTP.
