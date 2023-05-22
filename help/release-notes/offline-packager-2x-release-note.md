---
title: Versioni di Primetime Offline Packager 2.x
description: Novità delle versioni 2.1 e 2.3.1 di Primetime Offline Packager
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
exl-id: 911549b4-45b3-400a-b903-fa1479ee862b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---

# Versioni di Primetime Offline Packager {#primetime-offline-packager-x-releases}

Novità delle versioni 2.1 e 2.3.1 di Primetime Offline Packager

## Novità di Primetime Offline Packager 2.3.1 (ottobre 2016)  {#what-s-new-in-primetime-offline-packager-oct}

Il rilascio abilita il profilo on-demand per MPEG-DASH, aggiunge il supporto per `validate` opzione per lo strumento PlaylistCreator e presenta alcune correzioni di tasti per gli scenari Multi-DRM elencati di seguito.

| **Numero problema** | **Descrizione** |
|---|---|
| PTPUB-985 | HLS AAXS e Sample-AES non funzionano per la chiave generata dal packager |
| PTPUB-973 | È stato corretto un errore nell’algoritmo di crittografia per alcuni contenuti specifici di Widevine |
| PTPUB-964 | Crittografia CENC interrotta per alcuni tipi di contenuti multimediali su determinati lettori - Android TVSDK. |
| PTPUB-954 | La crittografia AES di esempio ignora AAXS DRM per impostazione predefinita / Errore generato con la consegna della chiave remota abilitata. |
| PTPUB-951 | Offline packager non genera eccezioni quando key_file_path non è specificato con Widevine. Viene invece generata l&#39;NPE. |

La documentazione più recente dei pacchetti Primetime è disponibile all’indirizzo [https://help.adobe.com/en_US/primetime/api/packagers/index.html](https://help.adobe.com/en_US/primetime/api/packagers/index.html).

### Problema noto nella versione 2.3.1 {#known-issue-in-version}

In questa versione sono presenti i seguenti problemi.

| **Numero problema** | **Descrizione** |
|---|---|
| PTPUB-1005 | PlaylistCreator non fornisce l&#39;URL corretto per il file .pssh nel file .mpd finale a livello di set generato per il DRM AAXS. |
| PTPUB-1001 | PlaylistCreator deve generare un errore quando viene fornito un percorso vuoto tramite il parametro in_path |
| PTPUB-990 | Per DASH, Offline Packager non scrive su disco il file IV generato da Packager quando i parametri `log_vi` E `iv_out_path` sono specificati. |
| PTPUB-980 | Quando il file di configurazione viene utilizzato per la creazione di pacchetti, utilizzando il parametro `key_url` non rimuove le virgolette dagli input forniti. |

## Adobe Primetime Offline Packager 2.3.1 {#adobe-primetime-offline-packager}

### Requisiti minimi di sistema {#minimum-system-requirements}

Sistemi operativi supportati

* Linux CentOS 6.3 a 64 bit

Requisiti hardware

* Processore Intel® Pentium® 4 da 3,2 GHz (Intel Xeon® doppio o più veloce consigliato)

* Sistemi operativi a 64 bit: 4 GB di RAM (8 GB consigliati)

* Disco rigido

(Disk-SAS): minimo 10 GB con 7.500 rpm

(Disk-SSD): velocità di lettura/scrittura di 400 MB/s

(NAS): collegamento dedicato da 1 GB

Requisiti software

* Oracle Java SE 1.8 o versione successiva

### Adobe Primetime Offline Packager 2.3.1 {#adobe-primetime-offline-packager-1}

1. Scaricare il software Java SE da [Oracle del sito](https://www.oracle.com/technetwork/java/javase/downloads/index.html) e seguire le istruzioni di installazione.
1. Estrai il file di archivio Adobe Primetime Offline Packager 2.3.1 denominato `PrimetimeOfflinePackager-2-3-1-b47-10142016.zip` sul disco.

### Configurazione di Offline Packager 2.3.1 {#configuring-the-offline-packager}

Le istruzioni di configurazione sono disponibili nella guida introduttiva di Primetime Offline Packager all&#39;indirizzo [https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)

## Novità di Primetime Offline Packager 2.1 (luglio 2015) {#what-s-new-in-primetime-offline-packager-july}

Supporto per PlayReady BuyDRM (per DASH). Per informazioni dettagliate, consulta la documentazione di supporto [disponibile qui](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html).

Il seguente miglioramento è stato apportato anche al packager offline.

PTPUB-780 Aggiunta del supporto per il tag EXT-X-START

## Novità di Primetime Offline Packager 2.0 (giugno 2015) {#what-s-new-in-primetime-offline-packager-june}

È stato aggiunto il supporto per l’output Clear DASH. Consulta la documentazione del prodotto [qui](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html) per i dettagli.

In questa versione sono stati risolti anche i seguenti problemi.

* PTPUB-783 Offline Packager è ora in grado di gestire file WebVTT vuoti.
* PTPUB- 781 Artefatti in output HLS su Chrome quando alcune risorse MP4 trascodificate vengono confezionate con offline packager per produrre output MBR.

## Adobe Primetime Offline Packager 2.1 {#adobe-primetime-offline-packager-2}

### Requisiti minimi di sistema {#minimum-system-requirements-1}

**Sistemi operativi supportati**

* Linux CentOS 6.3 a 64 bit

**Requisiti hardware**

* Processore Intel® Pentium® 4 da 3,2 GHz (Intel Xeon® doppio o più veloce consigliato)

* Sistemi operativi a 64 bit: 4 GB di RAM (8 GB consigliati)

* Scheda Ethernet da 1 Gb consigliata (supporto di più schede di rete e supporto di 10 Gb)

* Disco rigido

   * (Disk-SAS): minimo 10 GB con 7.500 rpm
   * (Disk-SSD): velocità di lettura/scrittura di 400 MB/s
   * (NAS): collegamento dedicato da 1 GB

**Requisiti software**

* Oracle Java SE 1.8 o versione successiva

### Installazione di Offline Packager 2.1 {#installing-offline-packager}

1. Scaricare il software Java SE da [Oracle del sito](https://www.oracle.com/technetwork/java/javase/downloads/index.html) e seguire le istruzioni di installazione.
1. Estrai `Adobe Primetime - Offline Packager 2.1.0 archive file, PrimetimeOfflinePackager-2-1-0-b15-07082015.zip`, sul disco.

### Configurazione di Offline Packager 2.1 {#configuring-the-offline-packager-1}

Consulta il documento Primetime Offline Packager Getting Started per i dettagli di configurazione disponibili qui [https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)

## Risorse utili {#helpful-resources}

* Consulta la documentazione completa dell’Aiuto all’indirizzo [Informazioni e supporto per Adobe Primetime](https://helpx.adobe.com/support/primetime.html) pagina.
