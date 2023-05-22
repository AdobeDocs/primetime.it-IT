---
title: Versioni di Primetime Streaming Server
description: Novità di Primetime Streaming Server 1.3 e 1.4.
products: SG_PRIMETIME
topic-tags: release-notes
exl-id: 80c4687e-b0ac-48f2-a1c3-8751552da9d1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1916'
ht-degree: 0%

---

# Versioni di Primetime Streaming Server {#primetime-streaming-server-x-releases}

Novità di Primetime Streaming Server 1.3 e 1.4.

## Novità di Primetime Streaming Server 1.4 (versione di dicembre) {#what-s-new-in-primetime-streaming-server-december-release}

**Offline Packager**

* I flussi HLS di output ora contengono metadati ID3 presenti in MPEG-2 TS
* Ora ai flussi solo audio HLS può essere associata un’immagine statica
* Supporto per la fornitura di input IV come utente per i flussi di lavoro di crittografia AES HLS
* Supporto per l&#39;output IV in un file quando IV viene generato da Offline Packager
* Playlist Creator ora supporta l’associazione di gruppi audio multilingue e di sottotitoli WebVTT multilingue ai flussi multimediali

**Server di origine**

* La crittografia HLS AES è disponibile per i flussi di lavoro Live e VOD. Primetime Origin può applicare la crittografia AES HLS ai flussi HLS in ingresso o ai file MP4.
* Può anche applicare la crittografia JIT HLS AES quando viene utilizzata per convertire i flussi HDS in ingresso in flussi HLS.
* Primetime Origin ora supporta l’inserimento di SWF nell’elenco Consentiti per i flussi PHLS. In precedenza era supportato solo per i flussi PHDS

**Primetime Live Packager**

* Supporto per la generazione di flussi HLS AES-128 per flussi RTMP e TS MPEG-2

I certificati PHDS/PHLS sono stati aggiornati. La nuova data di scadenza per lo stesso sarà il 10/01/2016.

### **Correzioni di bug incluse nella versione 1.4** {#bug-fixes-included-in-release}

* PTPUB-282- Il manifesto a livello di set HLS creato da OfflinePackager 1.3.1 non dispone di informazioni di codec e risoluzione.
* PTPUB-353 - PlayListCreator non supporta l&#39;aggiunta di informazioni WebVTT nel manifesto a livello di set
* PTPUB-583 - Lo strumento PlaylistCreator precede in modo imprevisto l’URI del gruppo con.
* PTPUB-605 Il creatore di playlist non elenca il gruppo SUBTITLE in ogni flusso di variante
* PTPUB-634 - Offline Packager aggiunge SpliceInsert al manifesto.
* PTPUB-635- Sono stati inseriti più tag SpliceOut per un singolo segnale pubblicitario.

### Problema noto nella versione 1.4 {#known-issue-in-release}

* PTPUB- 645 DPISimple Mode viene forzata anche quando viene specificata la modalità DPIScte35 quando sia i cue della riga di comando che i cue in-stream vengono forniti in configurazione offline packager

## Novità di Primetime Streaming Server 1.3.1 (versione di MAGGIO) {#what-s-new-in-primetime-streaming-server-may-release}

La versione 1.3.1 fa riferimento all’hotfix. I seguenti miglioramenti lo rendono un aggiornamento consigliato per i clienti in quanto consiste in miglioramenti delle prestazioni chiave per i casi d’uso JIT MP4:

1. Correzione delle prestazioni per la generazione di MP4 JIT m3u8 in Origin con DRM, inclusa la rotazione delle chiavi
1. È stata aggiunta la configurazione &quot;CopyQueryParamToJITFragmentURIs&quot; per copiare i parametri di query dalla richiesta manifest JIT agli URI del frammento generato per la conversione JIT MP4. Per informazioni sull’utilizzo di esempio, consulta la documentazione di HTTP Origin Server.
1. Consenti file MP4 senza estensione per la conversione JIT tramite la configurazione Config/MP4Only aggiunta a vod.xml

### Correzioni di bug incluse nella versione 1.3.1 {#bug-fixes-included-in-release-1}

* 3759167 - Non tutti i segnali SCTE35 vengono inseriti nel manifesto di output a causa di un&#39;anomalia di marca temporale durante la creazione del pacchetto. Applicare pts_adjustment su SpliceTime nel TimeSignal di SpliceInfoSection nel messaggio SCTE35.

### Problemi noti nella versione 1.3.1 {#known-issues-in-release}

