---
title: Versioni di Primetime Streaming Server
seo-title: Versioni Primetime Streaming Server 1.x
description: Novità delle release Primetime Streaming Server 1.3 e 1.4.
seo-description: Novità delle release Primetime Streaming Server 1.3 e 1.4.
uuid: be05db6b-713f-4406-940d-9f3a805f967b
products: SG_PRIMETIME
topic-tags: release-notes
discoiquuid: baec714e-9d41-4e8b-b134-13a736885cbd
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '1929'
ht-degree: 0%

---


# Rilasci di Primetime Streaming Server {#primetime-streaming-server-x-releases}

Novità delle release Primetime Streaming Server 1.3 e 1.4.

## Novità in Primetime Streaming Server 1.4 (release di dicembre) {#what-s-new-in-primetime-streaming-server-december-release}

**Offline Packager**

* I flussi HLS di output ora contengono i metadati ID3 presenti in MPEG-2 TS
* I flussi solo audio HLS possono ora avere un&#39;immagine statica associata
* Supporto per fornire IV come input dell&#39;utente per i flussi di lavoro di crittografia HLS AES
* Supporto per l&#39;output IV su un file quando IV viene generato dal packager offline
* Playlist Creator ora supporta l&#39;associazione di gruppi audio multilingue e di sottotitoli WebVTT per più lingue ai flussi multimediali

**Server di origine**

* La crittografia HLS AES è disponibile per i flussi di lavoro Live e VOD. Origin Primetime può solo in Time applicare la crittografia HLS AES ai flussi HLS in arrivo o ai file MP4.
* Può anche applicare la cifratura JIT HLS AES quando viene utilizzata per convertire i flussi HDS in arrivo nei flussi HLS.
* Primetime Origin ora supporta il formato SWF che consente l&#39;elencazione dei flussi PHLS. Precedentemente era supportato solo per i flussi PHDS

**Primetime Live Packager**

* Supporto per la generazione di flussi HLS AES-128 per flussi RTMP in ingresso e MPEG-2 TS

I certificati PHDS/PHLS sono stati aggiornati. La nuova data di scadenza per lo stesso sarà 10/01/2016.

### **Correzioni di bug incluse nella release 1.4** {#bug-fixes-included-in-release}

* PTPUB-282 - Il manifesto a livello di set HLS creato da OfflinePackager 1.3.1 non dispone di informazioni sul codec e sulla risoluzione.
* PTPUB-353 - PlayListCreator non supporta l&#39;aggiunta di informazioni WebVTT nel manifesto del livello impostato
* PTPUB-583 - Lo strumento PlaylistCreator antepone in modo imprevisto gli URI del gruppo con.
* PTPUB-605 Playlist Creator che non elenca SUBTITLE Group in ogni flusso di variante
* PTPUB-634 - Offline Packager aggiunge SpliceInsert al manifesto.
* PTPUB-635 - Tag SpliceOut multipli inseriti per un singolo segnale pubblicitario.

### Problema noto nella release 1.4 {#known-issue-in-release}

* La modalità PTPUB-645 DPISsimple viene forzata anche quando la modalità DPIScte35 viene specificata quando sia i segnali della riga di comando che i segnali in streaming sono entrambi forniti nella configurazione offline packager

## Novità di Primetime Streaming Server 1.3.1 (release di maggio) {#what-s-new-in-primetime-streaming-server-may-release}

La versione 1.3.1 fa riferimento all’hotfix. I seguenti miglioramenti lo rendono un aggiornamento consigliato per i clienti in quanto consiste in miglioramenti delle prestazioni chiave per i casi di utilizzo JIT MP4:

1. Correzione delle prestazioni per la generazione MP4 JIT m3u8 in origine con DRM, inclusa la rotazione delle chiavi
1. Aggiunta una configurazione &quot;CopyQueryParamToJITFragmentURI&quot; per copiare i parametri di query dalla richiesta di manifesto JIT agli URI di frammento generati per la conversione MP4 JIT. Fate riferimento alla documentazione del server di origine HTTP per un esempio di utilizzo
1. Consenti file MP4 senza estensione per conversione JIT, tramite configurazione Config/MP4Only aggiunta a vod.xml

### Correzioni di bug incluse nella release 1.3.1 {#bug-fixes-included-in-release-1}

* 3759167 - Non tutti i segnali SCTE35 lo rendono visibile nel manifesto di output a causa di un&#39;anomalia nella marca temporale durante la creazione del pacchetto. Nel messaggio SCTE35, applicate pts_Adjustment su SpliceTime nel messaggio TimeSignal di SpliceInfoSection.

