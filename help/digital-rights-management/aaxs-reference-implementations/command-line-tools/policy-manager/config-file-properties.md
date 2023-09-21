---
title: Proprietà del file di configurazione
description: Proprietà del file di configurazione
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 0%

---

# Proprietà del file di configurazione {#configuration-file-properties}

Il file di configurazione specifica le seguenti proprietà. Per nomi di proprietà che includono `n`, `n` rappresenta un numero intero che inizia con 1 e aumenta per ogni istanza della proprietà.

<table class="+ topic/table " id="table_p3x_54y_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> Proprietà/Opzione della riga di comando </th> 
   <th colname="2" class="- topic/entry entry"> Descrizione </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.name</span> <p class="- topic/p "><span class="codeph"> -n</span> <i class="+ topic/ph hi-d/i ">policyname</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Nome del criterio leggibile dall'utente. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.requireKeyServer</span> <p class="- topic/p "><span class="codeph"> -keyServer</span> <i class="+ topic/ph hi-d/i ">booleano</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Se è true, per la consegna delle chiavi ad iOS è necessario un server chiavi HTTPS. Il valore predefinito è false, se non specificato. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.enforceJailbreak</span> <p class="- topic/p "><span class="codeph"> -enforceJailbreak</span> <i class="+ topic/ph hi-d/i ">booleano</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Se true, per i dispositivi che supportano il rilevamento jailbreak, non consentire la riproduzione se è stato rilevato jailbreak. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.critical</span> <p class="- topic/p "><span class="codeph"> -critico</span> <i class="+ topic/ph hi-d/i ">booleano</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Impostare la criticità dei criteri. Se è true, il server deve comprendere tutte le parti del criterio (questo è il comportamento predefinito). Se false, il server può ignorare gli attributi dei criteri che non comprende. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.asymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry ">Certificato del server di licenze la cui chiave pubblica viene utilizzata per crittografare la chiave di crittografia radice per <a href="../../../aaxs-protecting-content/content-introduction/content-usage-rules/content-other-policy-options/content-enhanced-license-chaining.md" format="dita" scope="local"> Concatenamento licenze migliorato </a>
   Questa proprietà specifica un file che contiene solo il certificato (è possibile utilizzare il formato PEM o DER). </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.rootKey</span> <p class="- topic/p "><span class="codeph"> -rootKey</span> <i class="+ topic/ph hi-d/i ">root-key</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Specificare la chiave di crittografia radice per il concatenamento licenze avanzato. Se non viene specificata alcuna chiave e il Concatenamento licenze avanzato è abilitato, verrà generata una chiave casuale. La chiave deve essere lunga 16 byte e specificata come valori esadecimali. Lo spazio vuoto tra i valori esadecimali è facoltativo. Per gli aggiornamenti, l’opzione della riga di comando non è consentita e la proprietà viene ignorata. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.url</span> <p class="- topic/p "><span class="codeph"> -domainURL</span> <i class="+ topic/ph hi-d/i ">url</i> </p> </td> 
   <td colname="2" class="- topic/entry "> URL del server di dominio, se è richiesta la registrazione del dominio. Per gli aggiornamenti, l’opzione della riga di comando non è consentita e la proprietà viene ignorata. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.anonymous</span> <p class="- topic/p "><span class="codeph"> -domainAnon</span> </p> </td> 
   <td colname="2" class="- topic/entry "> Specifica se è consentita la registrazione anonima del dominio. Impostare la proprietà su true o includere questa opzione della riga di comando per consentire l'accesso anonimo. Impossibile utilizzare questa opzione con -domainAuthNS. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.authNamespace</span> <p class="- topic/p "><span class="codeph"> -domainAuthNS</span> <i class="+ topic/ph hi-d/i ">namespace</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Spazio dei nomi di autenticazione per la registrazione del dominio. Se specificato, il client deve eseguire l'autenticazione con un nome utente e una password emessi dall'autorità specificata. Per gli aggiornamenti, l’opzione della riga di comando non è consentita e la proprietà viene ignorata. Impossibile utilizzare questa opzione con -domainAnon. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.analogico</span> <p class="- topic/p "><span class="codeph"> -opAnalogico</span> <i class="+ topic/ph hi-d/i ">OpzioneAnalogica</i> </p> </td> 
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
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -drmBlacklist</span> <i class="+ topic/ph hi-d/i ">coppie nome/valore</i> </p> </td> 
   <td colname="2" class="- topic/entry ">Ai client DRM non è consentito l'accesso a contenuto protetto. Questa opzione specifica un elenco di versioni dei moduli DRM che non possono essere utilizzate (elenco Bloccati). Il valore è costituito da coppie nome=valore separate da virgola con il seguente formato: <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|arch|model|vendor|env|screen=value</span> </p> <p class="- topic/p ">Le coppie nome/valore aggiuntive devono essere separate da virgole. Ad esempio: <span class="codeph"> os=Win,release=2.0,arch=32</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -runtimeBlacklist</span> <i class="+ topic/ph hi-d/i ">coppie nome/valore</i> </p> </td> 
   <td colname="2" class="- topic/entry ">I runtime dell’applicazione non possono accedere al contenuto protetto. Questa opzione specifica un elenco di versioni dei moduli di runtime che non possono essere utilizzate (elenco Bloccati). Il valore è costituito da coppie nome=valore separate da virgola con il seguente formato: <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|application|arch|model|vendor|env|screen=value</span> </p> <p class="- topic/p ">Le coppie nome/valore aggiuntive devono essere separate da virgole. Ad esempio: <span class="codeph"> os=Win,application=AIR</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.v1DeviceCapabilities</span> <p class="- topic/p "><span class="codeph"> -devCapabilitiesV1</span> <i class="+ topic/ph hi-d/i ">coppie nome/valore</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica le funzionalità del dispositivo necessarie per accedere al contenuto protetto. Il valore è costituito da coppie nome=valore separate da virgola con il seguente formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> nonUserAccessibleBus|hardwareRootOfTrust=true|false</span> </p> <p class="- topic/p ">Ad esempio: <span class="codeph"> nonUserAccessibleBus=false,hardwareRootOfTrust=true</span>. Durante l’aggiornamento, utilizza <span class="codeph"> -devCapabilitiesV1</span> senza gli argomenti rimanenti per rimuovere la restrizione relativa alle funzionalità del dispositivo. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.syncFrequency</span> <p class="- topic/p "><span class="codeph"> -sync</span> <i class="+ topic/ph hi-d/i ">coppie nome/valore</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specificare la frequenza con cui i client devono inviare messaggi di sincronizzazione al server. Se non è impostato, i client non invieranno messaggi di sincronizzazione durante la riproduzione di contenuto protetto con questo criterio. Il valore è costituito da virgole separate <span class="codeph"> name=value</span> coppie con il seguente formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> start|force|hardStop=numberValue</span> </p> <p class="- topic/p "> 
     <ul id="ul_a5j_q4t_44"> 
      <li id="li_25CAF96C27F34848A95B2E3693847C71"><span class="codeph"> inizio</span> (obbligatorio) - Intervallo di avvio specifica che il client deve avviare la sincronizzazione con il server dopo molti minuti dall'ultima sincronizzazione. </li> 
      <li id="li_CC9068CFE75645029C947C9E1B53351F"><span class="codeph"> forzare</span> (facoltativo) - Probabilità di sincronizzazione forzata indica la probabilità (0-100) con cui il client deve forzare un messaggio di sincronizzazione durante la riproduzione. </li> 
      <li id="li_C31A6250F19348FBB8B7569D00C6314E"><span class="codeph"> hardStop</span> (facoltativo) - Intervallo di arresto rigido è il tempo in minuti dopo il quale il client non riesce a riprodurre il contenuto se non è in grado di eseguire la sincronizzazione. Se impostato, deve essere maggiore dell'intervallo di inizio. </li> 
     </ul>Durante l’aggiornamento, utilizza <span class="codeph"> -sync</span> senza gli argomenti rimanenti per rimuovere i requisiti di sincronizzazione. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.useRootLicense</span> </td> 
   <td colname="2" class="- topic/entry ">Indica se il criterio dispone di una licenza radice (vedere <i class="+ topic/ph hi-d/i ">Concatenamento licenze migliorato</i> in <i class="+ topic/ph hi-d/i ">Utilizzo dell’accesso agli Adobi per proteggere i contenuti</i>). </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.startDate</span> </td> 
   <td colname="2" class="- topic/entry ">La data dopo la quale il contenuto è valido. Utilizza il formato <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-gg</span> (ad esempio, <span class="codeph"> 31/01/09</span> rappresenta il 31 gennaio alle 12:00) o <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-gg-h24:min:sec</span> (ad esempio, <span class="codeph"> 2009-01-31-14:30:00</span> 31 gennaio alle 14:30). </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La data prima della quale il contenuto è valido. Entrambi <span class="codeph"> policy.expiration.endDate</span> e policy.expiration.duration non possono essere specificati contemporaneamente. Utilizza il formato <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-gg</span> o <span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-gg-h24:min:sec</span> (ad esempio, 2009-01-31-14:30:00 rappresenta il 31 gennaio alle 14:30). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La quantità di tempo di validità del contenuto (in minuti), a partire dal momento in cui viene inserito nel pacchetto. Entrambi <span class="codeph"> policy.expiration.endDate</span> e <span class="codeph"> policy.expiration.duration</span> non possono essere specificati contemporaneamente. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Quantità di tempo di memorizzazione nella cache di una licenza sul client (in minuti). Impostare questa proprietà su 0 per non consentire il caching delle licenze. Il valore deve essere maggiore o uguale a 0. Entrambi <span class="codeph"> policy.licenseCaching.duration</span> e <span class="codeph"> policy.licenseCaching.endDate</span> non possono essere utilizzati contemporaneamente. </p> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Nota</b>: questa impostazione dei criteri viene applicata solo al caching delle licenze sul disco. Non controlla la durata della licenza memorizzata nella cache. La licenza può essere memorizzata nella cache anche se la durata specificata dal criterio è zero. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Data dopo la quale le licenze non possono essere memorizzate nella cache. Entrambi <span class="codeph"> policy.licenseCaching.duration</span> e <span class="codeph"> policy.licenseCaching.endDate</span> non possono essere utilizzati contemporaneamente. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.anonymous</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica se è consentita l'acquisizione di licenze anonime. Se non viene specificato, il valore predefinito è "false" (è richiesta l’autenticazione nome utente/password). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.authNamespace</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se è richiesta l'autenticazione nome utente/password, questa proprietà specifica un qualificatore di nome facoltativo per i nomi utente. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Coppie nome/valore personalizzate che devono essere utilizzate dal server durante l'acquisizione della licenza. Utilizza il seguente formato per specificare le proprietà: <span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span>=<span class="+ topic/ph pr-d/codeph codeph">nome</span>=<span class="+ topic/ph pr-d/codeph codeph">valore</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.playbackWindow</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica la finestra di riproduzione (in minuti), che è la durata di validità della licenza dopo la prima riproduzione di contenuto protetto. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.digital</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Vincoli di protezione dell'output. I valori devono essere uno dei seguenti: </p> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">NO_PROTECTION, USE_IF_AVAILABLE, OBBLIGATORIO, NO_PLAYBACK</i> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Per accedere ai contenuti protetti, il modulo DRM deve disporre del livello di protezione minimo specificato o di un livello superiore. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Per accedere al contenuto protetto, il modulo runtime dell’applicazione deve disporre del livello minimo di sicurezza specificato o di un livello superiore. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedAIRApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Un elenco consentiti di applicazioni Adobe AIR o iOS che consentono di riprodurre contenuti protetti. La proprietà deve utilizzare il seguente formato: <span class="+ topic/ph pr-d/codeph codeph">pubId</span>[:<span class="+ topic/ph pr-d/codeph codeph">appId</span>[:[<span class="+ topic/ph pr-d/codeph codeph">min</span>]:[<span class="+ topic/ph pr-d/codeph codeph">max</span>]] </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedSWFApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Un elenco consentiti di applicazioni SWF consente di riprodurre contenuto protetto. Utilizza il seguente formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph">URL</span> o file=<span class="+ topic/ph pr-d/codeph codeph">file_swf</span>,ora=<i class="+ topic/ph hi-d/i ">max_time_to_verify</i> <i class="+ topic/ph hi-d/i ">file_swf</i> è il file SWF per il quale calcolare l’hash e <i class="+ topic/ph hi-d/i ">max_time_to_verify</i> è il tempo massimo per consentire il download e la verifica del SWF (in secondi). </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Coppie nome/valore personalizzate da includere nelle licenze rilasciate agli utenti. Utilizza il seguente formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n</span>=<span class="+ topic/ph pr-d/codeph codeph">nome</span>=<span class="+ topic/ph pr-d/codeph codeph">valore</span> </p> <p class="- topic/p ">Questa opzione può essere definita più volte per più proprietà personalizzate. </p> </td> 
  </tr> 
 </tbody> 
</table>
