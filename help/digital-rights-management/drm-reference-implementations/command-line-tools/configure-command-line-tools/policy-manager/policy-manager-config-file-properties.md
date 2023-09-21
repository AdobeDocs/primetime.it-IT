---
keywords: arresto rigido
title: Proprietà di configurazione
description: Proprietà di configurazione
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1217'
ht-degree: 0%

---

# Proprietà di configurazione {#configuration-properties}

<!--<a id="section_20A96CDCC5C340DEAF455C6E300E5712"></a>-->

>[!NOTE]
>
>Per nomi di proprietà che includono `.n`, il `n` rappresenta un numero intero che inizia con 1 e aumenta per ogni istanza della proprietà. Ad esempio: `policy.license.customProp.n`.

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
   <td colname="2" class="- topic/entry "> Nome del criterio DRM leggibile dall'utente. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.requireKeyServer</span> <p class="- topic/p "><span class="codeph"> -keyServer</span> <i class="+ topic/ph hi-d/i ">booleano</i> </p> </td> 
   <td colname="2" class="- topic/entry ">Si applicano le seguenti condizioni: 
    <ul id="ul_AF4EBD6C19DC4DFAAB4756EF24BAC57D"> 
     <li id="li_6CC48ABF78EC426E9FC51458BD946BC9">Se è true, per la consegna delle chiavi ad iOS è necessario un server chiavi HTTPS. </li> 
     <li id="li_63046A4ED7354C1E9E823B475E4AEFF7">Se non viene specificato, il valore predefinito è false. </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.enforceJailbreak</span> <p class="- topic/p "><span class="codeph"> -enforceJailbreak</span> <i class="+ topic/ph hi-d/i ">booleano</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Per i dispositivi che supportano il rilevamento jailbreak, se true, non consentire la riproduzione quando viene rilevato jailbreak. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.critical</span> <p class="- topic/p "><span class="codeph"> -critico</span> <i class="+ topic/ph hi-d/i ">booleano</i> </p> </td> 
   <td colname="2" class="- topic/entry ">Definisce la criticità della politica DRM: 
    <ul id="ul_63F1994798894233A67AC4F8220AB642"> 
     <li id="li_D05DD9AD70464D6B9DB9DFF95846E589">Se true, il server deve comprendere tutte le parti del criterio DRM, che rappresenta il comportamento predefinito. </li> 
     <li id="li_0211473DAF1F426787CC4A68F47643C6">Se false, il server può ignorare gli attributi dei criteri DRM non riconosciuti. </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.asymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry ">Certificato del server di licenze la cui chiave pubblica viene utilizzata per crittografare la chiave di crittografia radice per <a href="https://help.adobe.com/en_US/primetime/drm/5.3/protecting_content/index.html#DRM-concept-Enhanced_License_Chaining" class="- topic/xref " format="http" scope="external"> Concatenamento licenze migliorato</a>. Questa proprietà specifica un file che include solo il certificato. <p>Nota: sono supportati entrambi i formati PEM o DER. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.rootKey</span> <p class="- topic/p "><span class="codeph"> -rootKey</span> <i class="+ topic/ph hi-d/i ">root-key</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>Specifica la chiave di crittografia radice per <a href="https://help.adobe.com/en_US/primetime/drm/5.3/protecting_content/index.html#DRM-concept-Enhanced_License_Chaining" class="- topic/xref " format="http" scope="external"> Concatenamento licenze migliorato</a>. Se non viene specificata alcuna chiave e il Concatenamento licenze avanzato è abilitato, viene automaticamente generata una chiave casuale. </p> <p>La chiave deve essere lunga 16 byte e specificata come valori esadecimali. Lo spazio vuoto tra i valori esadecimali è facoltativo. Per gli aggiornamenti, l’opzione della riga di comando non è disponibile e la proprietà viene ignorata. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.url</span> <p class="- topic/p "><span class="codeph"> -domainURL</span> <i class="+ topic/ph hi-d/i ">url</i> </p> </td> 
   <td colname="2" class="- topic/entry ">Se è richiesta la registrazione del dominio, <i>url</i> specifica l'URL di un server di dominio. Per gli aggiornamenti, l’opzione della riga di comando non è disponibile e la proprietà viene ignorata. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.anonymous</span> <p class="- topic/p "><span class="codeph"> -domainAnon</span> </p> </td> 
   <td colname="2" class="- topic/entry ">Specifica se è consentita la registrazione anonima del dominio. Imposta la proprietà su true o include questa opzione della riga di comando per consentire l'accesso anonimo. <p>Nota: questa opzione non può essere utilizzata con <span class="codeph"> -domainAuthNS</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.authNamespace</span> <p class="- topic/p "><span class="codeph"> -domainAuthNS</span> <i class="+ topic/ph hi-d/i ">namespace</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>Spazio dei nomi di autenticazione per la registrazione del dominio. Se specificato, il client deve eseguire l'autenticazione con un nome utente e una password emessi dall'autorità specificata. </p> <p>Per gli aggiornamenti, l’opzione della riga di comando non è disponibile e la proprietà viene ignorata. </p> <p>Nota: questa opzione non può essere utilizzata con <span class="codeph"> -domainAnon</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.analogico</span> <p class="- topic/p "><span class="codeph"> -opAnalogico</span> <i class="+ topic/ph hi-d/i ">OpzioneAnalogica</i> </p> </td> 
   <td colname="2" class="- topic/entry ">Vincoli di protezione dell'output analogico e sono supportati i seguenti valori: 
    <ul class="- topic/ul " id="ul_h4x_54y_n4"> 
     <li class="- topic/li " id="li_F920EC01159C4231AFBE579D487C8770"><span class="+ topic/ph pr-d/codeph codeph"> NO_PROTECTION</span> </li> 
     <li class="- topic/li " id="li_2DE0494AF8C446EB9E4567915F5E97C3"><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE</span> </li> 
     <li class="- topic/li " id="li_207D2D6256D6423FBDABA7A8627A9B7D"><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_ACP</span> </li> 
     <li class="- topic/li " id="li_E17D944BED5F403FAE94708EE6AE4BBE"><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_CGMSA</span> </li> 
     <li class="- topic/li " id="li_66D5A0C8FE154445A522D91EFB05B7ED"><span class="+ topic/ph pr-d/codeph codeph"> OBBLIGATORIO</span> </li> 
     <li class="- topic/li " id="li_AF2024F212A249ED99AEECCF3E844A11"><span class="+ topic/ph pr-d/codeph codeph"> REQUIRED_ACP</span> </li> 
     <li class="- topic/li " id="li_FFF9B7DAE77740EE895EC35D1606A527"><span class="+ topic/ph pr-d/codeph codeph"> REQUIRED_CGMSA</span> </li> 
     <li class="- topic/li " id="li_52DED572F3AE495EB6A6450C611B440E"><span class="+ topic/ph pr-d/codeph codeph"> NO_PLAYBACK</span> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -drmBlacklist</span> <i class="+ topic/ph hi-d/i ">coppie nome/valore</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>I client DRM a cui è limitato l'accesso ai contenuti protetti. Questa opzione specifica un elenco di versioni dei moduli DRM che non possono essere utilizzate (elenco Bloccati). </p> <p>Il valore è costituito da virgole separate <span class="codeph"> name=value</span> coppie nel formato seguente: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|arch|model|vendor|env|screen=value</span> </p> <p class="- topic/p ">Le coppie nome/valore aggiuntive devono essere separate da virgole. Ad esempio: <span class="codeph"> os=Win,release=2.0,arch=32</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -runtimeBlacklist</span> <i class="+ topic/ph hi-d/i ">coppie nome/valore</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>Ai runtime dell’applicazione viene impedito l’accesso a contenuti protetti. Questa opzione specifica un elenco di versioni dei moduli di runtime che non possono essere utilizzate (elenco Bloccati). </p> <p>Il valore è separato da virgole <span class="codeph"> name=value</span> coppie nel formato seguente: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|application|arch|model|vendor|env|screen=value</span> </p> <p class="- topic/p ">Le coppie nome/valore aggiuntive devono essere separate da virgole. Ad esempio: <span class="codeph"> os=Win,application=AIR</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.v1DeviceCapabilities</span> <p class="- topic/p "><span class="codeph"> -devCapabilitiesV1</span> <i class="+ topic/ph hi-d/i ">coppie nome/valore</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica le funzionalità del dispositivo necessarie per accedere al contenuto protetto. Il valore è costituito da virgole separate <span class="codeph"> name=value</span> coppie nel formato seguente: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> nonUserAccessibleBus|hardwareRootOfTrust=true|false</span> </p> <p class="- topic/p ">Ad esempio: <span class="codeph"> nonUserAccessibleBus=false,hardwareRootOfTrust=true</span>. </p> <p>Durante un aggiornamento, devi applicare <span class="codeph"> -devCapabilitiesV1</span> senza gli argomenti rimanenti che rimuovono la restrizione relativa alle funzionalità del dispositivo. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.syncFrequency</span> <p class="- topic/p "><span class="codeph"> -sync</span> <i class="+ topic/ph hi-d/i ">coppie nome/valore</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica la frequenza con cui i client devono inviare messaggi di sincronizzazione al server. </p> <p>Se la proprietà non è impostata, i client non invieranno messaggi di sincronizzazione quando riproducono contenuti protetti con un criterio DRM. Il valore è separato da virgole <span class="codeph"> name=value</span> coppie nel formato seguente: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> start|force=numberValue</span> </p> <p class="- topic/p ">L'elenco seguente fornisce informazioni aggiuntive sulle opzioni: 
     <ul id="ul_a5j_q4t_44"> 
      <li id="li_FD2C0C6DA19E455AA1917A56E09A7F84">(obbligatorio) <span class="codeph"> inizio</span> specifica che il client deve avviare la sincronizzazione con il server nei minuti specificati dall'ultima sincronizzazione. </li> 
      <li id="li_9DEBC57385A442C3929AE3D0E3FA8992">(facoltativo) <span class="codeph"> forzare</span> è la probabilità (0-100) con cui il client deve forzare un messaggio di sincronizzazione durante la riproduzione. </li> 
     </ul>Durante l’aggiornamento, utilizza <span class="codeph"> -sync</span> senza gli argomenti rimanenti per rimuovere i requisiti di sincronizzazione. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.useRootLicense</span> </td> 
   <td colname="2" class="- topic/entry ">Indica se il criterio DRM dispone di una licenza radice. <p>Per ulteriori informazioni, consulta <a href="https://help.adobe.com/en_US/primetime/drm/5.3/protecting_content/index.html#DRM-concept-Enhanced_License_Chaining" class="- topic/xref " format="http" scope="external"> Concatenamento licenze migliorato</a>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.startDate</span> </td> 
   <td colname="2" class="- topic/entry ">Data dopo la quale il contenuto diventa valido. È possibile applicare uno dei seguenti formati: 
    <ul id="ul_6610B44D0C16485098F6F45DE3F151D7"> 
     <li id="li_986707D4C6164C44B3CCBE2EEB4C09B6"><span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-gg</span> <p>Ad esempio: <span class="codeph"> 31/01/09</span> significa 31 gennaio alle 00:00. </p> </li> 
     <li id="li_E15B782716124F6EAEFB04D16E5280DB"><span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-gg-h24:min:sec</span> <p>Ad esempio: <span class="codeph"> 2009-01-31-14:30:00</span> significa 31 gennaio alle 2:30. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La data prima della scadenza del contenuto. </p> <p>Nota: non è possibile specificare <span class="codeph"> policy.expiration.endDate</span> e <span class="codeph"> policy.expiration.duration</span> contemporaneamente. </p> <p>Ad esempio, 2009-01-31-14:30:00 significa che il contenuto scadrà il 31 gennaio alle 14:30. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Il tempo in minuti in cui il contenuto non è più valido. L’ora inizia quando crei un pacchetto di contenuto. </p> <p>Nota: non è possibile specificare <span class="codeph"> policy.expiration.endDate</span> e <span class="codeph"> policy.expiration.duration</span> contemporaneamente. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">L’ora in minuti in cui è possibile memorizzare una licenza nella cache del client. È possibile impostare questa proprietà su 0 per impedire il caching delle licenze. Il valore deve essere maggiore o uguale a 0. </p> <p>Nota: non è possibile specificare <span class="codeph"> policy.licenseCaching.duration</span> e <span class="codeph"> policy.licenseCaching.endDate</span> contemporaneamente. </p> <p class="- topic/p ">Questa impostazione dei criteri DRM viene applicata solo al caching delle licenze sul disco e non controlla la durata delle licenze memorizzate nella cache. La licenza può essere memorizzata nella cache anche se non si specifica un criterio DRM con durata pari a zero. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Data dopo la quale non è più possibile memorizzare nella cache le licenze. </p> <p>Nota: non è possibile specificare <span class="codeph"> policy.licenseCaching.duration</span> e <span class="codeph"> policy.licenseCaching.endDate</span> contemporaneamente. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.anonymous</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica se è consentita l'acquisizione di licenze anonime. Il valore predefinito è impostato su <span class="codeph"> false</span>, il che significa che sono necessari un nome utente e una password. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.authNamespace</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se sono necessari un nome utente e una password, questa proprietà specifica un qualificatore di nome facoltativo per i nomi utente. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Coppie nome/valore personalizzate che devono essere utilizzate dal server durante l'acquisizione della licenza. Per specificare le proprietà, potete applicare il seguente formato: <span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span>=<span class="+ topic/ph pr-d/codeph codeph">nome</span>=<span class="+ topic/ph pr-d/codeph codeph">valore</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.playbackWindow </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica la finestra di riproduzione in minuti. Questo valore rappresenta il periodo di validità della licenza dopo la prima riproduzione del contenuto protetto. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.digital</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Vincoli di protezione dell'output, che devono essere uno dei seguenti valori: 
     <ul id="ul_wsb_kfp_fs"> 
      <li id="li_FE012306F22F4F3FB981FE167C7A8B94"><span class="codeph"> NO_PROTECTION</span> </li> 
      <li id="li_A5591DC8983848FE9823C2A261BF7713"><span class="codeph"> USE_IF_AVAILABLE</span> </li> 
      <li id="li_74102C36ADE841C4B9ED71156E0A4C2C"><span class="codeph"> OBBLIGATORIO</span> </li> 
      <li id="li_769E15C85B4E4DD48213DBD019D60BA7"><span class="codeph"> NO_PLAYBACK</span> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.ota</span> </td> 
   <td colname="2" class="- topic/entry ">Specifica i tipi di connessione over the air (OTA) che devono essere elencati nell'elenco Consentiti. I tipi di connessione validi includono: 
    <ul id="ul_iz5_4fp_fs"> 
     <li id="li_FB07519EFEFE4B95B3B1F5BFD4DE6591"><span class="codeph"> MIRACAST</span> </li> 
     <li id="li_51E7DE83679F4630B01264407DAD0E84"><span class="codeph"> AIRPLAY</span> </li> 
     <li id="li_D499A0487AAC409CB2CEA6164265D3CF"><span class="codeph"> DLNA</span> </li> 
     <li id="li_4FCC0EC4A0FC48F99A13EC8A1B78D6A1"><span class="codeph"> WIDI</span> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.resolution</span> </td> 
   <td colname="2" class="- topic/entry "> Specifica il file di configurazione in cui vengono definiti i vincoli basati sulla risoluzione. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica il livello di protezione minimo per consentire al modulo DRM di accedere al contenuto protetto. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Per accedere al contenuto protetto, il modulo runtime dell’applicazione deve avere almeno il livello di sicurezza minimo specificato. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedAIRApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Un elenco consentiti di applicazioni non di Flash (Adobe AIR, iOS, Android, ecc.) che possono riprodurre contenuti protetti. La proprietà deve utilizzare il seguente formato: <span class="+ topic/ph pr-d/codeph codeph">pubId</span>[:<span class="+ topic/ph pr-d/codeph codeph">appId</span>[:[<span class="+ topic/ph pr-d/codeph codeph">min</span>]:[<span class="+ topic/ph pr-d/codeph codeph">max</span>]] </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedSWFApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Un elenco consentiti di applicazioni SWF che possono riprodurre contenuti protetti. La proprietà deve utilizzare il seguente formato: </p> <p class="- topic/p "> 
     <ul id="ul_EC20F52AD95C4BE3B7F703048A43CDF0"> 
      <li id="li_3E4A47D925C24834A2C25BC5943279D4"><span class="+ topic/ph pr-d/codeph codeph">URL</span> </li> 
      <li id="li_9A7CAF081C5F488FB5CDA6D38C5552F6"><span class="+ topic/ph pr-d/codeph codeph">file=swf_file</span> </li> 
      <li id="li_E10EA4223137489CBE4015DE999F7154"><span class="codeph">time=max_time_to_verify</span> </li> 
     </ul> <i class="+ topic/ph hi-d/i ">file_swf</i> è il file SWF utilizzato per calcolare l’hash, e <i class="+ topic/ph hi-d/i ">max_time_to_verify</i> è il tempo massimo in secondi consentito per scaricare e verificare il completamento del SWF. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Coppie nome/valore personalizzate che è necessario includere nelle licenze quando le licenze vengono rilasciate agli utenti. È necessario specificare il seguente formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n=name</span> </p> <p class="- topic/p ">Puoi definire questa opzione più volte per più proprietà personalizzate. </p> </td> 
  </tr> 
 </tbody> 
</table>