### Problemi noti nella release 1.3.1 {#known-issues-in-release}

* 3717039 - Quando il packager è configurato per produrre segnali in modalità semplice DPI, dovrebbe davvero cercare tipi di segnale specifici, come l&#39;inserzione di giunzione o l&#39;opportunità di posizionamento, e convertire solo quelli in segnali in modalità semplice. Deve ignorare altri tipi di segnali come l&#39;avvio del programma, l&#39;avvio della rete, ecc.

* 3718598 - Quando Origin Server è configurato per la trasmissione di contenuti protetti con accesso HSM abilitato, il client LunaSA back-end effettua una comunicazione frequente con il modulo HSM

## Novità di Primetime Streaming Server 1.3 (release APRIL) {#what-s-new-in-primetime-streaming-server-april-release}

Primetime 1.3 offre diverse nuove funzioni per lo streaming dei contenuti, una migliore usabilità e sicurezza.

**Primetime Streaming Server come modulo unificato di Live Packager e Origin Server**

Primetime Live Packager e Primetime Origin vengono messi insieme per funzionare come un singolo componente. Questo componente può essere utilizzato come Packager o come Origine oppure utilizzare le funzionalità combinate per creare pacchetti e ospitare un Live Stream.

Questo fornisce un&#39;interfaccia di file unificata a questi server, facilitandone l&#39;esecuzione su un solo computer. Continua a fornire la flessibilità da configurare come Packager o Origin separato.

**Supporto per MPEG-DASH Beta**

Primetime Streaming Server supporta la creazione di pacchetti MPEG-DASH per flussi di lavoro live e VOD. Il componente Live Packager converte i flussi RTMP o MPEG-2-TS in formato DASH. Il componente Origin accetta un flusso DASH.

Per i flussi di lavoro VOD, il componente Offline Packager converte le risorse MP4 e TS in formato MPEG-DASH ISOBFF.

**Conversione dal vivo al VOD**

È ora disponibile un nuovo server di registrazione che supporta l&#39;acquisizione di un flusso live e l&#39;archiviazione per la riproduzione VOD. Supporta la creazione di riproduzioni di eventi complete e di clip/evidenziazioni per parte dell&#39;evento. Può essere configurato per registrare flussi di solo audio, rimuovere annunci pubblicitari o Slates nel contenuto live. Il server di registrazione funziona sia con Primetime Streaming Server che con origini di terze parti.

**Conversione da RTMP a HLS in Primetime Live Packager**

Il componente Primetime Live Packager supporta la creazione di flussi HLS dai flussi RTMP. Consente inoltre di aggiungere DRM Primetime e Streaming protetto ai flussi HLS di output.

**Autenticazione per flussi RTMP in entrata in Primetime Live Packager**

Un usermgmt.jar ora viene fornito con Primetime Live Packager per configurare l&#39;accesso con le credenziali affidabili quando si invia un flusso RTMP a Primetime Live Packager

Ora è possibile configurare gli encoder in modo che utilizzino un nome utente o una password durante l&#39;invio dei flussi a Live Packager.

**PlaylistCreator Tool per creare manifesti di primo livello per HDS e HLS**

PlaylistCreator.jar è ora disponibile con Primetime Offline Packager per creare facilmente file manifesto di primo livello per le risorse HDS e HLS.

**Funzionalità di sicurezza aggiuntiva per l&#39;incorporazione di un modulo di protezione hardware**

Primetime Offline Packager ora supporta l&#39;accesso al certificato di credenziali Packager e alle chiavi comuni da un modulo di protezione hardware.

Un modulo di sicurezza hardware fornisce ulteriore protezione a queste risorse riservate.

**Prestazioni migliorate per il pacchetto VOD**

Sono stati incorporati diversi miglioramenti delle prestazioni per migliorare il tempo di creazione del pacchetto per le risorse mezzanine in Primetime Offline Packager

**Prestazioni migliorate per la creazione di pacchetti JIT MP4**

Diversi miglioramenti in termini di prestazioni sono stati integrati nelle funzionalità di creazione di pacchetti JIT di Primetime Origin per gestire le richieste degli utenti per una grande libreria di risorse VOD.

##  Adobe Primetime Streaming Server 1.4 {#adobe-primetime-streaming-server}

### Requisiti minimi di sistema {#minimum-system-requirements}

**Requisiti di rete**

* La rete deve essere abilitata per l&#39;invio di flussi MPEG-TS da un codificatore a Live Packager. Live Packager accetta anche un flusso RTMP da un codificatore che non richiede una rete multicast.

