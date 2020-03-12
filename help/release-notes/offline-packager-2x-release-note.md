---
title: Versioni Primetime Offline Packager 2.x
seo-title: Versioni Primetime Offline Packager 2.x
description: Novità delle release Primetime Offline Packager 2.1 e 2.3.1
seo-description: Novità delle release Primetime Offline Packager 2.1 e 2.3.1
uuid: 01926a10-890d-477d-b832-e22847d957e0
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
discoiquuid: 933a0711-846a-4bb7-bf51-b300822a93d4
translation-type: tm+mt
source-git-commit: e644e8497e118e2d03e72bef727c4ce1455d68d6

---


# Rilasci di Primetime Offline Packager {#primetime-offline-packager-x-releases}

Novità delle release Primetime Offline Packager 2.1 e 2.3.1

## Novità di Primetime Offline Packager 2.3.1 (ottobre 2016) {#what-s-new-in-primetime-offline-packager-oct}

La release abilita il profilo on-demand per MPEG-DASH, aggiunge il supporto per l&#39; `validate` opzione per lo strumento PlaylistCreator e dispone di alcune correzioni chiave per gli scenari Multi-DRM elencati di seguito.

| **Numero edizione** | **Descrizione** |
|---|---|
| PTPUB-985 | HLS AAXS e Sample-AES non funzionano per la chiave generata dal packager |
| PTPUB-973 | È stato corretto un errore nell&#39;algoritmo di cifratura per alcuni contenuti Widevine specifici |
| PTPUB-964 | Cifratura CENC interrotta per alcuni tipi di supporti su determinati lettori - Android TVSDK. |
| PTPUB-954 | La cifratura Sample-AES bypassa il DRM AAXS per impostazione predefinita / Errore restituito con la consegna della chiave remota abilitata. |
| PTPUB-951 | Il packager offline non genera eccezioni quando key_file_path non è specificato con Widevine. Al posto di ciò, getta il NPE. |

La documentazione più recente di Primetime Packager è disponibile all&#39;indirizzo [https://help.adobe.com/en_US/primetime/api/packagers/index.html](https://help.adobe.com/en_US/primetime/api/packagers/index.html).

### Problema noto nella versione 2.3.1 {#known-issue-in-version}

In questa versione sono presenti i seguenti problemi.

| **Numero edizione** | **Descrizione** |
|---|---|
| PTPUB-1005 | PlaylistCreator non fornisce l&#39;URL corretto per il file .pssh nel file .mpd del livello del set finale generato per il DRM AAXS. |
| PTPUB-1001 | PlaylistCreator dovrebbe generare un errore quando un percorso vuoto viene fornito tramite il parametro in_path |
| PTPUB-990 | Per DASH, Offline Packager non scrive il packager generato IV su disco quando vengono specificati i parametri `log_vi` e `iv_out_path` . |
| PTPUB-980 | Quando il file di configurazione viene utilizzato per la creazione di pacchetti, l&#39;uso del parametro `key_url` non rimuove le virgolette dagli input forniti. |

## Adobe Primetime Offline Packager 2.3.1 {#adobe-primetime-offline-packager}

### Requisiti minimi di sistema {#minimum-system-requirements}

Sistemi operativi supportati

* Linux CentOS 6.3 a 64 bit

Requisiti hardware

* Processore Intel® Pentium® 4 a 3,2 GHz (consigliato dual Intel Xeon® o più veloce)

* Sistemi operativi a 64 bit: 4 GB di RAM (consigliati 8 GB)

* Disco rigido

(Disk-SAS): Almeno 10 GB con 7,5.000 rpm

(Disk-SSD): Velocità di lettura/scrittura di 400 MBps

(NAS): Collegamento dedicato da 1 GB

Requisiti software

* Oracle Java SE 1.8 o versione successiva

### Adobe Primetime Offline Packager 2.3.1 {#adobe-primetime-offline-packager-1}

1. Scaricare il software Java SE dal sito [](https://www.oracle.com/technetwork/java/javase/downloads/index.html) Oracle e seguire le istruzioni di installazione.
1. Estrarre il file di archivio di Adobe Primetime Offline Packager 2.3.1 denominato `PrimetimeOfflinePackager-2-3-1-b47-10142016.zip` nel disco.

### Configurazione di Offline Packager 2.3.1 {#configuring-the-offline-packager}

Le istruzioni di configurazione sono disponibili nella guida introduttiva di Primetime Offline Packager all&#39;indirizzo [https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)

## Novità di Primetime Offline Packager 2.1 (luglio 2015) {#what-s-new-in-primetime-offline-packager-july}

Supporto per PlayReady BuyDRM (per DASH). Per informazioni dettagliate, consultate la documentazione della Guida [disponibile qui](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html).

Sono stati apportati i seguenti miglioramenti anche al packager offline.

PTPUB-780 È stato aggiunto il supporto per il tag EXT-X-START

## Novità di Primetime Offline Packager 2.0 (giugno 2015) {#what-s-new-in-primetime-offline-packager-june}

È stato aggiunto il supporto dell&#39;output DASH. Per informazioni dettagliate, consulta la documentazione del prodotto [qui](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html) .

In questa versione sono stati corretti anche i seguenti problemi.

* PTPUB-783 Offline Packager è ora in grado di gestire file WebVTT vuoti.
* PTPUB- 781 Artefatti in uscita HLS su Chrome quando alcune risorse MP4 transcodificate vengono confezionate con packager offline per produrre output MBR.

## Adobe Primetime Offline Packager 2.1 {#adobe-primetime-offline-packager-2}

### Requisiti minimi di sistema {#minimum-system-requirements-1}

**Sistemi operativi supportati**

* Linux CentOS 6.3 a 64 bit

**Requisiti hardware**

* Processore Intel® Pentium® 4 a 3,2 GHz (consigliato dual Intel Xeon® o più veloce)

* Sistemi operativi a 64 bit: 4 GB di RAM (consigliati 8 GB)

* Scheda Ethernet da 1 Gb consigliata (sono supportate più schede di rete e 10 Gb)

* Disco rigido

   * (Disk-SAS): Almeno 10 GB con 7,5.000 rpm
   * (Disk-SSD): Velocità di lettura/scrittura di 400 MBps
   * (NAS): Collegamento dedicato da 1 GB

**Requisiti software**

* Oracle Java SE 1.8 o versione successiva

### Installazione di Offline Packager 2.1 {#installing-offline-packager}

1. Scaricare il software Java SE dal sito [](https://www.oracle.com/technetwork/java/javase/downloads/index.html) Oracle e seguire le istruzioni di installazione.
1. Estrarre il `Adobe Primetime - Offline Packager 2.1.0 archive file, PrimetimeOfflinePackager-2-1-0-b15-07082015.zip`, sul disco.

### Configurazione di Offline Packager 2.1 {#configuring-the-offline-packager-1}

Per i dettagli di configurazione disponibili qui [https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html, consultate la documentazione introduttiva di Primetime Offline Packager.](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)

## Risorse utili {#helpful-resources}

* Consulta la documentazione completa della guida nella pagina Informazioni e supporto [di](https://helpx.adobe.com/support/primetime.html) Adobe Primetime.