* 3717039 - Quando il packager è configurato per produrre segnali in modalità semplice DPI, dovrebbe essere alla ricerca di tipi di segnale specifici, come l&#39;inserimento di giunti o l&#39;opportunità di posizionamento, e convertendo solo questi in segnali in modalità semplice. Dovrebbe ignorare altri tipi di segnali, come l’avvio del programma, l’avvio della rete, ecc.

* 3718598: quando Origin Server è configurato per fornire contenuti protetti con accesso HSM abilitato, il client LunaSA backend comunica frequentemente con il modulo HSM

## Novità di Primetime Streaming Server 1.3 (versione di APRILE) {#what-s-new-in-primetime-streaming-server-april-release}

La versione 1.3 di Primetime include diverse nuove funzioni relative ai contenuti in streaming, migliorando l’usabilità e la sicurezza.

**Server di streaming di Primetime come forma unificata di Live Packager e server di origine**

Primetime Live Packager e Primetime Origin vengono riuniti per funzionare come un singolo componente. Questo componente può essere utilizzato come Packager o come origine oppure utilizzare le funzionalità combinate per creare un pacchetto e ospitare un Live Stream.

Questo fornisce un&#39;interfaccia di file unificata a questi server, facilitandone l&#39;esecuzione su un singolo computer. Continua a fornire la flessibilità di essere configurato come Packager o Origine separata.

**Supporto per Beta MPEG-DASH**

Primetime Streaming Server supporta la creazione di pacchetti MPEG-DASH per i flussi di lavoro Live e VOD. Il componente Live Packager converte i flussi RTMP o MPEG-2-TS in formato DASH. Il componente Origine accetta un flusso DASH.

Per i flussi di lavoro VOD, il componente Offline Packager converte le risorse MP4 e TS in formato ISOBFF MPEG-DASH.

**Conversione da Live a VOD**

È ora disponibile un nuovo componente Recording Server che supporta l’acquisizione di un Live Stream e l’archiviazione per la riproduzione VOD. Supporta la creazione di Riproduzioni di eventi complete e di clip/punti salienti per parte dell’evento. Può essere configurato per registrare flussi di sola audio, rimuovere annunci o slate nei contenuti live. Recording Server funziona sia con Primetime Streaming Server che con Origins di terze parti.

**Conversione da RTMP a HLS in Primetime Live Packager**

Il componente Primetime Live Packager supporta la creazione di flussi HLS da flussi RTMP. Consente inoltre di aggiungere DRM Primetime e Flusso protetto ai flussi HLS in uscita.

**Autenticazione per flussi RTMP in arrivo su Primetime Live Packager**

Ora usermgmt.jar viene fornito con Primetime Live Packager per configurare l’accesso con credenziali attendibili quando si invia un flusso RTMP a Primetime Live Packager.

Ora è possibile configurare gli encoder in modo che utilizzino un nome utente o una password durante l’invio dei flussi a Live Packager.

**Strumento PlaylistCreator per creare manifesti di primo livello per HDS e HLS**

Con Primetime Offline Packager è ora disponibile un&#39;utility innovativa PlaylistCreator.jar per creare facilmente file manifest di primo livello per risorse HDS e HLS.

**Funzionalità di sicurezza aggiuntive per incorporare un modulo di sicurezza hardware**

Primetime Offline Packager ora supporta l&#39;accesso al certificato di credenziali Packager e alle chiavi comuni da un modulo di sicurezza hardware.

Un modulo di sicurezza hardware fornisce ulteriore protezione a queste risorse riservate.

**Prestazioni migliorate per il packaging VOD**

Sono stati incorporati diversi miglioramenti delle prestazioni per migliorare i tempi di packaging delle risorse mezzanine in Primetime Offline Packager

**Prestazioni migliorate per il packaging JIT MP4**

Diversi miglioramenti delle prestazioni sono stati incorporati nelle funzionalità di creazione pacchetti JIT di Primetime Origin per gestire le richieste degli utenti per una vasta libreria di risorse VOD.

## Adobe Primetime Streaming Server 1.4 {#adobe-primetime-streaming-server}

### Requisiti minimi di sistema {#minimum-system-requirements}

**Requisiti di rete**

* Per inviare lo streaming MPEG-TS da un codificatore a Live Packager, è necessario abilitare la rete multicast. Live Packager accetta inoltre un flusso RTMP da un codificatore che non richiede una rete multicast.

**Sistemi operativi supportati**

* Linux CentOS 6.3 a 64 bit

**Requisiti hardware**

