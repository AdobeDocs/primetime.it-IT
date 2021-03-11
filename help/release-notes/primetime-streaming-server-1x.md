---
title: Versioni di Primetime Streaming Server
description: Novità delle versioni Primetime Streaming Server 1.3 e 1.4.
products: SG_PRIMETIME
topic-tags: release-notes
translation-type: tm+mt
source-git-commit: b33240bf1b42b80389cd95a7ae4d3f85185a2d32
workflow-type: tm+mt
source-wordcount: '1916'
ht-degree: 0%

---


# Versioni di Primetime Streaming Server {#primetime-streaming-server-x-releases}

Novità delle versioni Primetime Streaming Server 1.3 e 1.4.

## Novità di Primetime Streaming Server 1.4 (versione di dicembre) {#what-s-new-in-primetime-streaming-server-december-release}

**Pacchetto offline**

* I flussi HLS in uscita ora contengono i metadati ID3 presenti in MPEG-2 TS
* I flussi di solo audio HLS possono ora avere un&#39;immagine statica associata
* Supporto per fornire IV come input utente per i flussi di lavoro di crittografia HLS AES
* Supporto dell&#39;output IV in un file quando IV viene generato dal packager offline
* Playlist Creator ora supporta l’associazione di gruppi audio multilingue e di gruppi di sottotitoli WebVTT multilingue ai flussi multimediali

**Server di origine**

* La crittografia HLS AES è disponibile per i flussi di lavoro Live e VOD. Primetime Origin può solo in tempo applicare la crittografia HLS AES ai flussi HLS in entrata o ai file MP4.
* Può anche applicare la crittografia JIT HLS AES quando viene utilizzato per convertire i flussi HDS in ingresso nei flussi HLS.
* Primetime Origin ora supporta l&#39;inserimento di file SWF nell&#39;elenco Consentiti per i flussi PHLS. In precedenza era supportato solo per i flussi PHDS

**Primetime Live Packager**

* Supporto per la generazione di flussi HLS AES-128 per flussi RTMP in ingresso e MPEG-2 TS

I certificati PHDS/PHLS sono stati aggiornati. La nuova data di scadenza per lo stesso sarà il 10/01/2016.

### **Correzioni di bug incluse nella versione 1.4** {#bug-fixes-included-in-release}

* PTPUB-282- Il manifesto a livello di set HLS creato da OfflinePackager 1.3.1 non dispone di informazioni sul codec e sulla risoluzione.
* PTPUB-353 - PlayListCreator non supporta l&#39;aggiunta di informazioni WebVTT nel manifesto del livello impostato
* PTPUB-583 - Lo strumento PlaylistCreator prepende in modo imprevisto gli URI del gruppo con.
* PTPUB-605 Playlist Creator non elencare SUBTITLE Group in ogni flusso di variante
* PTPUB-634 - Il Packager offline aggiunge SpliceInsert al manifesto.
* PTPUB-635- Sono stati inseriti più tag SpliceOut per il cue di un singolo annuncio.

### Problema noto nella versione 1.4 {#known-issue-in-release}

* PTPUB-645 DPISsimple Mode viene forzato anche quando viene specificata la modalità DPIScte35 quando sia i segnali della riga di comando che i segnali in-stream sono entrambi forniti nella configurazione del packager offline

## Novità di Primetime Streaming Server 1.3.1 (versione di maggio) {#what-s-new-in-primetime-streaming-server-may-release}

La versione 1.3.1 fa riferimento all’hotfix. I seguenti miglioramenti lo rendono un aggiornamento consigliato per i clienti in quanto consiste in miglioramenti delle prestazioni chiave per i casi d’uso di JIT MP4:

1. Correzione delle prestazioni per la generazione MP4 JIT m3u8 su Origin con DRM, inclusa la rotazione dei tasti
1. È stata aggiunta la configurazione &quot;CopyQueryParamToJITFragmentURI&quot; per copiare i parametri di query dalla richiesta di manifesto JIT agli URI di frammento generati per la conversione MP4 JIT. Fai riferimento alla documentazione del server di origine HTTP per un esempio di utilizzo
1. Consenti file MP4 senza estensione per la conversione JIT , tramite configurazione Config/MP4Only aggiunta a vod.xml

### Correzioni di bug incluse nella versione 1.3.1 {#bug-fixes-included-in-release-1}

* 3759167 - Non tutti i segnali SCTE35 lo rendono al manifesto di output a causa di anomalie di marca temporale durante il packaging. Applica pts_Adjustment sul messaggio SpliceTime nel TimeSignal di SpliceInfoSection nel messaggio SCTE35.

