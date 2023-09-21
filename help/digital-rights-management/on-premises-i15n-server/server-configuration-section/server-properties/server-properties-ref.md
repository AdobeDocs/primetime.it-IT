---
title: Riferimento proprietà server
description: Riferimento proprietà server
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 0%

---

# Riferimento proprietà server{#server-properties-reference}

<!--<a id="section_EC8810492A454BDBA6013FE376360F4E"></a>-->

## Server di personalizzazione

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
   <td>Le credenziali di trasporto vengono utilizzate per decrittografare le richieste ricevute dal client e firmare le risposte inviate. Assicurati di configurare <span class="filepath"> AdobeInitial.properties</span> con il percorso del file delle credenziali di trasporto e la password crittografata PKCS12. </td> 
   <td> 
    <ul id="ul_itx_fl2_jr"> 
     <li id="li_A2E65253F37245268A41E6B9C958C8DF"><span class="codeph"> cert.i15n.transport.file = </span> [File PKCS12 contenente il certificato e la chiave di trasporto per l'individuazione] </li> 
     <li id="li_28CDFC0B3D684795AF4708B6D26DF83F"><span class="codeph"> cert.i15n.transport.password =</span> [Password crittografata per il file PKCS12] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> Credenziali CA di personalizzazione </td> 
   <td>Il server di personalizzazione utilizza le credenziali CA di personalizzazione per firmare i certificati del computer che emette. Assicurati di configurare <span class="filepath"> AdobeInitial.properties</span> file in modo appropriato sia con il percorso del file di credenziali CA I15N che con la password crittografata PKCS12. </td> 
   <td> 
    <ul id="ul_xsj_nl2_jr"> 
     <li id="li_5A770D8A482F41A4A9AB63CA52C2EB90"><span class="codeph"> cert.i15n.ica.file =</span> [File PKCS12 contenente il certificato e la chiave della CA di Personalizzazione] </li> 
     <li id="li_C3C4A2D9AA2A4F86B6DDCFFD9CB55CBB"><span class="codeph"> cert.i15n.ica.password =</span> [Password crittografata per il file PKCS12] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> Credenziali di crittografia per la personalizzazione </td> 
   <td> Il server di individuazione utilizza le credenziali di crittografia per crittografare i file sensibili che devono essere trasmessi ai server di individuazione. Ad esempio, questo certificato supporta la migrazione delle licenze e viene utilizzato anche per crittografare le chiavi private DRM per i server di personalizzazione. </td> 
   <td> 
    <ul id="ul_nbr_kpd_w5"> 
     <li id="li_4226AD6CC85740669DAF467EFD00BBBE"><span class="codeph"> cert.i15n.decryption.file=i15n_transport.pfx</span> </li> 
     <li id="li_F51BDD94F4724FA58CEF9470B6FEE33B"><span class="codeph"> cert.i15n.decryption.password=password</span> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> Cache contenuto </td> 
   <td>Queste impostazioni controllano la posizione da cui il server di personalizzazione scarica il contenuto e da cui il contenuto viene memorizzato nella cache del disco. Il server di personalizzazione verifica la presenza di nuovi contenuti nel server dei contenuti una volta all'avvio e quindi alla frequenza/ora specificata da queste proprietà. <p>Per il server di personalizzazione locale è stato incluso un set iniziale di dati della cache del contenuto. Assicurati di copiare <i>SOMMARIO</i> della cartella della cache (non la cartella della cache stessa) al <span class="filepath"> AdobeInitial.properties</span> <span class="codeph"> contentServer.localDirectory</span> posizione. </p> </td> 
   <td> 
    <ul id="ul_r4n_1r2_jr"> 
     <li id="li_CA5F562577B04B4A9966EF46E039A137"><span class="codeph"> contentServer.localDirectory =</span> [Directory in cui memorizzare il contenuto locale (in genere tomcat/temp)] </li> 
     <li id="li_9A78FBD6C54D47708226378340B46E8E"><span class="codeph"> contentServer.server =</span> [Server web da contattare per informazioni ECI (<i>non supportato in questa versione</i>)] </li> 
     <li id="li_4E7D7F76085D411688B5003E855F860B"><span class="codeph"> contentServer.timeout =</span> [Timeout connessione, in secondi] </li> 
     <li id="li_4B751F238A1643A7AC730CD9354887B6"><span class="codeph"> contentServer.pollFrequency =</span> [Frequenza di polling del server, in giorni (minimo 1 giorno)] </li> 
     <li id="li_8E23C3C6E7EF46B0AFDD7993DE79F142"><span class="codeph"> contentServer.pollTime =</span> [Ora del giorno in cui eseguire il polling del server, in minuti dalla mezzanotte] </li> 
    </ul> <p>Assicurati di leggere la sezione <i>File CRL ed ECI</i> informazioni su come mantenere la cache aggiornata. </p> </td> 
  </tr> 
  <tr> 
   <td> CRL CA di personalizzazione </td> 
   <td> <p>Questo punto di distribuzione CRL (Certificate Revocation List) è incluso in ogni certificato del computer rilasciato dal server di personalizzazione. Durante la convalida del certificato del computer sul server licenze, il CRL verrà scaricato dal punto di distribuzione elencato nel certificato (o letto dalla cache se già scaricato) e selezionato per verificare che il certificato non sia stato revocato. Si consiglia di apportare questa modifica alla configurazione del server dopo aver completato il processo di creazione e distribuzione del CRL CA di personalizzazione. Riavvia il server di personalizzazione dopo qualsiasi modifica della configurazione. </p> <p>Per impostare l'URL del punto di distribuzione CRL, è necessario impostare <span class="filepath"> AdobeInitial.properties</span> <span class="codeph"> cert.machine.crldp</span> campo. </p> </td> 
   <td> 
    <ul id="ul_eq3_lv2_jr"> 
     <li id="li_5E37A9E318D742B6A5E1035120888819"><span class="codeph"> cert.machine.crldp =</span> [punto di distribuzione CRL] </li> 
    </ul> <p>Ad esempio: </p>
    <p> <code>
      cert.machine.crldp__DEV=<span>tps://onprem-individualization.com</span>CRL/onprem-individualization-ca.crl
     </code></p>
     <p>Il server licenze deve scaricare automaticamente questo CRL una volta gestita una richiesta di licenza. </p> <p importance="high">Nota: questo punto di distribuzione è <i>non</i> verifica della validità da parte di DRM Primetime. Verifica che questo URL sia valido. Gli errori risultanti da un URL non valido verranno visualizzati solo dopo la visualizzazione degli errori di convalida dal server licenze. </p> </td> 
  </tr> 
  <tr> 
   <td> Registrazione </td> 
   <td>Configurare <span class="filepath"> AdobeInitial.properties</span> per la registrazione in base alle esigenze. </td> 
   <td> 
    <ul id="ul_j1v_kw2_jr"> 
     <li id="li_B60002B33A3042FCBE1F694454966469"><span class="codeph"> adobe.weblogs.loc =</span> [Directory in cui verranno creati i file di registro] </li> 
     <li id="li_2DD4406FBBF047589BAAAE1C9082D8B3"><span class="codeph"> log.Level =</span> [Il livello più basso di messaggi di registro che possono comparire nei registri <span class="codeph"> [DEBUG | INFORMAZIONI]</span> ] </li> 
     <li id="li_610FAF239A554CE59DAC455174F0CF0A"><span class="codeph"> log.FileName =</span> [Prefisso per i file di registro. Data/ora ed estensione ".log" verranno aggiunte al nome file] </li> 
     <li id="li_1F2913B209BE4A0E8207FAAD052D1764"><span class="codeph"> log.RollInterval =</span> [Specifica la frequenza con cui viene eseguito il rollback dei registri.] </li> 
     <li id="li_3F46C15488114BB5B41035F710E7A19F"><span class="codeph"> log.RollSize =</span> [Eseguire il roll dei log quando raggiungono questa dimensione (i log verranno roll quando <span class="codeph"> RollInterval</span> o <span class="codeph"> DimensioneRullo</span> viene raggiunto, a seconda di quale dei due eventi si verifica per primo)] </li> 
     <li id="li_DA32E862F7B0413885DA20633B682484"><span class="codeph"> log.ReportLogging.Enabled =</span>[ [true | false ] Specifica se deve essere generato un file separato contenente i dati utilizzati dall'Adobe per generare rapporti di personalizzazione.] </li> 
     <li id="li_465CC6D81B8A484CBF4E7A39F7AF86AA"><span class="codeph"> log.ReportLogging.FileName =</span> [Prefisso per i file di registro dei rapporti. Data/ora e <span class="filepath"> .log</span> L'estensione verrà aggiunta al nome del file. L<span class="codeph"> og.Level</span> non si applica a questo file di registro, ma <span class="codeph"> log.RollInterval</span> e <span class="codeph"> log.RollSize</span> sì.] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> Altro </td> 
   <td></td> 
   <td> 
    <ul id="ul_b3b_g1f_jr"> 
     <li id="li_FACF07CB332D416E91FD34DE48152FAA"><span class="codeph"> deviceinfo.key =</span> [Chiave crittografata Base64 utilizzata per le informazioni sul dispositivo HMAC prima di includerla nel token del computer. La chiave può essere diversa per gli ambienti di sviluppo/staging/produzione, ma deve essere la stessa per tutti i server in un particolare ambiente. ] </li> 
     <li id="li_B19C77FD6F91496294DBF836A1922EE1"><span class="codeph"> keys.kgs.server =</span> [Posizione di Key Gen Server (un singolo host/porta, che rappresenta un pool di server chiave) ] </li> 
     <li id="li_5DA3C89770804B148EF6FAF01A5AD958"><span class="codeph"> keys.MinQueueSize =</span> [Recupera un altro batch di chiavi dal KGS quando sono presenti così tante chiavi nella coda] </li> 
     <li id="li_0C2E5F2FDB824182A6BE418B041D2F28"><span class="codeph"> status.Timeout =</span> [La pagina Stato eseguirà il ping del KGS per determinare se può raggiungere il server. Si verificherà un timeout se una risposta non viene ricevuta entro il periodo di tempo specificato.] </li> 
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
   <td> Generazione chiave </td> 
   <td></td> 
   <td> 
    <ul id="ul_nlj_ydf_jr"> 
     <li id="li_E4347D572F004BF0B237A662BFE7F3ED"><span class="codeph"> kgs.Threads =</span> [Numero di thread da utilizzare per generare le chiavi (deve essere uguale al numero di processori disponibili nel computer)] </li> 
     <li id="li_EDBC2535D48E4A66AEB240DB337187FC"><span class="codeph"> kgs.BatchSize =</span> [Numero di chiavi da generare per batch] </li> 
     <li id="li_07B41546D94F42349103BF8AF4605E14"><span class="codeph"> kgs.KeyDirectory =</span> [Directory in cui memorizzare i file batch chiave] </li> 
     <li id="li_F4962C97DC3D491DA7FAC826E38A4459"><span class="codeph"> kgs.MaxQueueSize =</span> [Numero massimo di file batch chiave da generare] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> Registrazione </td> 
   <td></td> 
   <td> 
    <ul id="ul_kwq_12f_jr"> 
     <li id="li_5E5D34FE5EB44BB898090494C7DDEBD8"><span class="codeph"> adobe.weblogs.loc =</span> [Directory in cui verranno creati i file di registro] </li> 
     <li id="li_0E34CD32CD5E47729B69B50414F93678"><span class="codeph"> log.FileName =</span> [Prefisso per i file di registro. Data/ora e <span class="filepath"> .log</span> l'estensione verrà aggiunta al nome del file] </li> 
     <li id="li_8AB15ACEC39041A2A04C7301154C6EDB"><span class="codeph"> log.Level =</span> [Il livello più basso di messaggi di registro che possono essere visualizzati nei registri] </li> 
     <li id="li_A17E84DA3ED243F381FF3A6184A3CAA0"><span class="codeph"> log.RollInterval =</span> [Specifica la frequenza con cui viene eseguito il rollback dei registri.] </li> 
     <li id="li_C2B3D111608945DA9D1428BE98D61664"><span class="codeph"> log.RollSize =</span> [Eseguire il roll dei log quando raggiungono questa dimensione (i log verranno roll quando <span class="codeph"> RollInterval</span> o <span class="codeph"> DimensioneRullo</span> viene raggiunto, a seconda di quale dei due eventi si verifica per primo)] </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