* Processore Intel® Pentium® 4 da 3,2 GHz (Intel Xeon® doppio o più veloce consigliato)
* Sistemi operativi a 64 bit: 4 GB di RAM (8 GB consigliati)
* Scheda Ethernet da 1 Gb consigliata (supporto di più schede di rete e supporto di 10 Gb)
* Disco:

   * (Disk-SAS): almeno 10 GB con 7.500 rpm
   * (Disk-SSD): 400 MBps in lettura/scrittura
   * (NAS) : collegamento dedicato da 1 GB

**Requisiti software**

* Oracle Java JRE 1.7 (consigliato: Sun/Oracle Hotspot JVM). JDK è necessario per l’accesso JConsole alle API JMX

### Installare e configurare Primetime Streaming Server {#install-and-configure-primetime-streaming-server}

**Installare il server di streaming**

1. Scarica Java SE e il software JDK da [Oracle del sito](https://www.oracle.com/technetwork/java/javase/downloads/index.html) e seguire le istruzioni di installazione.
2. Estrarre il file di archivio di Adobe Primetime-Streaming Server 1.4, `Primetime- StreamingServer-1-4-0-b206-12042014.zip` sul disco.

**Avviare il server di streaming Primetime**

Per avviare Streaming Server, eseguire il comando seguente dalla riga di comando nella directory principale di Streaming Server:\
`$./pss_start.sh`

**Configurare il server di streaming Primetime come Live Packager o HTTP Origin Server**

Per configurare il server di streaming come Live Packager o Server di origine, aggiornare il file di configurazione pss.xml posizionato nella directory conf nella directory principale del server di streaming:

```
<Config> 
<!-- Set this false to disable the Origin Component. --> 
<OriginEnabled&gt;true&lt;/OriginEnabled>  
<!-- Set this false to disable the Packager Component. -->  
<PackagerEnabled&gt;true&lt;/PackagerEnabled>
</Config>
```

**Arresta il server di streaming Primetime**

Per arrestare Streaming Server, eseguire il comando seguente nella directory principale di Streaming Server:\
`$./pss_stop.sh`

**Riavviare il server di streaming Primetime**

Per riavviare Streaming Server, arrestare e avviare Streaming Server.

<!-- 

Comment Type: draft

**Configuring Primetime Streaming Server**

Refer the Primetime Streaming Server Getting Started document for the configuration details available at [https://help.adobe.com/en_US/primetime/platform/primetime_streaming_server.pdf](https://help.adobe.com/en_US/primetime/platform/primetime_streaming_server.pdf).

-->

**Disinstallazione di Primetime Streaming Server**

Per disinstallare Streaming Server, arrestare Streaming Server e rimuovere la directory pss di Streaming Server nella directory Primetime

## Utilizzo di Live Packager e Origin Server 1.4 {#working-with-live-packager-and-origin-server}

Questa sezione si applica quando Primetime Streaming Server non viene utilizzato e invece viene distribuito Primetime Live Packager AND/OR Primetime Origin Server

### Requisiti minimi di sistema {#minimum-system-requirements-1}

**Requisiti di rete**

* Per inviare lo streaming MPEG-TS da un codificatore a Live Packager, è necessario abilitare la rete multicast. Live Packager accetta inoltre un flusso RTMP da un codificatore che non richiede una rete multicast.

**Sistemi operativi supportati**

* Linux CentOS 6.3 a 64 bit

**Requisiti hardware**

* Processore Intel® Pentium® 4 da 3,2 GHz (Intel Xeon® doppio o più veloce consigliato)
* Sistemi operativi a 64 bit: 4 GB di RAM (8 GB consigliati)
* Scheda Ethernet da 1 Gb consigliata (supporto di più schede di rete e supporto di 10 Gb)
* Disco:

   * (Disk-SAS): almeno 10 GB con 7.500 rpm
   * (Disk-SSD): 400 MBps in lettura/scrittura
   * (NAS) : collegamento dedicato da 1 GB

**Requisiti software**

* Oracle Java JRE 1.7 (consigliato: Sun/Oracle Hotspot JVM). JDK è necessario per l’accesso JConsole alle API JMX

I requisiti di sistema minimi di cui sopra valgono sia per Origin Server che per Live Packager.

### Installare e configurare Live Packager {#install-and-configure-the-live-packager}

**Installazione di Live Packager**

1. Scarica Java SE e il software JDK da [Oracle del sito](https://www.oracle.com/technetwork/java/javase/downloads/index.html) e seguire le istruzioni di installazione.
1. Estrai il file di archivio Adobe Primetime - Live Packager 1.4 `Primetime-LivePackager-1-4-0-b206-12042014.zip` sul disco.

**Installazione del server di origine HTTP**

1. Scarica il software Java JRE e JDK da [Oracle del sito](https://www.oracle.com/technetwork/java/javase/downloads/index.html) e seguire le istruzioni di installazione.
1. Estrarre il file di archivio Adobe Primetime - HTTP Origin Server 1.4 `Primetime-HttpOrigin-1-4-0-b206-12042014.zip`, sul disco.

**Per avviare Live Packager** Per avviare il packager, eseguire il comando seguente dalla directory radice del packager:\
`$packager_start.sh`

**Per avviare il server di origine HTTP**

Per avviare il server di origine HTTP, eseguire il comando seguente dalla riga di comando nella directory radice del server di origine:\
`$./origin_start.sh`

**Interrompi Live Packager**

Per arrestare il packager, eseguire il comando seguente dalla directory radice del packager:\
`$packager_stop.sh`

**Arresta il server di origine HTTP**

Per arrestare il server di origine HTTP, eseguire il comando seguente nella directory principale del server di origine:\
`$./origin_stop.sh`

**Riavvia Live Packager**

Per riavviare il programma di creazione pacchetti, arrestare e avviare il programma di creazione pacchetti.

**Nota**: all’avvio del programma di creazione pacchetti, tenta di inizializzare le informazioni di bootstrap dalla destinazione del frammento nella directory temporanea. Se le informazioni di bootstrap vengono trovate nella destinazione del frammento, significa che il packager è stato riavviato. In caso di riavvio, l’imballatore attende il limite del frammento successivo e quindi avvia l’imballaggio. Per indicare la presenza di frammenti mancanti, il programma di creazione pacchetti inserisce una voce gap nel bootstrap.

**Riavvia il server di origine HTTP**

Per riavviare il server di origine HTTP, arrestare e avviare il server di origine HTTP.

**Configurazione di Live Packager**

Il file di distribuzione contiene una configurazione di esempio che può essere utilizzata per testare il packager.

Dopo aver estratto l’archivio Adobe Primetime - Live Packager 1.4, modifica le directory nella directory packager ed esegui lo script packager_start.sh. La configurazione di esempio ascolta l&#39;indirizzo multicast 239.235.0.3:14000 ed esegue il server di origine locale sulla porta 8080. L&#39;output è configurato per essere scritto nel `packager/webroot/_default_/_default_/ directory`.

<!-- 

Comment Type: draft

For more details about the configuration refer [the Primetime Live Packager document](https://help.adobe.com/en_US/primetime/api/packagers/index.html).

-->

**Configurazione del server di origine HTTP**

Per i dettagli di configurazione disponibili qui, consulta il documento Primetime HTTP Origin Server Getting Started.

**Disinstallazione di Live Packager**

Per disinstallare il packager, arrestare il packager e rimuovere la directory packager dalla directory Primetime.

**Disinstallazione del server di origine HTTP**

Per disinstallare il server HTTP Origin, arrestare il server HTTP Origin e rimuovere la directory httporigin del server HTTP Origin nella directory Primetime.

## Adobe Primetime Offline Packager 1.4 {#adobe-primetime-offline-packager}

### Requisiti minimi di sistema {#minimum-system-requirements-2}

**Sistemi operativi supportati**

* Linux CentOS 6.3 a 64 bit

**Requisiti hardware**

* Processore Intel® Pentium® 4 da 3,2 GHz (Intel Xeon® doppio o più veloce consigliato)
* Sistemi operativi a 64 bit: 4 GB di RAM (8 GB consigliati)
* Scheda Ethernet da 1 Gb consigliata (supporto di più schede di rete e supporto di 10 Gb)
* Disco:

   * (Disk-SAS): almeno 10 GB con 7.500 rpm
   * (Disk-SSD): 400 MBps in lettura/scrittura
   * (NAS) : collegamento dedicato da 1 GB

**Requisiti software**

* Oracle Java JRE 1.7 o versione successiva.

### Installare e configurare Offline Packager {#install-and-configure-offline-packager}

Per installare Offline Packager, effettuare le seguenti operazioni:

1. Scaricare il software Java SE da [Oracle del sito](https://www.oracle.com/technetwork/java/javase/downloads/index.html) e seguire le istruzioni di installazione.
1. Estrarre il file di archivio Adobe Primetime - Offline Packager 1.4. `Primetime- OfflinePackager-1-4-0-b206-12042014.zip`, sul disco.

Per informazioni dettagliate sulla configurazione disponibile, consulta il documento Primetime Offline Packager Getting Started. [qui](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html).

## Risorse utili {#helpful-resources}

* Consulta la documentazione completa dell’Aiuto all’indirizzo [Informazioni e supporto per Adobe Primetime](https://helpx.adobe.com/support/primetime.html) pagina.