### Problemi noti nella versione 1.3.1 {#known-issues-in-release}

* 3717039 - Quando il packager è configurato per produrre segnali in modalità semplice DPI, dovrebbe davvero essere alla ricerca di tipi di segnale specifici, come l&#39;opportunità di inserimento o di posizionamento delle giunzioni, e convertire solo quelli in segnali in modalità semplice. Dovrebbe ignorare altri tipi di segnali, come l&#39;avvio del programma, l&#39;avvio della rete, ecc.

* 3718598 - Quando Origin Server è configurato per il servizio di contenuti protetti con l&#39;accesso HSM abilitato, il client LunaSA back-end effettua una comunicazione frequente con il modulo HSM

## Novità di Primetime Streaming Server 1.3 (versione APRILE) {#what-s-new-in-primetime-streaming-server-april-release}

Primetime 1.3 introduce diverse nuove funzioni per lo streaming dei contenuti, una migliore usabilità e sicurezza.

**Primetime Streaming Server come forma unificata di Live Packager e Origin Server**

Primetime Live Packager e Primetime Origin vengono messi insieme per funzionare come un singolo componente. Questo componente può essere utilizzato come Packager o come Origin o utilizzare le funzionalità combinate per creare pacchetti e ospitare un flusso live.

Questo fornisce un&#39;interfaccia file unificata a questi server, facilitandone l&#39;esecuzione su un singolo computer. Continua a fornire la flessibilità da configurare come Packager o Origin separato.

**Supporto MPEG-DASH beta**

Primetime Streaming Server supporta il packaging MPEG-DASH per flussi di lavoro live e VOD. Il componente Live packager converte i flussi RTMP o MPEG-2-TS di acquisizione in formato DASH. Il componente Origine accetta un flusso DASH.

Per i flussi di lavoro VOD, il componente Packager offline converte le risorse MP4 e TS in formato MPEG-DASH ISOBFF.

**Conversione dal vivo a VOD**

È ora disponibile un nuovo server di registrazione componente che supporta l&#39;acquisizione di un flusso live e l&#39;archiviazione per la riproduzione VOD. Supporta la creazione di Riproduzioni eventi complete e di clip/elementi di rilievo per parte dell&#39;evento. Può essere configurato per registrare flussi solo audio, rimuovere annunci o annunci nel contenuto live. Il server di registrazione funziona con Primetime Streaming Server e con origini di terze parti.

**Conversione da RTMP a HLS in Primetime Live Packager**

Il componente Primetime Live Packager supporta la creazione di flussi HLS dai flussi RTMP. Consente inoltre di aggiungere DRM di Primetime e Streaming protetto ai flussi HLS di uscita.

**Autenticazione per flussi RTMP in ingresso in Primetime Live packager**

Un usermgmt.jar ora viene fornito con Primetime Live Packager per configurare l&#39;accesso con credenziali affidabili durante l&#39;invio di un flusso RTMP a Primetime Live Packager

Ora gli encoder possono essere configurati per utilizzare un nome utente/password durante l&#39;invio dei flussi a Live Packager.

**Strumento PlaylistCreator per creare manifesti di primo livello per HDS e HLS**

È ora disponibile un&#39;utility eccellente PlaylistCreator.jar con Primetime Offline Packager per creare facilmente file manifest di primo livello per le risorse HDS e HLS.

**Funzionalità di sicurezza aggiuntive per incorporare un modulo di sicurezza hardware**

Primetime Offline Packager ora supporta l&#39;accesso al certificato credenziali Packager e alle chiavi comuni da un modulo di sicurezza hardware.

Un modulo di sicurezza hardware fornisce una protezione aggiuntiva per queste risorse riservate.

**Prestazioni migliorate per il pacchetto VOD**

Sono stati incorporati diversi miglioramenti delle prestazioni per migliorare il tempo di creazione dei pacchetti per le risorse mezzanine in Primetime Offline Packager

**Prestazioni migliorate per il pacchetto JIT MP4**

Sono stati incorporati diversi miglioramenti delle prestazioni alle funzionalità di packaging JIT di Primetime Origin per gestire le richieste degli utenti per una grande libreria di risorse VOD.

## Adobe Primetime Streaming Server 1.4 {#adobe-primetime-streaming-server}

### Requisiti minimi di sistema {#minimum-system-requirements}

**Requisiti di rete**

* La rete deve essere abilitata per l&#39;invio di flussi MPEG-TS da un codificatore a Live Packager. Live Packager accetta anche un flusso RTMP da un encoder che non richiede una rete multicast.

**Sistemi operativi supportati**

* Linux CentOS 6.3 a 64 bit

**Requisiti hardware**

