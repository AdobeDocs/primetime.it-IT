---
seo-title: Proprietà del file di configurazione
title: Proprietà del file di configurazione
uuid: aec5fee7-4d77-4299-8d85-3e9042b2bbd1
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '1121'
ht-degree: 0%

---


# Proprietà del file di configurazione {#configuration-file-properties}

Il file di configurazione specifica le seguenti proprietà. Per i nomi di proprietà che includono `n`, `n` rappresenta un numero intero che inizia con 1 e aumenta per ogni istanza della proprietà.

<table class="+ topic/table " id="table_p3x_54y_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> Opzione riga di comando/proprietà </th> 
   <th colname="2" class="- topic/entry entry"> Descrizione </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.name</span> <p class="- topic/p "><span class="codeph"> -n</span> nome <i class="+ topic/ph hi-d/i ">criterio</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Il nome di una politica leggibile dall'uomo. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.requestKeyServer</span> <p class="- topic/p "><span class="codeph"> -keyServer</span> <i class="+ topic/ph hi-d/i ">booleano</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Se true, per la distribuzione delle chiavi a iOS è necessario un server di chiavi HTTPS. Se non viene specificato, il valore predefinito è false. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.applyJailbreak</span> <p class="- topic/p "><span class="codeph"> -imposizioneJailbreak</span> <i class="+ topic/ph hi-d/i ">booleano</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Se true, per i dispositivi che supportano il rilevamento delle interruzioni di chiamata, non consentire la riproduzione se è stata rilevata un'interruzione di chiamata. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.critical</span> <p class="- topic/p "><span class="codeph"> -critical</span> <i class="+ topic/ph hi-d/i ">boolean</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Imposta la criticità dei criteri. Se true, il server deve comprendere tutte le parti del criterio (si tratta del comportamento predefinito). Se false, il server potrebbe ignorare gli attributi del criterio che non capisce. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chining.asymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry ">Certificato del server delle licenze con chiave pubblica utilizzata per crittografare la chiave di crittografia principale per il concatenamento delle licenze <a href="../../../aaxs-protecting-content/content-introduction/content-usage-rules/content-other-policy-options/content-enhanced-license-chaining.md" format="dita" scope="local"> Enhanced </a>Questa proprietà specifica un file che contiene solo il certificato (il formato PEM o DER è accettabile). </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chining.rootKey</span> <p class="- topic/p "><span class="codeph"> -rootKey</span> <i class="+ topic/ph hi-d/i ">root-key</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Specifica la chiave di crittografia principale per il concatenamento delle licenze avanzato. Se non viene specificata alcuna chiave e l'opzione Concatenamento licenze avanzato è abilitata, verrà generata una chiave casuale. La chiave deve avere una lunghezza di 16 byte e deve essere specificata come valore esadecimale. Lo spazio vuoto tra i valori esadecimali è facoltativo. Per gli aggiornamenti, l'opzione della riga di comando non è consentita e la proprietà viene ignorata. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.url</span> <p class="- topic/p "><span class="codeph"> -domainURL</span> <i class="+ topic/ph hi-d/i ">url</i> </p> </td> 
   <td colname="2" class="- topic/entry "> URL del server di dominio, se è richiesta la registrazione del dominio. Per gli aggiornamenti, l'opzione della riga di comando non è consentita e la proprietà viene ignorata. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.anonimo</span> <p class="- topic/p "><span class="codeph"> -domainAnon</span> </p> </td> 
   <td colname="2" class="- topic/entry "> Specifica se è consentita la registrazione del dominio anonimo. Impostate la proprietà su true o includete questa opzione della riga di comando per consentire l'accesso anonimo. Questa opzione non può essere utilizzata con -domainAuthNS. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.authNamespace</span> <p class="- topic/p "><span class="codeph"> -domainAuthNS</span> <i class="+ topic/ph hi-d/i ">namespace</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Spazio dei nomi di autenticazione per la registrazione del dominio. Se specificato, il client deve autenticarsi con un nome utente e una password emessi dall'autorità specificata. Per gli aggiornamenti, l'opzione della riga di comando non è consentita e la proprietà viene ignorata. Questa opzione non può essere utilizzata con -domainAnon. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.analog</span> <p class="- topic/p "><span class="codeph"> -opAnalogico</span> <i class="+ topic/ph hi-d/i ">AnalogicoOption</i> </p> </td> 
   <td colname="2" class="- topic/entry ">Limiti di protezione dell'uscita analogica. Sono supportati i seguenti valori: 
    <ul class="- topic/ul " id="ul_h4x_54y_n4"> 
     <li class="- topic/li " id="li_5BC8F39B61894E83A7B27570FF848F09"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> NO_PROTECTION</span> </p> </li> 
     <li class="- topic/li " id="li_FF14594A0714480496793A82C3FA1610"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE</span> </p> </li> 
     <li class="- topic/li " id="li_721FCC4DC1F34AE398EFAE4C0D3F50F5"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_ACP</span> </p> </li> 
     <li class="- topic/li " id="li_D588BB278BEE4CEAB034BD48550EBCDC"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_CGMSA</span> </p> </li> 
     <li class="- topic/li " id="li_7E5F006D2F114502BA6D0A9C4173004E"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> RICHIESTO</span> </p> </li> 
     <li class="- topic/li " id="li_9EBFAA4AACF249C2A94432D88E12C3B9"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> REQUIRED_ACP</span> </p> </li> 
     <li class="- topic/li " id="li_6720C6A085864BEB957C0BF2C38551C9"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> REQUIRED_CGMSA</span> </p> </li> 
     <li class="- topic/li " id="li_6FD98473ECDB4A66AC4B506FB9B3B360"> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> NO_PLAYBACK</span> </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -drmBlacklist</span> <i class="+ topic/ph hi-d/i ">name/value-pair</i> </p> </td> 
   <td colname="2" class="- topic/entry ">Ai client DRM è stato negato l'accesso al contenuto protetto. Questa opzione specifica un elenco di versioni dei moduli DRM che non possono essere utilizzate (elenco dei blocchi). Il valore è costituito da coppie nome=valore separate da virgola con il seguente formato: <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|arch|model|vendor|env|screen=value</span> </p> <p class="- topic/p ">Le coppie nome/valore aggiuntive devono essere separate da virgola. Ad esempio: <span class="codeph"> os=Win,release=2.0,arch=32</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -runtimeBlacklist</span> <i class="+ topic/ph hi-d/i ">name/value-pair</i> </p> </td> 
   <td colname="2" class="- topic/entry ">I runtime dell'applicazione non possono accedere al contenuto protetto. Questa opzione specifica un elenco di versioni di moduli runtime che non possono essere utilizzate (elenco blocchi). Il valore è costituito da coppie nome=valore separate da virgola con il seguente formato: <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|applicazione|arco|modello|fornitore|env|screen=value</span> </p> <p class="- topic/p ">Le coppie nome/valore aggiuntive devono essere separate da virgola. Ad esempio, <span class="codeph"> os=Win,application=AIR</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.v1DeviceCapabilities</span> <p class="- topic/p "><span class="codeph"> -devCapabilitiesV1</span> <i class="+ topic/ph hi-d/i ">name/value-pair</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica le funzionalità dei dispositivi necessarie per accedere al contenuto protetto. Il valore è costituito da coppie nome=valore separate da virgola con il seguente formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> nonUserAccessibleBus|hardwareRootOfTrust=true|false</span> </p> <p class="- topic/p ">Ad esempio, <span class="codeph"> nonUserAccessibleBus=false,hardwareRootOfTrust=true</span>. Durante l'aggiornamento, utilizzare <span class="codeph"> -devCapabilitiesV1</span> senza gli argomenti rimanenti per rimuovere la restrizione delle capacità del dispositivo. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.syncFrequency</span> <p class="- topic/p "><span class="codeph"> -sync</span> <i class="+ topic/ph hi-d/i ">name/value-pair</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specificate la frequenza con cui i client devono inviare i messaggi di sincronizzazione al server. In caso contrario, i client non invieranno messaggi di sincronizzazione durante la riproduzione del contenuto protetto con questo criterio. Il valore è costituito da coppie <span class="codeph"> nome=valore</span> separate da virgola con il seguente formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> start|force|hardStop=numberValue</span> </p> <p class="- topic/p "> 
     <ul id="ul_a5j_q4t_44"> 
      <li id="li_25CAF96C27F34848A95B2E3693847C71"><span class="codeph"> start</span> (obbligatorio) - L'intervallo di avvio specifica che il client deve avviare la sincronizzazione con il server molti minuti dall'ultima sincronizzazione. </li> 
      <li id="li_CC9068CFE75645029C947C9E1B53351F"><span class="codeph"> force</span> (facoltativo) - Forza probabilità di sincronizzazione è la probabilità (0-100) con cui il client deve forzare un messaggio di sincronizzazione durante la riproduzione. </li> 
      <li id="li_C31A6250F19348FBB8B7569D00C6314E"><span class="codeph"> hardStop</span> (facoltativo) - L'intervallo di arresto fisso è il tempo in minuti dopo il quale il client non riesce a riprodurre se non è in grado di eseguire la sincronizzazione. Se impostato, deve essere maggiore dell'intervallo iniziale. </li> 
     </ul>Durante l'aggiornamento, utilizzate <span class="codeph"> -sync</span> senza gli argomenti rimanenti per rimuovere i requisiti di sincronizzazione. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.useRootLicense</span> </td> 
   <td colname="2" class="- topic/entry ">Indica se questo criterio dispone di una licenza radice (vedere Concatenamento <i class="+ topic/ph hi-d/i ">licenze</i> avanzato in <i class="+ topic/ph hi-d/i ">Utilizzo di Adobe Access per la protezione dei contenuti</i>). </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.startDate</span> </td> 
   <td colname="2" class="- topic/entry ">Data dopo la quale il contenuto è valido. Utilizzare il formato <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> (ad esempio, <span class="codeph"> 2009-01-31</span> rappresenta il 31 gennaio alle 12:00 AM) o <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:sec</span> (ad esempio, <span class="codeph"> 2009-01-31-14:300 0:00</span> rappresenta il 31 gennaio alle 14:30). </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expires.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Data prima della quale il contenuto è valido. Non è possibile specificare contemporaneamente <span class="codeph"> policy.expires.endDate</span> e policy.Expending.Duration. Utilizzate il formato <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> o <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:sec</span> (ad esempio, 2009-01-31-14:30:00 rappresenta il 31 gennaio alle 2:30 PM). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expires.Duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Il tempo di validità del contenuto (in minuti), a partire dal momento in cui viene creato il pacchetto. È possibile che <span class="codeph"> policy.Expend.endDate</span> e <span class="codeph"> policy.Expending.Duration</span> non vengano specificate contemporaneamente. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.Duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Il tempo durante il quale una licenza può essere memorizzata nella cache del client (in minuti). Impostare questa proprietà su 0 per impedire il caching delle licenze. Il valore deve essere 0 o superiore. Non è possibile utilizzare contemporaneamente <span class="codeph"> policy.licenseCaching.durata</span> e <span class="codeph"> policy.licenseCaching.endDate</span> . </p> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Nota</b>: Questa impostazione viene applicata solo al caching delle licenze sul disco. Non controlla la durata della licenza memorizzata nella cache. La licenza può essere memorizzata nella cache anche se la durata specificata dal criterio è pari a zero. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Data dopo la quale le licenze non possono essere memorizzate nella cache. Non è possibile utilizzare contemporaneamente <span class="codeph"> policy.licenseCaching.durata</span> e <span class="codeph"> policy.licenseCaching.endDate</span> . </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.anonimo</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica se l'acquisizione anonima della licenza è consentita. Il valore predefinito è "false" (l'autenticazione nome utente/password è obbligatoria) se non viene specificato. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.authNamespace</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se è richiesta l'autenticazione tramite nome utente/password, questa proprietà specifica un qualificatore di nome facoltativo per i nomi utente. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Coppie nome/valore personalizzate che devono essere utilizzate dal server durante l'acquisizione della licenza. Utilizzare il formato seguente per specificare le proprietà: <span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span>=<span class="+ topic/ph pr-d/codeph codeph">name</span>=<span class="+ topic/ph pr-d/codeph codeph">value</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.playWindow</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica la finestra di riproduzione (in minuti), ossia la durata della validità della licenza dopo la prima esecuzione del contenuto protetto. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.digital</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Limiti di protezione dell'output. I valori devono essere uno dei seguenti: </p> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">NO_PROTECTION, USE_IF_AVAILABLE, REQUIRED, NO_PLAYBACK</i> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Per accedere al contenuto protetto, il modulo DRM deve avere il livello di protezione minimo specificato o superiore. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Per accedere al contenuto protetto, il modulo runtime dell'applicazione deve avere il livello di protezione minimo specificato, o superiore. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowAIRApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Un elenco di autorizzazioni per le applicazioni Adobe AIR o iOS consentite per la riproduzione di contenuto protetto. La proprietà deve utilizzare il formato seguente: <span class="+ topic/ph pr-d/codeph codeph">pubId</span>[:<span class="+ topic/ph pr-d/codeph codeph">appId</span>[:[<span class="+ topic/ph pr-d/codeph codeph">min</span>]:[<span class="+ topic/ph pr-d/codeph codeph">max</span>]] </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowSWFApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Elenco di applicazioni SWF consentite per riprodurre contenuto protetto. Utilizzate il formato seguente: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph">URL</span> o file=<span class="+ topic/ph pr-d/codeph codeph">swf_file</span>,time=<i class="+ topic/ph hi-d/i ">max_time_to_verify</i> <i class="+ topic/ph hi-d/i ">swf_file</i> è il file SWF per il quale calcolare l’hash e <i class="+ topic/ph hi-d/i ">max_time_to_verify</i> è il tempo massimo per consentire il download e la verifica del file SWF per il completamento (in secondi). </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Coppie nome/valore personalizzate da includere nelle licenze rilasciate agli utenti. Utilizzate il formato seguente: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n</span>=<span class="+ topic/ph pr-d/codeph codeph">name</span>=<span class="+ topic/ph pr-d/codeph codeph">value</span> </p> <p class="- topic/p ">Questa opzione può essere definita più volte per più proprietà personalizzate. </p> </td> 
  </tr> 
 </tbody> 
</table>

