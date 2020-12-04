---
description: 'null'
keywords: hard stop
seo-description: 'null'
seo-title: Proprietà di configurazione
title: Proprietà di configurazione
uuid: 216921d1-a9c1-4650-9dce-c025836986e5
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '1218'
ht-degree: 0%

---


# Proprietà di configurazione {#configuration-properties}

<!--<a id="section_20A96CDCC5C340DEAF455C6E300E5712"></a>-->

>[!NOTE]
>
>Per i nomi di proprietà che includono `.n`, il `n` rappresenta un numero intero che inizia con 1 e aumenta per ogni istanza della proprietà. Ad esempio: `policy.license.customProp.n`.

<table class="+ topic/table " id="table_p3x_54y_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> Opzione riga di comando/proprietà </th> 
   <th colname="2" class="- topic/entry entry"> Descrizione </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.name</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">npolicyname</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Il nome della politica DRM leggibile dall'utente. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.requestKeyServer</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">keyServerboolean</i> </p> </td> 
   <td colname="2" class="- topic/entry ">Si applicano le seguenti condizioni: 
    <ul id="ul_AF4EBD6C19DC4DFAAB4756EF24BAC57D"> 
     <li id="li_6CC48ABF78EC426E9FC51458BD946BC9">Se true, per la distribuzione delle chiavi a iOS è necessario un server di chiavi HTTPS. </li> 
     <li id="li_63046A4ED7354C1E9E823B475E4AEFF7">Se non viene specificato, il valore predefinito è false. </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.applyJailbreak</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">applyJailbreakboolean</i> </p> </td> 
   <td colname="2" class="- topic/entry "> Per i dispositivi che supportano il rilevamento dell'interruzione di chiamata, se true, non consentire la riproduzione quando viene rilevata l'interruzione di chiamata. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.critical</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">criticalBoolean</i> </p> </td> 
   <td colname="2" class="- topic/entry ">Imposta la criticità del criterio DRM: 
    <ul id="ul_63F1994798894233A67AC4F8220AB642"> 
     <li id="li_D05DD9AD70464D6B9DB9DFF95846E589">Se true, il server deve comprendere tutte le parti del criterio DRM, che rappresenta il comportamento predefinito. </li> 
     <li id="li_0211473DAF1F426787CC4A68F47643C6">Se false, il server può ignorare gli attributi del criterio DRM che non riconosce. </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chining.asymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry ">Certificato del server delle licenze con chiave pubblica utilizzata per crittografare la chiave di crittografia principale per il sistema di concatenamento delle licenze <a href="https://help.adobe.com/en_US/primetime/drm/5.3/protecting_content/index.html#DRM-concept-Enhanced_License_Chaining" class="- topic/xref " format="http" scope="external"> Enhanced</a>. Questa proprietà specifica un file che include solo il certificato. <p>Nota:  Sono supportati entrambi i formati PEM o DER. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chining.rootKey</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">rootKeyroot-key</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>Specifica la chiave di crittografia principale per la <a href="https://help.adobe.com/en_US/primetime/drm/5.3/protecting_content/index.html#DRM-concept-Enhanced_License_Chaining" class="- topic/xref " format="http" scope="external"> Concatenamento licenze avanzato</a>. Se non viene specificata alcuna chiave e l'opzione Concatenamento licenze avanzato è abilitata, viene generata automaticamente una chiave casuale. </p> <p>La chiave deve essere lunga 16 byte e specificata come valori esadecimali. Lo spazio vuoto tra i valori esadecimali è facoltativo. Per gli aggiornamenti, l'opzione della riga di comando non è disponibile e la proprietà viene ignorata. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.url</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">domainURLurl</i> </p> </td> 
   <td colname="2" class="- topic/entry ">Se è richiesta la registrazione del dominio, <i>url</i> specifica l'URL di un server di dominio. Per gli aggiornamenti, l'opzione della riga di comando non è disponibile e la proprietà viene ignorata. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.anonimo</span> <p class="- topic/p "><span class="codeph"> -domainAnon</span> </p> </td> 
   <td colname="2" class="- topic/entry ">Specifica se è consentita la registrazione del dominio anonimo. Imposta la proprietà su true o include questa opzione della riga di comando per consentire l'accesso anonimo. <p>Nota: Questa opzione non può essere utilizzata con <span class="codeph"> -domainAuthNS</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.authNamespace</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">domainAuthNSnamespace</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>Spazio dei nomi di autenticazione per la registrazione del dominio. Se specificato, il client deve autenticarsi con un nome utente e una password emessi dall'autorità specificata. </p> <p>Per gli aggiornamenti, l'opzione della riga di comando non è disponibile e la proprietà viene ignorata. </p> <p>Nota: Questa opzione non può essere utilizzata con <span class="codeph"> -domainAnon</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.analog</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">opAnalogicoOpzione</i> </p> </td> 
   <td colname="2" class="- topic/entry ">Sono supportati i vincoli di protezione dell'uscita analogica e i seguenti valori: 
    <ul class="- topic/ul " id="ul_h4x_54y_n4"> 
     <li class="- topic/li " id="li_F920EC01159C4231AFBE579D487C8770"><span class="+ topic/ph pr-d/codeph codeph"> NO_PROTECTION</span> </li> 
     <li class="- topic/li " id="li_2DE0494AF8C446EB9E4567915F5E97C3"><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE</span> </li> 
     <li class="- topic/li " id="li_207D2D6256D6423FBDABA7A8627A9B7D"><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_ACP</span> </li> 
     <li class="- topic/li " id="li_E17D944BED5F403FAE94708EE6AE4BBE"><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_CGMSA</span> </li> 
     <li class="- topic/li " id="li_66D5A0C8FE154445A522D91EFB05B7ED"><span class="+ topic/ph pr-d/codeph codeph"> RICHIESTO</span> </li> 
     <li class="- topic/li " id="li_AF2024F212A249ED99AEECCF3E844A11"><span class="+ topic/ph pr-d/codeph codeph"> REQUIRED_ACP</span> </li> 
     <li class="- topic/li " id="li_FFF9B7DAE77740EE895EC35D1606A527"><span class="+ topic/ph pr-d/codeph codeph"> REQUIRED_CGMSA</span> </li> 
     <li class="- topic/li " id="li_52DED572F3AE495EB6A6450C611B440E"><span class="+ topic/ph pr-d/codeph codeph"> NO_PLAYBACK</span> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">drmBlacklistname/value-pair</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>Client DRM con restrizioni all'accesso al contenuto protetto. Questa opzione specifica un elenco di versioni dei moduli DRM che non possono essere utilizzate ( elenco Bloccati). </p> <p>Il valore è costituito da coppie <span class="codeph"> name=value</span> separate da virgola nel seguente formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|arch|model|vendor|env|screen=value</span> </p> <p class="- topic/p ">Le coppie nome/valore aggiuntive devono essere separate da virgola. Ad esempio, <span class="codeph"> os=Win,release=2.0,arch=32</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">runtimeBlacklsitname/value-pair</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>I runtime dell'applicazione non possono accedere al contenuto protetto. Questa opzione specifica un elenco di versioni di moduli runtime che non possono essere utilizzate ( elenco Bloccati). </p> <p>Il valore è costituito da coppie <span class="codeph"> name=value</span> separate da virgola nel seguente formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|applicazione|arco|modello|fornitore|env|screen=value</span> </p> <p class="- topic/p ">Le coppie nome/valore aggiuntive devono essere separate da virgola. Ad esempio, <span class="codeph"> os=Win,application=AIR</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.v1DeviceCapabilities</span> <p class="- topic/p "><span class="codeph"> -devCapabilitiesV1</span> <i class="+ topic/ph hi-d/i ">name/value-pair</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica le funzionalità del dispositivo necessarie per accedere al contenuto protetto. Il valore è costituito da coppie <span class="codeph"> name=value</span> separate da virgola nel seguente formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> nonUserAccessibleBus|hardwareRootOfTrust=true|false</span> </p> <p class="- topic/p ">Ad esempio, <span class="codeph"> nonUserAccessibleBus=false,hardwareRootOfTrust=true</span>. </p> <p>Durante un aggiornamento, è necessario applicare <span class="codeph"> -devCapabilitiesV1</span> senza gli argomenti rimanenti che rimuovono la restrizione delle capacità del dispositivo. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.syncFrequency</span> <p class="- topic/p "><span class="codeph"> -</span> <i class="+ topic/ph hi-d/i ">syncname/value-pair</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica la frequenza con cui i client devono inviare messaggi di sincronizzazione al server. </p> <p>Se la proprietà non è impostata, i client non invieranno messaggi di sincronizzazione quando riproducono contenuto protetto tramite un criterio DRM. Il valore è costituito da coppie <span class="codeph"> name=value</span> separate da virgola nel seguente formato: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> start|force=numberValue</span> </p> <p class="- topic/p ">L'elenco seguente contiene ulteriori informazioni sulle opzioni: 
     <ul id="ul_a5j_q4t_44"> 
      <li id="li_FD2C0C6DA19E455AA1917A56E09A7F84">(obbligatorio) <span class="codeph"> start</span> specifica che il client deve avviare la sincronizzazione con il server nei minuti specificati dall'ultima sincronizzazione. </li> 
      <li id="li_9DEBC57385A442C3929AE3D0E3FA8992">(facoltativo) <span class="codeph"> force</span> è la probabilità (0-100) con cui il client deve forzare un messaggio di sincronizzazione durante la riproduzione. </li> 
     </ul>Durante l'aggiornamento, utilizzate <span class="codeph"> -sync</span> senza gli argomenti rimanenti per rimuovere i requisiti di sincronizzazione. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.useRootLicense</span> </td> 
   <td colname="2" class="- topic/entry ">Indica se il criterio DRM dispone di una licenza radice. <p>Per ulteriori informazioni, vedere <a href="https://help.adobe.com/en_US/primetime/drm/5.3/protecting_content/index.html#DRM-concept-Enhanced_License_Chaining" class="- topic/xref " format="http" scope="external"> Concatenamento delle licenze avanzato</a>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.startDate</span> </td> 
   <td colname="2" class="- topic/entry ">Data dopo la quale il contenuto diventa valido. È possibile applicare uno dei seguenti formati: 
    <ul id="ul_6610B44D0C16485098F6F45DE3F151D7"> 
     <li id="li_986707D4C6164C44B3CCBE2EEB4C09B6"><span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-gg</span> <p>Ad esempio, <span class="codeph"> 2009-01-31</span> indica il 31 gennaio alle 12:00. </p> </li> 
     <li id="li_E15B782716124F6EAEFB04D16E5280DB"><span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-gg-h24:min:sec</span> <p>Ad esempio, <span class="codeph"> 2009-01-31-14:30:00</span> indica il 31 gennaio alle 2:30 PM. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expires.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La data prima che il contenuto diventi non valido. </p> <p>Nota: Non è possibile specificare <span class="codeph"> policy.Expend.endDate</span> e <span class="codeph"> policy.expires.Duration</span> contemporaneamente. </p> <p>Ad esempio, 2009-01-31-14:30:00 significa che il contenuto scade il 31 gennaio alle 2:30 PM. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expires.Duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Tempo in minuti in cui il contenuto diventa non valido. L'ora inizia quando si crea il pacchetto del contenuto. </p> <p>Nota: Non è possibile specificare <span class="codeph"> policy.Expend.endDate</span> e <span class="codeph"> policy.expires.Duration</span> contemporaneamente. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.Duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">L'ora in minuti in cui una licenza può essere memorizzata nella cache del client. È possibile impostare questa proprietà su 0 per impedire il caching delle licenze. Il valore deve essere 0 o superiore. </p> <p>Nota: Non è possibile specificare contemporaneamente <span class="codeph"> policy.licenseCaching.durata</span> e <span class="codeph"> policy.licenseCaching.endDate</span>. </p> <p class="- topic/p ">Questa impostazione del criterio DRM viene applicata solo al caching delle licenze sul disco e non controlla la durata della licenza memorizzata nella cache della memoria. La licenza può essere memorizzata nella cache anche se non si specifica un criterio DRM con una durata pari a zero. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Data dopo la quale non è più possibile memorizzare le licenze nella cache. </p> <p>Nota: Non è possibile specificare contemporaneamente <span class="codeph"> policy.licenseCaching.durata</span> e <span class="codeph"> policy.licenseCaching.endDate</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.anonimo</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica se l'acquisizione anonima della licenza è consentita. Il valore predefinito è impostato su <span class="codeph"> false</span>, il che significa che è richiesto un nome utente e una password. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.authNamespace</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se sono richiesti nome utente e password, questa proprietà specifica un qualificatore di nome facoltativo per i nomi utente. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Coppie nome/valore personalizzate che devono essere utilizzate dal server durante l'acquisizione della licenza. È possibile applicare il formato seguente per specificare le proprietà: <span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span>=<span class="+ topic/ph pr-d/codeph codeph">name</span>=<span class="+ topic/ph pr-d/codeph codeph">value</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.playWindow  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica la finestra di riproduzione in minuti. Questo valore rappresenta la durata della licenza dopo la prima riproduzione del contenuto protetto. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.digital</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Limiti di protezione dell'output, che devono essere uno dei seguenti valori: 
     <ul id="ul_wsb_kfp_fs"> 
      <li id="li_FE012306F22F4F3FB981FE167C7A8B94"><span class="codeph"> NO_PROTECTION</span> </li> 
      <li id="li_A5591DC8983848FE9823C2A261BF7713"><span class="codeph"> USE_IF_AVAILABLE</span> </li> 
      <li id="li_74102C36ADE841C4B9ED71156E0A4C2C"><span class="codeph"> RICHIESTO</span> </li> 
      <li id="li_769E15C85B4E4DD48213DBD019D60BA7"><span class="codeph"> NO_PLAYBACK</span> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.ota</span> </td> 
   <td colname="2" class="- topic/entry ">Specifica i tipi di connessione sopra l'aria (OTA) che devono essere consentiti nell'elenco. I tipi di connessione validi includono: 
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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Il modulo runtime dell'applicazione deve avere almeno il livello minimo di protezione specificato per accedere al contenuto protetto. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowAIRApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Un elenco consentiti  di applicazioni non Flash ( Adobe AIR, iOS, Android, ecc.) che possono riprodurre contenuto protetto. La proprietà deve utilizzare il formato seguente: <span class="+ topic/ph pr-d/codeph codeph">pubId</span>[:<span class="+ topic/ph pr-d/codeph codeph">appId</span>[:[<span class="+ topic/ph pr-d/codeph codeph">min</span>]:[<span class="+ topic/ph pr-d/codeph codeph">max</span>]] </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowSWFApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Un elenco consentiti  di applicazioni SWF consentite per la riproduzione di contenuto protetto. La proprietà deve utilizzare il formato seguente: </p> <p class="- topic/p "> 
     <ul id="ul_EC20F52AD95C4BE3B7F703048A43CDF0"> 
      <li id="li_3E4A47D925C24834A2C25BC5943279D4"><span class="+ topic/ph pr-d/codeph codeph">URL</span> </li> 
      <li id="li_9A7CAF081C5F488FB5CDA6D38C5552F6"><span class="+ topic/ph pr-d/codeph codeph">file=swf_file</span> </li> 
      <li id="li_E10EA4223137489CBE4015DE999F7154"><span class="codeph">time=max_time_to_verify</span> </li> 
     </ul> <i class="+ topic/ph hi-d/i ">swf_</i> file è il file SWF utilizzato per calcolare l'hash;  <i class="+ topic/ph hi-d/i ">max_time_to_</i> verifyè il tempo massimo in secondi consentito per scaricare e verificare il completamento del file SWF. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Coppie nome/valore personalizzate che è necessario includere nelle licenze al momento dell'emissione delle licenze agli utenti. È necessario specificare il formato seguente: </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n=name</span> </p> <p class="- topic/p ">Potete definire questa opzione più volte per più proprietà personalizzate. </p> </td> 
  </tr> 
 </tbody> 
</table>