* Processore Intel® Pentium® 4 a 3,2 GHz (consigliato doppio processore Intel Xeon® o più veloce)
* Sistemi operativi a 64 bit: 4 GB di RAM (8 GB consigliati)
* Scheda Ethernet da 1 Gb consigliata (sono supportate più schede di rete e 10 Gb)
* Disco:

   * (Disk-SAS): Almeno 10 GB con 7,5.000 rpm
   * (Disk-SSD) : Lettura/scrittura a 400 MBps
   * (NAS) : Collegamento dedicato da 1 GB

**Requisiti software**

* Oracle Java JRE 1.7 (Consiglia: Sun/Oracle Hotspot JVM). JDK è richiesto per l’accesso JConsole alle API JMX

### Installare e configurare Primetime Streaming Server {#install-and-configure-primetime-streaming-server}

**Installare il server di streaming**

1. Scarica il software Java SE e JDK dal [sito di Oracle](https://www.oracle.com/technetwork/java/javase/downloads/index.html) e segui le istruzioni di installazione.
2. Estrai il file di archivio Adobe Primetime-Streaming Server 1.4 `Primetime- StreamingServer-1-4-0-b206-12042014.zip` sul disco.

**Avviare Primetime Streaming Server**

Per avviare il server di streaming, eseguire il comando seguente dalla riga di comando nella directory principale del server di streaming:\
`$./pss_start.sh`

**Configurare Primetime Streaming Server come Live Packager o HTTP Origin Server**

Per configurare il server di streaming come Live Packager o Origin Server, aggiorna il file di configurazione pss.xml posizionato nella directory conf nella directory principale del server di streaming:

```
<Config> 
<!-- Set this false to disable the Origin Component. --> 
<OriginEnabled&gt;true&lt;/OriginEnabled>  
<!-- Set this false to disable the Packager Component. -->  
<PackagerEnabled&gt;true&lt;/PackagerEnabled>
</Config>
```

**Arrestare il server di streaming Primetime**

Per arrestare il server di streaming, eseguire il comando seguente nella directory principale del server di streaming:\
`$./pss_stop.sh`

**Riavvia il server di streaming Primetime**

Per riavviare il server di streaming, arrestare e avviare il server di streaming.

<!-- 

Comment Type: draft

**Configuring Primetime Streaming Server**

Refer the Primetime Streaming Server Getting Started document for the configuration details available at [https://help.adobe.com/en_US/primetime/platform/primetime_streaming_server.pdf](https://help.adobe.com/en_US/primetime/platform/primetime_streaming_server.pdf).

-->

**Disinstallazione del server di streaming Primetime**

Per disinstallare il server di streaming, arrestare il server di streaming e rimuovere la directory pss del server di streaming nella directory Primetime

## Utilizzo di Live Packager e Origin Server 1.4 {#working-with-live-packager-and-origin-server}

Questa sezione si applica quando Primetime Streaming Server non viene utilizzato e viene implementato invece Primetime Live packager AND/OR Primetime Origin Server

### Requisiti minimi di sistema {#minimum-system-requirements-1}

**Requisiti di rete**

* La rete deve essere abilitata per l&#39;invio di flussi MPEG-TS da un codificatore a Live Packager. Live Packager accetta anche un flusso RTMP da un encoder che non richiede una rete multicast.

**Sistemi operativi supportati**

* Linux CentOS 6.3 a 64 bit

**Requisiti hardware**

* Processore Intel® Pentium® 4 a 3,2 GHz (consigliato doppio processore Intel Xeon® o più veloce)
* Sistemi operativi a 64 bit: 4 GB di RAM (8 GB consigliati)
* Scheda Ethernet da 1 Gb consigliata (sono supportate più schede di rete e 10 Gb)
* Disco:

   * (Disk-SAS): Almeno 10 GB con 7,5.000 rpm
   * (Disk-SSD) : Lettura/scrittura a 400 MBps
   * (NAS) : Collegamento dedicato da 1 GB

**Requisiti software**

* Oracle Java JRE 1.7 (Consiglia: Sun/Oracle Hotspot JVM). JDK è richiesto per l’accesso JConsole alle API JMX

I requisiti minimi di sistema indicati sopra sono validi sia per Origin Server che per Live Packager.

### Installa e configura il Live Packager {#install-and-configure-the-live-packager}

**Installazione di Live Packager**

1. Scarica il software Java SE e JDK dal [sito di Oracle](https://www.oracle.com/technetwork/java/javase/downloads/index.html) e segui le istruzioni di installazione.
1. Estrai il file di archivio Adobe Primetime - Live Packager 1.4 `Primetime-LivePackager-1-4-0-b206-12042014.zip` sul tuo disco.

**Installazione del server di origine HTTP**

1. Scarica il software Java JRE e JDK dal [sito di Oracle](https://www.oracle.com/technetwork/java/javase/downloads/index.html) e segui le istruzioni di installazione.
1. Estrai il file di archivio Adobe Primetime - HTTP Origin Server 1.4 `Primetime-HttpOrigin-1-4-0-b206-12042014.zip` sul disco.

**Per avviare Live** PackagerPer avviare il packager, eseguire il seguente comando dalla directory principale del packager:\
`$packager_start.sh`

**Per avviare il server di origine HTTP**

Per avviare il server di origine HTTP, esegui il seguente comando dalla riga di comando nella directory principale del server di origine:\
`$./origin_start.sh`

**Interrompi Live Packager**

Per arrestare il packager, eseguire il seguente comando dalla directory principale del packager:\
`$packager_stop.sh`

**Arresta il server di origine HTTP**

Per arrestare il server di origine HTTP, esegui il seguente comando nella directory principale del server di origine:\
`$./origin_stop.sh`

**Riavvia il Live Packager**

Per riavviare il packager, arrestare e avviare il packager.

**Nota**: All&#39;avvio del packager, tenta di inizializzare le informazioni di avvio dal target del frammento nella directory temporanea. Se le informazioni di avvio si trovano nella destinazione del frammento, significa che il packager è stato riavviato. In caso di riavvio, il imballatore attende fino al limite del frammento successivo e quindi avvia il packaging. Il packager inserisce una voce gap nel bootstrap per indicare che mancano frammenti.

**Riavvia il server di origine HTTP**

Per riavviare il server di origine HTTP, arrestare e avviare il server di origine HTTP.

**Configurazione di Live Packager**

Il file di distribuzione contiene una configurazione di esempio che può essere utilizzata per testare il packager.

Dopo aver estratto l&#39;archivio Adobe Primetime - Live Packager 1.4, cambia le directory nella directory del packager ed esegui lo script packager_start.sh. La configurazione di esempio ascolta l&#39;indirizzo multicast 239.235.0.3:14000 ed esegue il server di origine locale sulla porta 8080. L&#39;output è configurato per essere scritto in `packager/webroot/_default_/_default_/ directory`.

<!-- 

Comment Type: draft

For more details about the configuration refer [the Primetime Live Packager document](https://help.adobe.com/en_US/primetime/api/packagers/index.html).

-->

**Configurazione del server di origine HTTP**

Consulta la Guida introduttiva di Primetime HTTP Origin Server per i dettagli di configurazione disponibili qui.

**Disinstallazione di Live Packager**

Per disinstallare il packager, arrestare il packager e rimuovere la directory packager dalla directory Primetime.

**Disinstallazione del server di origine HTTP**

Per disinstallare il server di origine HTTP, arresta il server di origine HTTP e rimuovi la directory httporigin del server di origine HTTP nella directory Primetime .

## Pacchetto offline Adobe Primetime 1.4 {#adobe-primetime-offline-packager}

### Requisiti minimi di sistema {#minimum-system-requirements-2}

**Sistemi operativi supportati**

* Linux CentOS 6.3 a 64 bit

**Requisiti hardware**

* Processore Intel® Pentium® 4 a 3,2 GHz (consigliato doppio processore Intel Xeon® o più veloce)
* Sistemi operativi a 64 bit: 4 GB di RAM (8 GB consigliati)
* Scheda Ethernet da 1 Gb consigliata (sono supportate più schede di rete e 10 Gb)
* Disco:

   * (Disk-SAS): Almeno 10 GB con 7,5.000 rpm
   * (Disk-SSD) : Lettura/scrittura a 400 MBps
   * (NAS) : Collegamento dedicato da 1 GB

**Requisiti software**

* Oracle Java JRE 1.7 o successivo.

### Installa e configura il pacchetto offline {#install-and-configure-offline-packager}

Per installare il pacchetto offline, segui questi passaggi:

1. Scarica il software Java SE dal [sito di Oracle](https://www.oracle.com/technetwork/java/javase/downloads/index.html) e segui le istruzioni di installazione.
1. Estrai il file di archivio Adobe Primetime - Offline Packager 1.4, `Primetime- OfflinePackager-1-4-0-b206-12042014.zip`, sul tuo disco.

Consulta il documento Primetime Offline Packager Getting Started per i dettagli di configurazione disponibili [qui](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html).

## Risorse utili {#helpful-resources}

* Consulta la documentazione completa della guida nella pagina [Informazioni e supporto per Adobe Primetime](https://helpx.adobe.com/support/primetime.html) .