---
title: Proprietà del file di configurazione
description: Proprietà del file di configurazione
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '1121'
ht-degree: 0%

---


# Proprietà del file di configurazione {#configuration-file-properties}

Il file di configurazione specifica le seguenti proprietà. Per i nomi di proprietà che includono `n`, `n` rappresenta un numero intero che inizia con 1 e aumenta per ogni istanza della proprietà.

<table class="+ topic/table " id="table_p3x_54y_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> Opzione proprietà/riga di comando </th> 
   <th colname="2" class="- topic/entry entry"> Descrizione </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.name</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">npolicyname</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Il nome della politica leggibile dall'uomo. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.requiredKeyServer</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">keyServerBoolean</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Se true, per la distribuzione delle chiavi a iOS è necessario un server di chiavi HTTPS. Il valore predefinito è false, se non specificato. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.forcelJailbreak</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">forcementJailbreakboolean</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Se true, per i dispositivi che supportano il rilevamento jailbreak, non consentire la riproduzione se è stato rilevato jailbreak. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.critical</span> <p class="- topic/p "><span class="codeph"> - </span> <i class="+ topic/ph hi-d/i ">critico booleano</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Imposta criticità politica. Se true, il server deve comprendere tutte le parti del criterio (questo è il comportamento predefinito). Se false, il server potrebbe ignorare gli attributi dei criteri che non comprende. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chining.asymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry ">Certificato del server di licenza la cui chiave pubblica viene utilizzata per crittografare la chiave di crittografia principale per il <a href="../../../aaxs-protecting-content/content-introduction/content-usage-rules/content-other-policy-options/content-enhanced-license-chaining.md" format="dita" scope="local"> Concatenamento licenze avanzato </a>
   Questa proprietà specifica un file contenente solo il certificato (è accettabile il formato PEM o DER). </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chining.rootKey</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">rootKeyroot-key</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Specificare la chiave di crittografia radice per il concatenamento licenze avanzato. Se non viene specificata alcuna chiave e l’opzione Concatenamento licenze avanzato è abilitata, verrà generata una chiave casuale. La chiave deve avere una lunghezza di 16 byte e deve essere specificata come valore esadecimale. Lo spazio vuoto tra i valori esadecimali è facoltativo. Per gli aggiornamenti, l'opzione della riga di comando non è consentita e la proprietà viene ignorata. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.url</span> <p class="- topic/p "><span class="codeph"> - </span> <i class="+ topic/ph hi-d/i ">domainURLurl</i> </p> </td> 
   <td colname="2" class="- topic/entry "> URL del server di dominio, se è richiesta la registrazione del dominio. Per gli aggiornamenti, l'opzione della riga di comando non è consentita e la proprietà viene ignorata. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.anonymous</span> <p class="- topic/p "><span class="codeph"> -domainAnon</span> </p> </td> 
   <td colname="2" class="- topic/entry "> Specifica se la registrazione del dominio anonimo è consentita. Impostare la proprietà su true o includere questa opzione della riga di comando per consentire l'accesso anonimo. Questa opzione non può essere utilizzata con -domainAuthNS. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.authNamespace</span> <p class="- topic/p "><span class="codeph"> - </span> <i class="+ topic/ph hi-d/i ">domainAuthNSnamespace</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Spazio dei nomi di autenticazione per la registrazione del dominio. Se specificato, il client deve eseguire l'autenticazione con un nome utente e una password emessi dall'autorità specificata. Per gli aggiornamenti, l'opzione della riga di comando non è consentita e la proprietà viene ignorata. Questa opzione non può essere utilizzata con -domainAnon. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.analogico</span> <p class="- topic/p "><span class="codeph"> - </span> <i class="+ topic/ph hi-d/i ">opAnalogAnalogOption</i> </p> </td> 
   <td colname="2" class="- topic/entry ">Vincoli di protezione dell'uscita analogica. Sono supportati i seguenti valori: 
    <ul class="- topic/ul " id="ul_h4x_54y_n4"> 
     <li class="- topic/li " id="li_5BC8F39B61894E83A7B27570FF848F09"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> NO_PROTECTION</span> </p> </li> 
     <li class="- topic/li " id="li_FF14594A0714480496793A82C3FA1610"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE</span> </p> </li> 
     <li class="- topic/li " id="li_721FCC4DC1F34AE398EFAE4C0D3F50F5"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_ACP</span> </p> </li> 
     <li class="- topic/li " id="li_D588BB278BEE4CEAB034BD48550EBCDC"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_CGMSA</span> </p> </li> 
     <li class="- topic/li " id="li_7E5F006D2F114502BA6D0A9C4173004E"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> OBBLIGATORIO</span> </p> </li> 
     <li class="- topic/li " id="li_9EBFAA4AACF249C2A94432D88E12C3B9"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> REQUIRED_ACP</span> </p> </li> 
     <li class="- topic/li " id="li_6720C6A085864BEB957C0BF2C38551C9"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> REQUIRED_CGMSA</span> </p> </li> 
     <li class="- topic/li " id="li_6FD98473ECDB4A66AC4B506FB9B3B360"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> NO_PLAYBACK</span> </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">drmBlacklistname/value-pair</i> </p> </td> 
   <td colname="2" class="- topic/entry ">I client DRM non possono accedere ai contenuti protetti. Questa opzione specifica un elenco di versioni dei moduli DRM che potrebbero non essere utilizzate (elenco Bloccati). Il valore è costituito da coppie nome=valore separate da virgola con il seguente formato: <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|arch|model|fornitore|env|screen=value</span> </p> <p class="- topic/p ">Le coppie nome/valore aggiuntive devono essere separate da virgola. Ad esempio: <span class="codeph"> os=Win,release=2.0,arch=32</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">runtimeBlacklsitname/value-pair</i> </p> </td> 
   <td colname="2" class="- topic/entry ">I runtime dell’applicazione non possono accedere a contenuti protetti. Questa opzione specifica un elenco di versioni dei moduli di runtime che potrebbero non essere utilizzate (elenco Bloccati). Il valore è costituito da coppie nome=valore separate da virgola con il seguente formato: <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|application|arch|model|vendor|env|screen=value</span> </p> <p class="- topic/p ">Le coppie nome/valore aggiuntive devono essere separate da virgola. Ad esempio, <span class="codeph"> os=Win,application=AIR</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.v1DeviceCapabilities</span> <p class="- topic/p "><span class="codeph"> -devCapabilitiesV1</span> <i class="+ topic/ph hi-d/i ">coppie nome/valore</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica le funzionalità del dispositivo necessarie per accedere al contenuto protetto. Il valore è costituito da coppie nome=valore separate da virgola con il seguente formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> nonUserAccessibleBus|hardwareRootOfTrust=true|false</span> </p> <p class="- topic/p ">Ad esempio, <span class="codeph"> nonUserAccessibleBus=false,hardwareRootOfTrust=true</span>. Durante l'aggiornamento, utilizzare <span class="codeph"> -devCapabilitiesV1</span> senza gli argomenti rimanenti per rimuovere la restrizione delle funzionalità del dispositivo. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.syncFrequency</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">syncname/value-pair</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specificare la frequenza con cui i client devono inviare i messaggi di sincronizzazione al server. Se non è impostato, i client non invieranno messaggi di sincronizzazione durante la riproduzione di contenuto protetto con questo criterio. Il valore è costituito da coppie <span class="codeph"> name=value</span> separate da virgola con il seguente formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> start|force|hardStop=numberValue</span> </p> <p class="- topic/p "> 
     <ul id="ul_a5j_q4t_44"> 
      <li id="li_25CAF96C27F34848A95B2E3693847C71"><span class="codeph"> start</span>  (obbligatorio) - L'intervallo di avvio specifica che il client deve iniziare la sincronizzazione con il server a partire dall'ultima sincronizzazione. </li> 
      <li id="li_CC9068CFE75645029C947C9E1B53351F"><span class="codeph"> force</span>  (facoltativo) - La probabilità di sincronizzazione forzata è la probabilità (0-100) con cui il client deve forzare un messaggio di sincronizzazione durante la riproduzione. </li> 
      <li id="li_C31A6250F19348FBB8B7569D00C6314E"><span class="codeph"> hardStop</span>  (facoltativo) - L'intervallo di arresto rigido è il tempo in minuti dopo il quale il client non riesce a riprodurre se non è in grado di eseguire la sincronizzazione. Se impostato, deve essere maggiore dell'intervallo iniziale. </li> 
     </ul>Durante l'aggiornamento, utilizza <span class="codeph"> -sync</span> senza gli argomenti rimanenti per rimuovere i requisiti di sincronizzazione. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.useRootLicense</span> </td> 
   <td colname="2" class="- topic/entry ">Indica se questo criterio dispone di una licenza radice (vedere <i class="+ topic/ph hi-d/i ">Concatenamento licenze avanzato</i> in <i class="+ topic/ph hi-d/i ">Utilizzo dell'accesso Adobe per la protezione dei contenuti</i>). </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.startDate</span> </td> 
   <td colname="2" class="- topic/entry ">La data successiva alla quale il contenuto è valido. Utilizzare il formato <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-gg</span> (ad esempio, <span class="codeph"> 2009-01-31</span> rappresenta il 31 gennaio alle 12:00) o <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-gg-h24:min:sec</span> (ad esempio, <span class="codeph"> 2009-01-31-14:30:00</span> rappresenta il 31 gennaio alle 2:30 del pomeriggio). </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Data prima della quale il contenuto è valido. Non è possibile specificare contemporaneamente sia <span class="codeph"> policy.expiration.endDate</span> che policy.expiration.duration. Utilizzare il formato <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-gg</span> o <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-gg-h24:min:sec</span> (ad esempio, 2009-01-31-14:30:00 rappresenta il 31 gennaio alle 2:30 PM). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Il tempo di validità del contenuto (in minuti) a partire dal momento in cui viene compilato. Non è possibile specificare contemporaneamente sia <span class="codeph"> policy.expiration.endDate</span> che <span class="codeph"> policy.expiration.duration</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Quantità di tempo per cui una licenza può essere memorizzata nella cache del cliente (in minuti). Impostare questa proprietà su 0 per impedire il caching delle licenze. Il valore deve essere 0 o superiore. Non è possibile utilizzare contemporaneamente sia <span class="codeph"> policy.licenseCaching.duration</span> che <span class="codeph"> policy.licenseCaching.endDate</span>. </p> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Nota</b>: Questa impostazione dei criteri viene applicata solo alla memorizzazione in cache delle licenze sul disco. Non controlla la durata della licenza memorizzata nella cache. La licenza può essere memorizzata nella cache anche se la durata specificata dal criterio è zero. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Data successiva alla quale le licenze non possono essere memorizzate nella cache. Non è possibile utilizzare contemporaneamente sia <span class="codeph"> policy.licenseCaching.duration</span> che <span class="codeph"> policy.licenseCaching.endDate</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.anonymous</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica se l'acquisizione di licenze anonime è consentita. Il valore predefinito è "false" (l'autenticazione nome utente/password è obbligatoria) se non specificato. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.authNamespace</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se è richiesta l'autenticazione tramite nome utente/password, questa proprietà specifica un qualificatore di nome facoltativo per i nomi utente. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Coppie nome/valore personalizzate che devono essere utilizzate dal server durante l'acquisizione della licenza. Utilizza il formato seguente per specificare le proprietà: <span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span>=<span class="+ topic/ph pr-d/codeph codeph">name</span>=<span class="+ topic/ph pr-d/codeph codeph">value</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.playbackWindow</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica la finestra di riproduzione (in minuti), la durata della validità della licenza dopo la prima riproduzione di contenuto protetto. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.digital</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Vincoli di protezione dell'output. I valori devono essere uno dei seguenti: </p> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">NO_PROTECTION, USE_IF_AVAILABLE, OBBLIGATORIO, NO_PLAYBACK</i> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Il modulo DRM deve avere il livello di sicurezza minimo specificato, o superiore, per accedere al contenuto protetto. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Per accedere al contenuto protetto, il modulo runtime dell’applicazione deve disporre del livello di protezione minimo specificato o superiore. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedAIRApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Un elenco consentiti di applicazioni Adobe AIR o iOS autorizzate a riprodurre contenuti protetti. La proprietà deve utilizzare il formato seguente: <span class="+ topic/ph pr-d/codeph codeph">pubId</span>[:<span class="+ topic/ph pr-d/codeph codeph">appId</span>[:[<span class="+ topic/ph pr-d/codeph codeph">min</span>]:[<span class="+ topic/ph pr-d/codeph codeph">max</span>]]] </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedSWFApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Un elenco consentiti di applicazioni SWF autorizzate a riprodurre contenuto protetto. Utilizza il formato seguente: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"></span> URLor file=<span class="+ topic/ph pr-d/codeph codeph">swf_file</span>,time=<i class="+ topic/ph hi-d/i ">max_time_to_</i> <i class="+ topic/ph hi-d/i ">verifyswf_</i> file è il file SWF per il quale calcolare l'hash e  <i class="+ topic/ph hi-d/i ">max_time_to_</i> verifyè il tempo massimo per consentire il download e la verifica del file SWF da completare (in secondi). </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Coppie personalizzate di nome/valore da includere nelle licenze rilasciate agli utenti. Utilizza il formato seguente: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n</span>=<span class="+ topic/ph pr-d/codeph codeph">name</span>=<span class="+ topic/ph pr-d/codeph codeph">value</span> </p> <p class="- topic/p ">Questa opzione può essere definita più volte per più proprietà personalizzate. </p> </td> 
  </tr> 
 </tbody> 
</table>

