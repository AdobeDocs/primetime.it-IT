---
title: Versioni di Primetime Offline Packager 2.x
description: Novità delle versioni Primetime Offline Packager 2.1 e 2.3.1
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
translation-type: tm+mt
source-git-commit: b33240bf1b42b80389cd95a7ae4d3f85185a2d32
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---


# Versioni di Primetime Offline Packager {#primetime-offline-packager-x-releases}

Novità delle versioni Primetime Offline Packager 2.1 e 2.3.1

## Novità di Primetime Offline Packager 2.3.1 (ottobre 2016) {#what-s-new-in-primetime-offline-packager-oct}

La versione abilita il profilo on-demand per MPEG-DASH, aggiunge il supporto per l&#39;opzione `validate` per lo strumento PlaylistCreator e dispone di alcune correzioni chiave per gli scenari Multi-DRM elencati di seguito.

| **Numero del problema** | **Descrizione** |
|---|---|
| PTPUB-985 | HLS AAXS e Sample-AES non funzionano per la chiave generata dal packager |
| PTPUB-973 | È stato corretto un errore nell’algoritmo di crittografia per alcuni contenuti Widevine specifici. |
| PTPUB-964 | Crittografia CENC interrotta per alcuni tipi di file multimediali su determinati lettori - Android TVSDK. |
| PTPUB-954 | La crittografia Sample-AES bypassa AAXS DRM per impostazione predefinita / Errore generato con la consegna della chiave remota abilitata. |
| PTPUB-951 | Il packager offline non genera eccezioni quando key_file_path non è specificato con Widevine. Al suo posto getta NPE. |

La documentazione più recente sui pacchetti Primetime è disponibile all&#39;indirizzo [https://help.adobe.com/en_US/primetime/api/packagers/index.html](https://help.adobe.com/en_US/primetime/api/packagers/index.html).

### Problema noto nella versione 2.3.1 {#known-issue-in-version}

In questa versione sono presenti i seguenti problemi.

| **Numero del problema** | **Descrizione** |
|---|---|
| PTPUB-1005 | PlaylistCreator non fornisce l&#39;URL corretto per il file .pssh nel file .mpd del livello del set finale generato per il DRM AAXS. |
| PTPUB-1001 | PlaylistCreator dovrebbe generare un errore quando il percorso vuoto viene fornito tramite il parametro in_path |
| PTPUB-990 | Per DASH, il Packager offline non scrive il packager generato IV su disco quando sono specificati i parametri `log_vi` e `iv_out_path`. |
| PTPUB-980 | Quando il file di configurazione viene utilizzato per il packaging, l&#39;utilizzo del parametro `key_url` non rimuove le virgolette dagli input forniti. |

## Pacchetto offline Adobe Primetime 2.3.1 {#adobe-primetime-offline-packager}

### Requisiti minimi di sistema {#minimum-system-requirements}

Sistemi operativi supportati

* Linux CentOS 6.3 a 64 bit

Requisiti hardware

* Processore Intel® Pentium® 4 a 3,2 GHz (consigliato doppio processore Intel Xeon® o più veloce)

* Sistemi operativi a 64 bit: 4 GB di RAM (8 GB consigliati)

* Disco rigido

(Disk-SAS): Almeno 10 GB con 7,5.000 rpm

(Disk-SSD): Velocità di lettura/scrittura di 400 MBps

(NAS): Collegamento dedicato da 1 GB

Requisiti software

* Oracle Java SE 1.8 o versione successiva

### Pacchetto offline Adobe Primetime 2.3.1 {#adobe-primetime-offline-packager-1}

1. Scarica il software Java SE dal [sito di Oracle](https://www.oracle.com/technetwork/java/javase/downloads/index.html) e segui le istruzioni di installazione.
1. Estrai il file di archivio Adobe Primetime Offline Packager 2.3.1 denominato `PrimetimeOfflinePackager-2-3-1-b47-10142016.zip` sul disco.

### Configurazione del pacchetto offline 2.3.1 {#configuring-the-offline-packager}

Le istruzioni di configurazione sono disponibili nella guida introduttiva di Primetime Offline Packager all&#39;indirizzo [https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)

## Novità di Primetime Offline Packager 2.1 (luglio 2015) {#what-s-new-in-primetime-offline-packager-july}

Supporto per PlayReady BuyDRM (per DASH). Per ulteriori informazioni, consulta la documentazione della Guida [disponibile qui](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html).

È stato apportato il seguente miglioramento anche al packager offline.

PTPUB-780 È stato aggiunto il supporto per il tag EXT-X-START

## Novità di Primetime Offline Packager 2.0 (giugno 2015) {#what-s-new-in-primetime-offline-packager-june}

È stato aggiunto il supporto per l’output Clear DASH. Per ulteriori informazioni, consulta la documentazione del prodotto [qui](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html) .

In questa versione sono stati risolti anche i seguenti problemi.

* PTPUB-783 Offline Packager ora può gestire file WebVTT vuoti.
* PTPUB- 781 Artifact in uscita HLS su Chrome quando alcune risorse MP4 transcodificate sono imballate con il packager offline per produrre l&#39;output MBR.

## Pacchetto offline Adobe Primetime 2.1 {#adobe-primetime-offline-packager-2}

### Requisiti minimi di sistema {#minimum-system-requirements-1}

**Sistemi operativi supportati**

* Linux CentOS 6.3 a 64 bit

**Requisiti hardware**

* Processore Intel® Pentium® 4 a 3,2 GHz (consigliato doppio processore Intel Xeon® o più veloce)

* Sistemi operativi a 64 bit: 4 GB di RAM (8 GB consigliati)

* Scheda Ethernet da 1 Gb consigliata (sono supportate più schede di rete e 10 Gb)

* Disco rigido

   * (Disk-SAS): Almeno 10 GB con 7,5.000 rpm
   * (Disk-SSD): Velocità di lettura/scrittura di 400 MBps
   * (NAS): Collegamento dedicato da 1 GB

**Requisiti software**

* Oracle Java SE 1.8 o versione successiva

### Installazione del pacchetto offline 2.1 {#installing-offline-packager}

1. Scarica il software Java SE dal [sito di Oracle](https://www.oracle.com/technetwork/java/javase/downloads/index.html) e segui le istruzioni di installazione.
1. Estrai il `Adobe Primetime - Offline Packager 2.1.0 archive file, PrimetimeOfflinePackager-2-1-0-b15-07082015.zip` sul disco.

### Configurazione del pacchetto offline 2.1 {#configuring-the-offline-packager-1}

Consulta il documento Primetime Offline Packager Getting Started per i dettagli di configurazione disponibili qui [https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)

## Risorse utili {#helpful-resources}

* Consulta la documentazione completa della guida nella pagina [Informazioni e supporto per Adobe Primetime](https://helpx.adobe.com/support/primetime.html) .