---
title: Utilizza il pacchetto offline incluso di Primetime
description: Utilizza il pacchetto offline incluso di Primetime
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# Utilizza il pacchetto offline incluso di Primetime{#use-the-included-primetime-offline-packager}

Il pacchetto Java Packager di Primetime è preconfigurato con la maggior parte delle impostazioni necessarie per creare il pacchetto del contenuto. Sono disponibili solo alcune aree da aggiornare per iniziare.

## Aggiorna le proprietà del packager {#section_99904D35E99944A28FF43D924E516CC2}

Contesto dell&#39;attività corrente

* Aggiorna le seguenti proprietà del packager prima di utilizzare il file di configurazione per creare il pacchetto del contenuto:

### Proprietà file di configurazione XML fornito dall&#39;utente

| Nome proprietà | Descrizione |
|---|---|
| `policy_file` | percorso del file dei criteri. L&#39;Adobe fornisce diversi criteri preconfigurati tra cui scegliere. |
| `pkgr_pfx` | Percorso credenziali del Packager. È necessario fornire la credenziale del packager rilasciato da un Adobe ( [!DNL .pfx]) qui. |
| `pkgr_pfx_pwd` | Password delle credenziali del Packager. È necessario fornire la password alla credenziale del packager emesso da Adobe qui. |

## Pacchetto che utilizza la riga di comando {#section_DFBE462679E34D62963BE201FD3321F9}

Prima di creare pacchetti di contenuto, assicurati di disporre di tutte le informazioni necessarie fornite nel file di configurazione.

* Per creare un pacchetto di contenuti con il file di configurazione, utilizza la seguente sintassi sulla riga di comando:

```
java -jar OfflinePackager.jar -conf_path [configuration filename]
```

Vengono forniti file di configurazione di esempio per creare un pacchetto del contenuto in formato HLS o HDS, denominati [!DNL config_hds.xml] e [!DNL config.hls.xml].

Il contenuto HDS o HLS verrà inviato alla cartella [!DNL /output] nella directory del kit di protezione. Per poter essere riprodotti, tutti gli artefatti scritti in questa directory devono essere ospitati su un server web HTTP.