**Sistemi operativi supportati**

* Linux CentOS 6.3 a 64 bit

**Requisiti hardware**

* Processore Intel® Pentium® 4 a 3,2 GHz (consigliato dual Intel Xeon® o più veloce)
* Sistemi operativi a 64 bit: 4 GB di RAM (consigliati 8 GB)
* Scheda Ethernet da 1 Gb consigliata (sono supportate più schede di rete e 10 Gb)
* Disco:

   * (Disk-SAS): Almeno 10 GB con 7,5.000 rpm
   * (Disk-SSD): Lettura/scrittura a 400 MBps
   * (NAS): Collegamento dedicato da 1 GB

**Requisiti software**

*  Oracle Java JRE 1.7 (consigliato: Sun/ Oracle Hotspot JVM). JDK è richiesto per l&#39;accesso JConsole alle API JMX

### Installazione e configurazione di Primetime Streaming Server {#install-and-configure-primetime-streaming-server}

**Installare il server di streaming**

1. Scaricate il software Java SE e JDK dal [ sito Oracle](https://www.oracle.com/technetwork/java/javase/downloads/index.html) e seguite le istruzioni di installazione.
2. Estrarre il  file di archivio di Adobe Primetime-Streaming Server 1.4, `Primetime- StreamingServer-1-4-0-b206-12042014.zip` sul disco.

**Avviare Primetime Streaming Server**

Per avviare il server di streaming, eseguire il comando seguente dalla riga di comando nella directory principale del server di streaming:\
`$./pss_start.sh`

**Configurare Primetime Streaming Server come Live Packager o HTTP Origin Server**

Per configurare il server di streaming come Live Packager o il server di origine, aggiornate il file di configurazione pss.xml collocato nella directory conf della directory principale del server di streaming:

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

**Riavviare Primetime Streaming Server**

Per riavviare il server di streaming, arrestare e avviare il server di streaming.

<!-- 

Comment Type: draft

**Configuring Primetime Streaming Server**

Refer the Primetime Streaming Server Getting Started document for the configuration details available at [https://help.adobe.com/en_US/primetime/platform/primetime_streaming_server.pdf](https://help.adobe.com/en_US/primetime/platform/primetime_streaming_server.pdf).

-->

**Disinstallazione di Primetime Streaming Server**

Per disinstallare il server di streaming, arrestare il server di streaming e rimuovere la directory pss del server di streaming nella directory Primetime

## Utilizzo di Live Packager e Origin Server 1.4 {#working-with-live-packager-and-origin-server}

Questa sezione si applica quando Primetime Streaming Server non viene utilizzato e viene distribuito Primetime Live Packager AND/OR Primetime Origin Server

### Requisiti minimi di sistema {#minimum-system-requirements-1}

**Requisiti di rete**

* La rete deve essere abilitata per l&#39;invio di flussi MPEG-TS da un codificatore a Live Packager. Live Packager accetta anche un flusso RTMP da un codificatore che non richiede una rete multicast.

**Sistemi operativi supportati**

* Linux CentOS 6.3 a 64 bit

**Requisiti hardware**

* Processore Intel® Pentium® 4 a 3,2 GHz (consigliato dual Intel Xeon® o più veloce)
* Sistemi operativi a 64 bit: 4 GB di RAM (consigliati 8 GB)
* Scheda Ethernet da 1 Gb consigliata (sono supportate più schede di rete e 10 Gb)
* Disco:

   * (Disk-SAS): Almeno 10 GB con 7,5.000 rpm
   * (Disk-SSD): Lettura/scrittura a 400 MBps
   * (NAS): Collegamento dedicato da 1 GB

**Requisiti software**

*  Oracle Java JRE 1.7 (consigliato: Sun/ Oracle Hotspot JVM). JDK è richiesto per l&#39;accesso JConsole alle API JMX

I requisiti minimi di sistema indicati sopra sono validi sia per Origin Server che per Live Packager.

### Installare e configurare Live Packager {#install-and-configure-the-live-packager}

**Installazione di Live Packager**

1. Scaricate il software Java SE e JDK dal [ sito Oracle](https://www.oracle.com/technetwork/java/javase/downloads/index.html) e seguite le istruzioni di installazione.
1. Estrarre il file di archivio  Adobe Primetime - Live Packager 1.4 `Primetime-LivePackager-1-4-0-b206-12042014.zip` sul disco.

**Installazione del server di origine HTTP**

1. Scaricate il software Java JRE e JDK dal [ sito Oracle](https://www.oracle.com/technetwork/java/javase/downloads/index.html) e seguite le istruzioni di installazione.
1. Estrarre il file di archivio  Adobe Primetime - HTTP Origin Server 1.4, `Primetime-HttpOrigin-1-4-0-b206-12042014.zip`, sul disco.

**Per avviare Live** PackagerPer avviare il packager, eseguite il seguente comando dalla directory principale del packager:\
`$packager_start.sh`

**Per avviare il server di origine HTTP**

Per avviare il server di origine HTTP, esegui il comando seguente dalla riga di comando nella directory principale del server di origine:\
`$./origin_start.sh`

**Arrestare Live Packager**

Per arrestare il packager, eseguite il comando seguente dalla directory principale del packager:\
`$packager_stop.sh`

**Arrestare il server di origine HTTP**

Per arrestare il server di origine HTTP, eseguite il comando seguente nella directory principale del server di origine:\
`$./origin_stop.sh`

**Riavviate Live Packager**

Per riavviare il packager, arrestate e avviate il packager.

**Nota**: Quando viene avviato, il packager tenta di inizializzare le informazioni di avvio dal target del frammento nella directory temporanea. Se le informazioni di avvio vengono trovate nella destinazione del frammento, significa che il packager è stato riavviato. In caso di riavvio, il packager attende fino al limite successivo del frammento e quindi avvia il package. Il packager inserisce una voce gap nel bootstrap per indicare che mancano frammenti.

**Riavvia il server di origine HTTP**

Per riavviare il server di origine HTTP, arrestate e avviate il server di origine HTTP.

**Configurazione di Live Packager**

Il file di distribuzione contiene una configurazione di esempio che può essere utilizzata per testare il packager.

Dopo aver estratto l&#39;archivio  Adobe Primetime - Live Packager 1.4, modificate le directory nella directory del packager ed eseguite lo script packager_start.sh. La configurazione di esempio ascolta l&#39;indirizzo multicast 239.235.0.3:14000 ed esegue il server di origine locale sulla porta 8080. L&#39;output è configurato per essere scritto in `packager/webroot/_default_/_default_/ directory`.

<!-- 

Comment Type: draft

For more details about the configuration refer [the Primetime Live Packager document](https://help.adobe.com/en_US/primetime/api/packagers/index.html).

-->

**Configurazione del server di origine HTTP**

Per i dettagli di configurazione disponibili qui, consultare la Guida introduttiva del server di origine HTTP Primetime.

**Disinstallazione di Live Packager**

Per disinstallare il packager, arrestate il packager e rimuovete la directory del packager dalla directory Primetime.

**Disinstallazione del server di origine HTTP**

Per disinstallare il server di origine HTTP, arrestate il server di origine HTTP e rimuovete la directory di origine HTTP del server di origine HTTP nella directory Primetime.

##  Adobe Primetime Offline Packager 1.4 {#adobe-primetime-offline-packager}

### Requisiti minimi di sistema {#minimum-system-requirements-2}

**Sistemi operativi supportati**

* Linux CentOS 6.3 a 64 bit

**Requisiti hardware**

* Processore Intel® Pentium® 4 a 3,2 GHz (consigliato dual Intel Xeon® o più veloce)
* Sistemi operativi a 64 bit: 4 GB di RAM (consigliati 8 GB)
* Scheda Ethernet da 1 Gb consigliata (sono supportate più schede di rete e 10 Gb)
* Disco:

   * (Disk-SAS): Almeno 10 GB con 7,5.000 rpm
   * (Disk-SSD): Lettura/scrittura a 400 MBps
   * (NAS): Collegamento dedicato da 1 GB

**Requisiti software**

*  Oracle Java JRE 1.7 o versione successiva.

### Installazione e configurazione di Offline Packager {#install-and-configure-offline-packager}

Per installare Offline Packager, effettuate le seguenti operazioni:

1. Scaricate il software Java SE dal [ sito Oracle](https://www.oracle.com/technetwork/java/javase/downloads/index.html) e seguite le istruzioni di installazione.
1. Estrarre il file di archivio  Adobe Primetime - Offline Packager 1.4, `Primetime- OfflinePackager-1-4-0-b206-12042014.zip`, sul disco.

Per i dettagli di configurazione disponibili in [qui](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html), consultare la Guida introduttiva di Primetime Offline Packager.

## Risorse utili {#helpful-resources}

* Consulta la documentazione completa della guida in linea alla pagina [ Informazioni e supporto per Adobe Primetime](https://helpx.adobe.com/support/primetime.html).