---
title: Riferimento proprietà server
description: Riferimento proprietà server
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 0%

---


# Riferimento proprietà server{#server-properties-reference}

<!--<a id="section_EC8810492A454BDBA6013FE376360F4E"></a>-->

## Individualization Server

<table id="table_ats_tk2_jr">  
 <thead> 
  <tr> 
   <th class="entry"> Configurazione </th> 
   <th class="entry"> Descrizione </th> 
   <th class="entry"> Esempio </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> Credenziali di trasporto </td> 
   <td>La credenziale di trasporto viene utilizzata per decrittografare le richieste ricevute dal client e firmare le risposte restituite. Assicurati di configurare il file <span class="filepath"> AdobeInitial.properties</span> in modo appropriato sia con il percorso del file delle credenziali di trasporto sia con la password PKCS12 crittografata. </td> 
   <td> 
    <ul id="ul_itx_fl2_jr"> 
     <li id="li_A2E65253F37245268A41E6B9C958C8DF"><span class="codeph"> cert.i15n.transport.file =  </span> [file PKCS12 contenente il certificato e la chiave di trasporto Individualization] </li> 
     <li id="li_28CDFC0B3D684795AF4708B6D26DF83F"><span class="codeph"> cert.i15n.transport.password = </span> [Password crittografata per il file PKCS12] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> Credenziale CA per l'identificazione </td> 
   <td>Il server Individualization utilizza la credenziale Individualization CA per firmare i certificati computer che genera. Assicurati di configurare il file <span class="filepath"> AdobeInitial.properties</span> in modo appropriato sia con il percorso del file di credenziali CA I15N sia con la password PKCS12 crittografata. </td> 
   <td> 
    <ul id="ul_xsj_nl2_jr"> 
     <li id="li_5A770D8A482F41A4A9AB63CA52C2EB90"><span class="codeph"> cert.i15n.ica.file = </span> [PKCS12 file contenente il certificato e la chiave della CA Individualization] </li> 
     <li id="li_C3C4A2D9AA2A4F86B6DDCFFD9CB55CBB"><span class="codeph"> cert.i15n.ica.password = </span> [Password crittografata per il file PKCS12] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> Credenziali di cifratura dell'individualizzazione </td> 
   <td> Il server Individualization utilizza le credenziali Encryption per crittografare i file sensibili che devono essere trasmessi ai server Individualization. Ad esempio, questo certificato supporta la migrazione delle licenze e viene utilizzato anche per crittografare le chiavi private DRM per i server Individualization. </td> 
   <td> 
    <ul id="ul_nbr_kpd_w5"> 
     <li id="li_4226AD6CC85740669DAF467EFD00BBBE"><span class="codeph"> cert.i15n.decryption.file=i15n_transport.pfx</span> </li> 
     <li id="li_F51BDD94F4724FA58CEF9470B6FEE33B"><span class="codeph"> cert.i15n.decryption.password=password</span> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> Cache dei contenuti </td> 
   <td>Queste impostazioni controllano la posizione da cui il server Individualization scarica il contenuto e la posizione in cui il contenuto viene memorizzato nella cache su disco. Il server Individualization controlla il server dei contenuti una volta all'avvio, quindi alla frequenza/ora specificate da queste proprietà. <p>Per il server di individuazione locale on, abbiamo incluso un set iniziale di dati della cache del contenuto. Assicurati di copiare la cartella <i>CONTENTS</i> della cache (non la cartella cache stessa) nella posizione <span class="filepath"> AdobeInitial.properties</span> <span class="codeph"> contentServer.localDirectory</span> configurata. </p> </td> 
   <td> 
    <ul id="ul_r4n_1r2_jr"> 
     <li id="li_CA5F562577B04B4A9966EF46E039A137"><span class="codeph"> contentServer.localDirectory =</span> [Directory in cui memorizzare il contenuto locale (normalmente tomcat/temp)] </li> 
     <li id="li_9A78FBD6C54D47708226378340B46E8E"><span class="codeph"> contentServer.server =</span> [Server Web da contattare per informazioni ECI (<i>non supportato in questa versione</i>)] </li> 
     <li id="li_4E7D7F76085D411688B5003E855F860B"><span class="codeph"> contentServer.timeout =</span> [Timeout connessione, in secondi] </li> 
     <li id="li_4B751F238A1643A7AC730CD9354887B6"><span class="codeph"> contentServer.pollFrequency =</span> [Frequenza del polling del server, in giorni (minimo 1 giorno)] </li> 
     <li id="li_8E23C3C6E7EF46B0AFDD7993DE79F142"><span class="codeph"> contentServer.pollTime = </span> [Ora del giorno per il polling del server, in minuti dalla mezzanotte] </li> 
    </ul> <p>Leggi la sezione <i>CRL e ECI Files</i> per informazioni su come mantenere la cache aggiornata. </p> </td> 
  </tr> 
  <tr> 
   <td> Individuazione CA CRL </td> 
   <td> <p>Il punto di distribuzione dell’elenco di revoca dei certificati (CRL) è incluso in ogni certificato computer rilasciato dal server di Individualization. Durante la convalida del certificato del computer sul server licenze, il CRL verrà scaricato dal punto di distribuzione elencato nel certificato (o letto dalla cache se già scaricato) e controllato per verificare che il certificato non sia stato revocato. È consigliabile eseguire questa modifica della configurazione del server dopo aver completato il processo di creazione e distribuzione dell'Individualization CA CRL. Riavvia il server Individualization dopo qualsiasi modifica della configurazione. </p> <p>Per impostare l'URL per il punto di distribuzione CRL, è necessario impostare il campo <span class="filepath"> AdobeInitial.properties</span> <span class="codeph"> cert.machine.crldp</span> . </p> </td> 
   <td> 
    <ul id="ul_eq3_lv2_jr"> 
     <li id="li_5E37A9E318D742B6A5E1035120888819"><span class="codeph"> cert.machine.crldp = </span> [punto di distribuzione CRL] </li> 
    </ul> <p>Ad esempio: </p>
    <p> <code>
      cert.machine.crldp__DEV=<span>tps://onprem-individualization.com</span>CRL/onprem-individualization-ca.crl
     </code></p>
     <p>Il server licenze deve scaricare automaticamente questo CRL una volta gestita la richiesta di licenza. </p> <p importance="high">Nota: Questo punto di distribuzione è <i>non</i> controllato da Primetime DRM per la validità. Verifica che questo URL sia valido. Gli errori risultanti da un URL non valido verranno visualizzati solo dopo che gli errori di convalida saranno stati visualizzati dal server licenze. </p> </td> 
  </tr> 
  <tr> 
   <td> Registrazione </td> 
   <td>Configura il file <span class="filepath"> AdobeInitial.properties</span> per la registrazione come necessario. </td> 
   <td> 
    <ul id="ul_j1v_kw2_jr"> 
     <li id="li_B60002B33A3042FCBE1F694454966469"><span class="codeph"> adobe.weblogs.loc = </span> [Directory in cui verranno creati i file di registro] </li> 
     <li id="li_2DD4406FBBF047589BAAAE1C9082D8B3"><span class="codeph"> log.Level =</span> [Il livello più basso dei messaggi di log che possono apparire nei log  <span class="codeph"> [DEBUG | INFORMAZIONI]</span> ] </li> 
     <li id="li_610FAF239A554CE59DAC455174F0CF0A"><span class="codeph"> log.FileName = </span> [Prefisso per i file di log. Data/ora e l'estensione ".log" verrà aggiunta al nome del file] </li> 
     <li id="li_1F2913B209BE4A0E8207FAAD052D1764"><span class="codeph"> log.RollInterval =</span> [Specifica la frequenza di scorrimento dei log.] </li> 
     <li id="li_3F46C15488114BB5B41035F710E7A19F"><span class="codeph"> log.RollSize = </span> [Ruota i log quando raggiungono questa dimensione (i Registri gireranno quando viene raggiunto il  <span class="codeph"> </span> RollIntervalor  <span class="codeph"> </span> RollSizeis, a seconda di quale dei due si verifica per primo)] </li> 
     <li id="li_DA32E862F7B0413885DA20633B682484"><span class="codeph"> log.ReportLogging.Enabled =</span>[ [true | false ] Specifica se è necessario generare un file separato contenente i dati utilizzati dall'Adobe per generare rapporti di Individualizzazione.] </li> 
     <li id="li_465CC6D81B8A484CBF4E7A39F7AF86AA"><span class="codeph"> log.ReportLogging.FileName = </span> [Prefisso per i file di registro dei report. Al nome del file verranno aggiunti data/ora e l'estensione <span class="filepath"> .log</span> . La proprietà l<span class="codeph"> og.Level</span> non si applica a questo file di log, ma <span class="codeph"> log.RollInterval</span> e <span class="codeph"> log.RollSize</span> do.] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> Altro </td> 
   <td></td> 
   <td> 
    <ul id="ul_b3b_g1f_jr"> 
     <li id="li_FACF07CB332D416E91FD34DE48152FAA"><span class="codeph"> deviceinfo.key = </span> [Chiave codificata Base64 crittografata utilizzata per le informazioni sul dispositivo HMAC prima di includerla nel token del computer. La chiave può essere diversa per gli ambienti di sviluppo/staging/produzione, ma deve essere la stessa per tutti i server in un particolare ambiente. ] </li> 
     <li id="li_B19C77FD6F91496294DBF836A1922EE1"><span class="codeph"> keys.kgs.server =</span> [Posizione del server Key Gen (un singolo host/porta, che rappresenta un pool di server chiavi) ] </li> 
     <li id="li_5DA3C89770804B148EF6FAF01A5AD958"><span class="codeph"> keys.MinQueueSize = </span> [Recupera un altro batch di chiavi dal KGS quando ci sono queste molte chiavi rimanenti nella coda] </li> 
     <li id="li_0C2E5F2FDB824182A6BE418B041D2F28"><span class="codeph"> status.Timeout =</span> [La pagina di stato eseguirà il ping del KGS per determinare se può raggiungere il server. Si verificherà un timeout se una risposta non viene ricevuta nuovamente nel periodo di tempo specificato.] </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## Server di generazione chiavi {#section_37FA8EEBA258461F8CFA3ADF37714577}

<table id="table_ats_tk2_js"> 
 <thead> 
  <tr> 
   <th class="entry"> Configurazione </th> 
   <th class="entry"> Descrizione </th> 
   <th class="entry"> Esempio </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> Generazione di chiavi </td> 
   <td></td> 
   <td> 
    <ul id="ul_nlj_ydf_jr"> 
     <li id="li_E4347D572F004BF0B237A662BFE7F3ED"><span class="codeph"> kgs.Threads =</span> [Numero di thread da utilizzare per generare chiavi (dovrebbe corrispondere al numero di processori disponibili sul computer)] </li> 
     <li id="li_EDBC2535D48E4A66AEB240DB337187FC"><span class="codeph"> kgs.BatchSize =</span> [Numero di chiavi da generare per batch] </li> 
     <li id="li_07B41546D94F42349103BF8AF4605E14"><span class="codeph"> kgs.KeyDirectory =</span> [Directory in cui memorizzare i file batch di chiavi] </li> 
     <li id="li_F4962C97DC3D491DA7FAC826E38A4459"><span class="codeph"> kgs.MaxQueueSize =</span> [Numero massimo di file batch di chiavi da generare] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> Registrazione </td> 
   <td></td> 
   <td> 
    <ul id="ul_kwq_12f_jr"> 
     <li id="li_5E5D34FE5EB44BB898090494C7DDEBD8"><span class="codeph"> adobe.weblogs.loc = </span> [Directory in cui verranno creati i file di registro] </li> 
     <li id="li_0E34CD32CD5E47729B69B50414F93678"><span class="codeph"> log.FileName = </span> [Prefisso per i file di log. Data/ora e l'estensione <span class="filepath"> .log</span> verrà aggiunta al nome del file] </li> 
     <li id="li_8AB15ACEC39041A2A04C7301154C6EDB"><span class="codeph"> log.Level =</span> [Il livello più basso dei messaggi di log che possono apparire nei log] </li> 
     <li id="li_A17E84DA3ED243F381FF3A6184A3CAA0"><span class="codeph"> log.RollInterval =</span> [Specifica la frequenza di scorrimento dei log.] </li> 
     <li id="li_C2B3D111608945DA9D1428BE98D61664"><span class="codeph"> log.RollSize = </span> [Ruota i log quando raggiungono questa dimensione (i Registri gireranno quando viene raggiunto il  <span class="codeph"> </span> RollIntervalor  <span class="codeph"> </span> RollSizeis, a seconda di quale dei due si verifica per primo)] </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
