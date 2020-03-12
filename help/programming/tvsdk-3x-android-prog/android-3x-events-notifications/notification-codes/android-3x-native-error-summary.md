---
seo-title: Dettagli per la notifica NATIVE_ERROR
title: Dettagli per la notifica NATIVE_ERROR
uuid: d16ef930-d1f4-4984-be6e-1cf4993ab71d
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Dettagli per la notifica NATIVE_ERROR {#details-for-the-native-error-notification}

Quando TVSDK gestisce un errore nativo, restituisce come stringhe alcuni o tutti i seguenti valori di chiave di metadati.

<table id="table_7F713B7A56024D8DA3C84E449D09CC91"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>Nome chiave metadati</b></th> 
   <th colname="col2" class="entry"><b>Valore metadati</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> NATIVE_ERROR_CODE</span> </td> 
   <td colname="col2"> <p>Codice di errore nativo da AVE. </p> <p>Questi codici rappresentano quanto segue: 
     <ul id="ul_1F33D523DDFE4CE8B4F0DC279FF7E4F8"> 
      <li id="li_07A2D9BEE6364935A61EF3BD4AB6DE27">Errori DRM (codici da 3300 a 3367). Sono gli stessi dei codici di errore equivalenti di Flash Player </li> 
      <li id="li_433BA22DE3504AEEB623598BB4F939FA">Errori di riproduzione video (da -1 a 89) </li> 
      <li id="li_B347CB151DB94DE0A1DDEB1B33D2DABA">Errori di crittografia (da 300 a 307) </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> NATIVE_ERROR</span> </td> 
   <td colname="col2">Breve descrizione della notifica (ad esempio, <span class="codeph"> AAXS_InvalidVoucher</span> o <span class="codeph"> DECODER_FAILED</span>). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DESCRIPTION</span> </td> 
   <td colname="col2"> Descrizione lunga della notifica (ad esempio, Operazione di risoluzione annunci non riuscita). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> PSDK_ERROR_CODE</span> </td> 
   <td colname="col2"><span class="codeph"> com.adobe.mediacore.PSDKErrorCode</span> valore numerico come stringa (ad esempio, "13"). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> PSDK_ERROR</span> </td> 
   <td colname="col2"><span class="codeph"> com.adobe.mediacore.PSDKErrorCode</span> come stringa (ad esempio, <span class="codeph"> kECNetworkError</span>). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AVVISO</span> </td> 
   <td colname="col2"> Descrizione dell’avviso. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ERRORE</span> </td> 
   <td colname="col2"> Descrizione dell’errore. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>DRM</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> NATIVE_SUBERROR_CODE</span> </td> 
   <td colname="col2"> Errore secondario dal modulo DRM. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DRM_ERROR_STRING</span> </td> 
   <td colname="col2"> Descrizione dell’errore. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DRM_ERROR_SERVER_URL</span> </td> 
   <td colname="col2"> URL del server DRM a cui TVSDK ha tentato di parlare. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Errore di caricamento del manifesto annuncio</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_URL</span> </td> 
   <td colname="col2"> URL del contenuto che non è stato possibile caricare. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_TYPE</span> </td> 
   <td colname="col2">Tipo di annuncio (una costante dall’enum <span class="codeph"> MediaResource.Type</span> ). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_DURATION</span> </td> 
   <td colname="col2"> Durata dell'annuncio in millisecondi. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_ID</span> </td> 
   <td colname="col2"> ID assegnato all’annuncio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Errori del file</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DOWNLOAD_ERROR</span> </td> 
   <td colname="col2"> Descrizione dell'errore durante il download del file multimediale. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> URL</span> </td> 
   <td colname="col2"> URL del file che si sta scaricando. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> MANIFEST_ERROR</span> </td> 
   <td colname="col2"> Descrizione dell'errore durante il download del file manifesto. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> CONTENT_ERROR</span> </td> 
   <td colname="col2">Descrizione dell'errore durante il download del frammento (ad esempio, <span class="codeph"> ts</span>). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Errori di traccia audio</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AUDIO_TRACK_NAME</span> </td> 
   <td colname="col2"> Nome della traccia audio che non è stato possibile caricare, come specificato nel manifesto. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AUDIO_TRACK_LANGUAGE</span> </td> 
   <td colname="col2"> Lingua della traccia audio, come specificato nel manifesto. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Errori di ricerca</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DESIRED_SEEK_PERIOD</span> </td> 
   <td colname="col2"> ID del punto (numero intero). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DESIRED_SEEK_POSITION</span> </td> 
   <td colname="col2"> <p>Posizione (in millisecondi) ricercata (doppia). </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Varie</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AUDITUDE_ERROR_CODE</span> </td> 
   <td colname="col2"> Codice di errore Auditude (numero). </td> 
  </tr> 
 </tbody> 
</table>

## NATIVE_ERROR: Valori DRM {#section_D240082B93D34902A18C3923C1C717B3}

L&#39;interfaccia Video Encoder del motore video Adobe restituisce queste notifiche DRM nell&#39;oggetto `NATIVE_ERROR` metadata.

Quando segnalate errori DRM ad Adobe, accertatevi di includere il `NATIVE_SUBERROR_CODE` e `DRM_ERROR_STRING` per assistenza nella risoluzione dei problemi.

>[!TIP]
>
>Questo elenco contiene informazioni specifiche per TVSDK sugli errori. Per una descrizione completa, consultate Guida di riferimento di ActionScript per gli errori di runtime [ActionScript per la piattaforma](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/runtimeErrors.html#3300)Adobe Flash.

<table id="table_CD59A859865F4FFDBAA249C89C74770A"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>Valore per la chiave di metadati NATIVE_- ERROR_CODE</b></th> 
   <th colname="col2" class="entry"><b>Valore per la chiave di metadati NATIVE_ERROR_NAME</b></th> 
   <th colname="col3" class="entry"><b>Significato</b></th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 3300 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidVoucher</span> </td> 
   <td colname="col3"> 
    <ul id="ul_516E4CB32D624B22892DDB9266CB04CA"> 
     <li id="li_348FC0F38B11417994119B61C9244076">Cosa deve fare il software del distributore: 
      <ul id="ul_7AFD45CF92454BA4927783FAA628FBC4"> 
       <li id="li_0D9CCE61612643648C12DCDDD252E52A">Se utilizzate Google Chrome e siete in modalità Incognito e la versione di Flash Player è inferiore alla 11.6, l'errore potrebbe verificarsi. <p>È consigliabile che il lettore controlli il numero di versione del browser e consigliamo all'utente di uscire dalla modalità Incognito. </p> </li> 
       <li id="li_1DC6B755BD0840D48BEC92568FD330BA">Richiedete di nuovo la licenza. <p>Se la richiesta ha esito positivo, non è necessario registrarsi o inoltrare la richiesta. Se la richiesta non riesce, registrate il contenuto che ha causato l’errore. <span class="codeph"> subErrorId</span> contiene un errore di riga, se presente. </p> </li> 
      </ul> </li> 
     <li id="li_060B5D60C9BB419CBFA7B062FBCF2632">Cosa deve fare il distributore: 
      <ul id="ul_FADB29DBF0DA4A0E8E54134AEB7DCD8A"> 
       <li id="li_FC5B1C04D21E4AECB0EBD9ADD3198504">Se i tentativi non vengono eseguiti correttamente in configurazioni diverse da Chrome con Flash meno della versione 11.6, è possibile che si sia verificato un errore nel pacchetto. </li> 
       <li id="li_A720ECE591254021879B335B81B1F76D">Verificate se il problema è specifico a determinati contenuti e reinserite il pacchetto. </li> 
      </ul> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3301 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AuthenticationFailed</span> </td> 
   <td colname="col3"> <p>Il server non è riuscito ad autenticare o autorizzare il client. </p> 
    <ul id="ul_BE77AC1848FB4C09B6318359ACF1B8EE"> 
     <li id="li_6FB37D317D174E8488C5070D20CD241C">Il software del distributore deve intraprendere qualsiasi azione necessaria per ripristinare le credenziali dell'utente o per guidare l'utente ad acquisire l'accesso al contenuto. </li> 
     <li id="li_BE071D59805B42D38E3E7650BC936417">Il distributore deve confermare che il meccanismo di autorizzazione e autenticazione del distributore funziona correttamente. <p>Se i distributori non intendono utilizzare le funzioni di autenticazione o autorizzazione, devono verificare se il criterio del contenuto che ha commesso l'errore richiede l'autenticazione e vedere Differenze di criteri di diagnostica/licenza. </p> </li> 
    </ul> <p>Per ulteriori informazioni su questo codice di errore, vedere <a href="https://forums.adobe.com/thread/1277149" format="https" scope="external"> DRM error 3301 cause e risoluzione</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3302 </td> 
   <td colname="col2"><span class="codeph"> AAXS_RequireSSL</span> </td> 
   <td colname="col3"> <p>In Access 4.0 e versioni successive, questo errore viene restituito su iOS quando l'URL della chiave remota non utilizza HTTPS come schema. HTTPS è obbligatorio. </p> 
    <ul id="ul_3D47777BBCA14B67B107FBBE3E37E40C"> 
     <li id="li_7F7BBB27AE754CC39ABAAF9269739C49">Se il distributore utilizza una versione precedente ad Access v4 o almeno 4 ma la piattaforma non è iOS, il software del distributore deve registrare l'errore. <p>L'errore viene restituito solo su iOS. </p> </li> 
     <li id="li_D83C427D2A0D47408F723EF7195070B6">Se il software del distributore è almeno Adobe Access versione 4 e la piattaforma è iOS, i distributori devono modificare l'URL del server della chiave remota che stanno utilizzando in HTTPS. <p>Se utilizzavano solo HTTP, i distributori potrebbero dover configurare un server HTTPS. In caso contrario, i distributori devono inviare ad Adobe le informazioni registrate e inoltrare il problema. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3303 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ContentExpired</span> </td> 
   <td colname="col3"> <p>Il contenuto visualizzato è scaduto in base alle regole impostate dal provider di contenuti. subErrorId contiene un errore di riga o un errore specifico del client. </p> <p> 
     <ul id="ul_1E4B3B8AE87A4E79997553BB2A0E52B9"> 
      <li id="li_EE3F2EEBF73743B9A38E4FCB7531E275">Il software del distributore deve tentare di riacquisire la licenza dal server una volta per determinare se è disponibile una nuova licenza non scaduta. <p>Se la licenza non è disponibile o se la licenza è scaduta, consentire all'utente di acquisire una nuova licenza o informare l'utente che il contenuto non può essere guardato. Se il contenuto è stato incluso in un pacchetto con un criterio con una data di scadenza/fine scaduta, i registri del server di licenze segnalano un'eccezione <span class="codeph"> PolicyEvaluationException</span> e dichiarano che la data di fine del criterio è scaduta (codice di errore del server 303). Controllare i file di registro del server per verificare. </p> <p>Se possibile, i clienti devono verificare se il criterio utilizzato durante la creazione del pacchetto è scaduto. Lo strumento della riga di comando Java è: <code> java&nbsp;-jar&nbsp;libs/AdobePolicyManager.jar&nbsp;&nbsp;&nbsp;detail&nbsp;demo.pol</code> </p> </li> 
      <li id="li_50DBE680D8F04E7DA3E29C65A93188E7">Il distributore deve confermare se le date di scadenza della licenza sono configurate come previsto. </li> 
     </ul> </p> <p>Per ulteriori informazioni su questo codice di errore, vedere <a href="https://forums.adobe.com/thread/1300813" format="https" scope="external"> 3303 (Contenuto scaduto) con AMS/FMS che utilizza un Live Stream?</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3304 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AuthorizationFailed</span> </td> 
   <td colname="col3">Per ulteriori informazioni su questo codice di errore, vedere <a href="https://forums.adobe.com/thread/1277149" format="https" scope="external"> DRM error 3301 cause e risoluzione</a>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3305 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerConnectionFailed</span> </td> 
   <td colname="col3"> <p>Timeout della connessione ai server licenze o di dominio a causa di un ritardo di rete o della disconnessione del client. Normalmente subErrorId contiene il codice di ritorno HTTP. </p> 
    <ul id="ul_938C7D8F07F64B4FA71A09DDF37E2E64"> 
     <li id="li_6648EA0049094E369BD9AE9CCA6B148D">Il software del distributore deve tentare una connessione di rete a un server di interesse noto. <p>Se il tentativo non riesce, richiedere all'utente di riconnettersi alla rete. Se il tentativo ha esito positivo, registratelo. </p> </li> 
     <li id="li_2ECA2C04BA08449DA3AD79A52EFAA229">Il distributore deve verificare che i server di licenze e domini in uso siano online e visibili dalla rete del client. </li> 
    </ul> <p>Per ulteriori informazioni su questo codice di errore, vedere <a href="https://forums.adobe.com/thread/1284947" format="https" scope="external"> Cause e risoluzione</a>DRM 3305 [ServerConnectionFailed]. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3306 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ClientUpdateRequest</span> </td> 
   <td colname="col3"> Utilizzate una versione più recente di TVSDK per Android. <p>Il client corrente non è in grado di completare l'azione richiesta, ma un client aggiornato potrebbe essere in grado di completare la richiesta. </p> <p>Questo può essere dovuto a diverse cause: 
     <ul id="ul_2EC4D42D5273439FA1AFDA1A2578B3D6"> 
      <li id="li_FCA926F5FAED4E7190BE855545AB6ACF">È stato utilizzato un dominio condiviso che non è disponibile su questo client. Questo è probabilmente il caso quando la riproduzione funziona su Chrome, ma non su qualsiasi altro browser e viceversa. <p> <p>Suggerimento: Chrome utilizza una chiave PHDS/PHLS diversa dagli altri browser utilizzati. Per ulteriori informazioni, consultate <a href="https://adobeprimetime.zendesk.com/agent/tickets/2891" format="https" scope="external"> https://adobeprimetime.zendesk.com/agent/tickets/2891</a>. </p> </p> </li> 
      <li id="li_3B633FB699234DCEA136E9BE3CC3386D">L'applicazione sta tentando di aggiungere più sessioni DRMS quando viene eseguita su una versione iOS precedente alla 5.0. </li> 
      <li id="li_F7ED993AF0B941A7A27216B4D587A999">I metadati hanno una versione 3 o superiore quando è supportata solo la versione 2. </li> 
     </ul> </p> 
     <ul id="ul_EE4AE6AD4F1745A5B5623E53B599DB62"> 
      <li id="li_7A83869D4262443DA35FA1DF8D3097DD">Il software del distributore deve avvisare l'utente e interrompere l'operazione. <p>Se il software ha un modo per determinare se un aggiornamento è disponibile, indirizzare l'utente a tale aggiornamento nel modo appropriato per la piattaforma. </p> </li> 
      <li id="li_AF9C2711FDE54DA196EB9D2864632000">Se il problema si verifica a causa di un dominio condiviso, il distributore dovrà verificare con Adobe se è disponibile un runtime o una libreria aggiornata. <p>Per il runtime Flash, il distributore può forzare l'aggiornamento direttamente nella propria applicazione. Nel caso di una libreria, il distributore dovrà ottenere una libreria aggiornata, ricreare l'applicazione e distribuirla ai propri utenti. </p> <p>Se il problema si verifica a causa di più sessioni DRMS, il distributore dovrà aggiornare l'applicazione per controllare il numero di versione iOS prima di aggiungere più sessioni DRMS. Oppure possono limitare la distribuzione dell'applicazione a iOS v5 e versioni successive. </p> <p>se il problema si verifica perché la versione dei metadati è superiore alla versione 2, il problema potrebbe essere causato da metadati danneggiati. Possono provare a ricreare i metadati e a osservare i risultati. Se il problema persiste, registrarlo e inoltrarlo ad Adobe. </p> </li> 
     </ul> <p>Per ulteriori informazioni su questo codice di errore, vedere <a href="https://forums.adobe.com/thread/1266675" format="https" scope="external"> Come risolvere un codice di errore 3306 DRMErrorEvent</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3307 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InternalFailed</span> </td> 
   <td colname="col3"> <p>In genere questo rappresenta un bug nel codice di Adobe Access ed è imprevisto, a meno che non sia presente un bug noto, come indicato di seguito. subErrorId contiene un errore di riga o un errore specifico del client. </p> 
    <ul id="ul_79F4A9655A2148519B1E9509C41F78C3"> 
     <li id="li_0E093AB4D6BD489B852279E6C1525A15">Se il browser è Chrome su Windows e la versione Flash è 11.6 (SWF versione 19 o successiva), il software del distributore deve presupporre che l'utente abbia premuto <span class="uicontrol"> Rifiuta</span> sulla barra laterale e abbia lo stesso trattamento di 3368. </li> 
     <li id="li_0215D1089B344861A2C0A73E1067CFEF">Se si verifica 3307 quando il browser non è Chrome o la versione Flash non è 11.6, il distributore deve passare ad Adobe. </li> 
    </ul> <p>Importante: <span class="codeph"> 3307:1107296344 (FailedToGetBrokerHandle)</span> potrebbe verificarsi con le versioni del browser Chrome 24-28. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3308 </td> 
   <td colname="col2"><span class="codeph"> AAXS_WrongLicenseKey</span> </td> 
   <td colname="col3"> <p>Questo errore viene generato ogni volta che la licenza utilizzata contiene la chiave sbagliata per decrittografare il contenuto. subErrorId contiene un errore di riga o un errore specifico del client. </p> <p>Esistono solo due modi per generare questo bug: 
    <ul id="ul_1C955BD74C7843809D1B5A0CDCA5ED7B"> 
     <li id="li_18F0A7FDA6584887AD9DB3EDE54080D8">Il cliente ha modificato lo strumento standard Adobe per la generazione di licenze (ad esempio, il framework Java del server licenziatario). <p>In questo caso, la licenza contiene una chiave non valida che potrebbe non corrispondere ad alcun contenuto. </p> </li> 
     <li id="li_21D04ED1F1FA464785BC297D385766FF">Il cliente ha rilasciato più licenze con lo stesso ID licenza. <p>In questo caso, sul client sono disponibili più licenze che corrispondono ai metadati del contenuto e il codice di accesso ha selezionato quella errata per l'uso. </p> </li> 
    </ul> </p> 
    <ul id="ul_64AEE62BE36946F290067CF475A36ECA"> 
     <li id="li_9EEB2B11A4DA41E78C5840D8FAA81F0D">Il software del distributore deve tentare di riacquisire la licenza dal server. 
      <ul id="ul_ACADC5518B054D0A853AEED2B675DB23"> 
       <li id="li_394835C8731048A5BF7D9370AC12448C">Se non è disponibile alcuna licenza o la licenza è scaduta, fornite il flusso di lavoro per consentire all'utente di acquisire una nuova licenza, oppure informate l'utente che il contenuto non può essere guardato e registrate il problema. </li> 
       <li id="li_3FE50518BE53405F9563FA620F7EAD5F">Se si tratta di un contenuto associato a un dominio (per AIR), fornite all'utente la possibilità di unirsi al dominio. </li> 
      </ul> </li> 
     <li id="li_C80B353C1AEA4E9398241420CB491E84">Il distributore deve: 
      <ul id="ul_B5C50009374C4EED9B2B050B48F5F0F6"> 
       <li id="li_D5E6B760E0BC4B5C949ED1544B398838">Verificare che non siano state personalizzate le porzioni di rilascio della licenza del server delle licenze di accesso. </li> 
       <li id="li_AA8F4E4B6DDD40BA8807C0920A92186B">Verifica che stiano rilasciando ID di licenza univoci per tutte le licenze. </li> 
       <li id="li_A2C53FE779AC4FDDB65E00A2C4F43EC4">Escalate il problema con Adobe. </li> 
      </ul> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3309 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CorruptedAdditionalHeader </span> </td> 
   <td colname="col3"> <p>Ciò si verificherà se l'intestazione è superiore a 65536 byte. </p> 
    <ul id="ul_82C0F688519B4F43A764D59A891F1903"> 
     <li id="li_E66AC9149A0649E88A79C5289C12C395">Il software del distributore deve registrare quale parte del contenuto ha causato l'errore. </li> 
     <li id="li_1C5916A33E7B4DC9968105B9BD20A727">Il distributore deve confermare che l’errore è riproducibile con contenuti specifici. Realizza il pacchetto del contenuto interrotto. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3310 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AppIDMismatch </span> </td> 
   <td colname="col3">L'applicazione Android non corrisponde a quella in uso. <p>L’applicazione AIR o il file SWF Flash corretto non viene utilizzato. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3311 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AppVersionMismatch </span> </td> 
   <td colname="col3"> Non in uso. Questo problema potrebbe essere ancora generato dallo stack della versione 1.x in AIR. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3312 </td> 
   <td colname="col2"><span class="codeph"> AAXS_LicenseIntegrity </span> </td> 
   <td colname="col3"> Per risolvere il problema, scaricate nuovamente la licenza dal server. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3313 </td> 
   <td colname="col2"><span class="codeph"> AAXS_WriteMicrosafeFailed </span> </td> 
   <td colname="col3"> <p>Questo problema si verifica quando il sistema non è in grado di scrivere nel file system. <span class="codeph"> subErrorId</span> contiene un errore di riga o un errore specifico del client. </p> <p>In Microsoft Windows, l'errore 3313 potrebbe essere restituito da Active X o dal lettore Flash NPAPI se il contenuto crittografato dispone di un ID licenza o di un ID criterio troppo lungo. Ciò è dovuto alla lunghezza massima del percorso in Windows. (Il plugin del pepe non ha questo problema.) </p> <p>Vedere watson 3549660 </p> 
    <ul id="ul_DFD527D1E1224A439766DF7BED878E3B"> 
     <li id="li_FAF8FD98A4E8478CA7A92F770676ADFC">Il software del distributore deve richiedere all'utente di confermare che la propria directory utente non è bloccata né su un volume pieno o bloccato. </li> 
     <li id="li_6D1136EA750A459BBECEEE5F73F527BB">Se il distributore utilizza AIR, anziché Flash, il problema potrebbe essere causato da una limitazione della lunghezza del percorso. <p>I distributori devono ridurre il nome dell’applicazione AIR a qualcosa di ragionevole. Inoltre, pubblicate nuovamente i contenuti con un <span class="codeph"> ID</span> licenza più breve e un <span class="codeph"> ID</span>criterio. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3314 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CorruptedDRMMetadata </span> </td> 
   <td colname="col3"> <p>Questo errore spesso indica che il contenuto è stato incluso in un pacchetto con certificati PKI di prova e che il lettore è stato creato con PKI di produzione o viceversa. subErrorId contiene un errore di riga o un errore specifico del client. </p> 
    <ul id="ul_A122EF304CAF48A8B4DA1E3F4413E29B"> 
     <li id="li_A9A1A5B23E884C22A71E2DE7535FEB3B">Il software del distributore deve registrare quale parte del contenuto ha causato l'errore. </li> 
     <li id="li_7AD7F13A4B1B4998A7E49664E7645815">Il distributore deve confermare che l'errore è riproducibile con specifici contenuti. <p>Potrebbe essere necessario creare nuovamente un pacchetto per i contenuti interrotti. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3315 </td> 
   <td colname="col2"><span class="codeph"> AAXS_PermissionRifiutato </span> </td> 
   <td colname="col3"> <p>Esistono bug noti in cui questo codice di errore viene generato quando è previsto un codice 3305. Per ulteriori informazioni, consultate <a href="https://forums.adobe.com/thread/1284947" format="https" scope="external"> Cause e risoluzione</a>DRM 3305 [ServerConnectionFailed]. </p> <p>Il file SWF remoto caricato da AIR non può accedere alla funzionalità di Flash Access. Questo codice di errore può essere generato anche se si verifica un errore di sicurezza durante l'accesso alla rete. Alcuni esempi includono il server di destinazione che non consente al client di connettersi utilizzando crossdomain.xml oppure il crossdomain.xml non è raggiungibile. </p> <p>Per ulteriori informazioni, vedere Errore <a href="https://forums.adobe.com/thread/1266592" format="https" scope="external"> DRM 3315 possibile causa principale e risoluzione</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3316 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NOTUSED_MOVED </span> </td> 
   <td colname="col3"> Era <span class="codeph"> ADOBECPSHIM_MinorErr_MissingAdobeCPMomodule</span>. Spostato a 3344 a causa di un conflitto con il codice di errore Flash. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3317 </td> 
   <td colname="col2"><span class="codeph"> AAXS_LoadAdobeCPFail </span> </td> 
   <td colname="col3"> <p>Importante:  Si tratta di un errore raro che in genere non si verifica in un ambiente di produzione. </p> <p>Se l'errore si verifica, potete effettuare una delle seguenti operazioni: 
     <ul id="ul_BC435E61623444BB98A86216531DC892"> 
      <li id="li_FA433D0758B642D2AFDCF04906B3FE18">Se utilizzate AIR, reinstallatela. </li> 
      <li id="li_F08D9AAFF46244F8842DEE5FD9CBBE0A">Se utilizzate Flash Player, scaricate di nuovo i moduli <span class="codeph"> AdobeCP</span> . </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3318 </td> 
   <td colname="col2"><span class="codeph"> AAXS_IncompatibleAdobeCPVersion </span> </td> 
   <td colname="col3"> Non applicabile per Android. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3319 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MissingAdobeCPGetAPI </span> </td> 
   <td colname="col3"> Non applicabile per Android. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3320 </td> 
   <td colname="col2"><span class="codeph"> AAXS_HostAuthenticateFailed </span> </td> 
   <td colname="col3"> Non applicabile per Android. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3321 </td> 
   <td colname="col2"><span class="codeph"> AAXS_I15nFailed </span> </td> 
   <td colname="col3"> <p>Il processo di provisioning del client con chiavi non è riuscito. subErrorId contiene un errore di riga o specifico del server specifico per il client. </p> 
    <ul id="ul_98D919B9060A441AACB6106F6D8E8DA7"> 
     <li id="li_DCAB00A8AC4A426CBBD377374B3F71AE">Il software del distributore deve ripetere l'operazione almeno una volta. <p>Se utilizzate Google Chrome in Windows, fornite una spiegazione su come consentire l'accesso del plugin che non è in una sandbox. Per ulteriori informazioni, consultate <a href="https://helpx.adobe.com/adobe-access/kb/error-3321.html" format="html" scope="external"> Accesso non sandbox di Google Chrome negato</a>. </p> </li> 
     <li id="li_7FB7681FE32D444BB1BDBA3E5953A2C3">Il distributore deve completare una delle seguenti attività: 
      <ul id="ul_486B64F187C44AE3B4775953A6142836"> 
       <li id="li_095B1D4CD051427CB2BFA7082B454056">Se l'errore è coerente su più piattaforme, è necessario inoltrare il problema ad Adobe. </li> 
       <li id="li_0C6EB7B912FA41E59657216498DA3515">Se l'errore è limitato a Chrome in Windows, guidare l'utente per consentire l'accesso ai plug-in non sandbox. </li> 
      </ul> <p>I distributori devono aggiornare il file SWF alla versione 19 o successiva e l'errore 3321 specifico per Chrome, generando un errore 3368. L'errore 3368 può essere gestito in modo più specifico dal software del distributore. Questa modifica è stata introdotta in Chrome Stable Channel versione 26.0.1410.43. </p> <p>Suggerimento: L'errore <span class="codeph"> 3321:1090519056</span> potrebbe verificarsi con Flash Player dalle versioni da 11.1 a 11.6. È consigliabile effettuare l'aggiornamento alla versione più recente di Flash Player. </p> </li> 
    </ul> <p>Per ulteriori informazioni, consultate Errore <a href="https://forums.adobe.com/thread/1277138" format="https" scope="external"> DRM 3321 Causes &amp; Resolution (Cause e risoluzione</a>DRM). </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Errori di corruzione nel negozio globale</b> </td> 
   <td colname="col2"> </td> 
   <td colname="col3"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3322 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DeviceBindingFailed </span> </td> 
   <td colname="col3"> <p>Il dispositivo non sembra corrispondere alla configurazione presente al momento dell'inizializzazione. subErrorId contiene un errore di riga o specifico del client. </p> <p>Il software del distributore deve completare una delle seguenti attività: 
     <ul id="ul_444401051A2E407B95BC44491E9BB71C"> 
      <li id="li_93493EA05DB44CB1AEC368663F1ABA8D"> <p>Se il dispositivo non utilizza Flash Player e utilizza AIR, iOS e così via, chiamate <span class="codeph"> DRMManager.resetDRMVouchers()</span>. </p> <p>Se il problema si verifica su iOS in una fase di sviluppo, chiedete allo sviluppatore di confermare se il problema viene osservato quando si passa da una build scaricata da sistemi di distribuzione di terze parti (ad esempio, HockeyApp) a una build locale da Xcode. Gli attributi di un'installazione precedente non vengono sovrascritti completamente quando si passa da una build distribuita da HockeyApp a una build da Xcode. Questa situazione potrebbe causare l'errore 3322. </p> <p>Per risolvere questo problema, lo sviluppatore deve rimuovere la build precedente dal dispositivo prima di installare la nuova build. </p> </li> 
      <li id="li_A5C9633F11584C788A2D9A23CC18FA6D">Se il dispositivo utilizza Flash Player ed è inutilizzabile dai codici di errore 3322 o 3346, consultare le istruzioni fornite da Adobe su come ripristinare programmaticamente lo store licenze DRM su <a href="https://forums.adobe.com/message/5535907#5535907" format="https" scope="external"> DRM Error 3322/3346/3368 in Chrome (Info-Bar Problems)</a>. </li> 
     </ul> </p> <p>Questo errore non deve verificarsi frequentemente. Negli ambienti aziendali che utilizzano i profili di roaming, se un utente visualizzava contenuto protetto da DRM, l'errore di probabilità 3322 aumenta quando l'utente accede da computer diversi. Se possibile, il distributore deve cercare di ottenere queste informazioni dall'utente. </p> <p>Se l’errore si verifica frequentemente, eseguite l’inoltro fino ad Adobe. È necessario notificare ad Adobe se il ripristino dello store licenze ha risolto il problema (o meno) e indicare ad Adobe in quali browser si trova l'errore. </p> <p>Per ulteriori informazioni, consultate i seguenti articoli: 
     <ul id="ul_C468409D1EA046178CA7F54DCDCB84EA"> 
      <li id="li_20C8CA3853574CE486F21E7A3667DAB9"><a href="https://forums.adobe.com/message/5520902" format="https" scope="external"> https://forums.adobe.com/message/5520902</a> </li> 
      <li id="li_6E6F1BD6FE7843449B3E2F06F342EFF7"><a href="https://forums.adobe.com/message/5535911" format="https" scope="external"> https://forums.adobe.com/message/5535911</a> </li> 
      <li id="li_2BE40E513A0C4BAD900C7B69FEF5D690"><a href="https://forums.adobe.com/message/5748618" format="https" scope="external"> https://forums.adobe.com/message/5748618</a> </li> 
      <li id="li_9C2BD122E3874E2893DD43E082A877E0"><a href="https://forums.adobe.com/message/6061165" format="https" scope="external"> https://forums.adobe.com/message/6061165</a> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3323 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CorruptGlobalStateStore </span> </td> 
   <td colname="col3"> <p>I file utilizzati dal client DRM sono stati modificati in modo imprevisto. subErrorId contiene un errore di riga o specifico del client. </p> 
    <ul id="ul_96EA771046CA4B2B9FAE24D493F43FF2"> 
     <li id="li_D2693CD8EFEF46108828BA17E3F54FF6">Il software del distributore deve guidare l'utente a reimpostare come per 3322. </li> 
     <li id="li_0149B82436B64E28AC2B8C9B0EB09898">Se GlobalStore non riesce a un tasso superiore al tasso di errore previsto per i dischi rigidi della base utenti, inoltrate il problema ad Adobe. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3324 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MachineTokenInvalid </span> </td> 
   <td colname="col3"> Reimpostare l'archiviazione locale DRM per l'applicazione. Chiama DRMManager.resetDRM. <p>Il server licenze potrebbe non essere in grado di connettersi al server Elenco revoca certificati (CRL, Certificate Revocation List) per aggiornare i file CRL oppure il computer client richiede una licenza/autenticazione revocata dal server licenze. </p> <p>Nei registri del server, il codice di errore 111 è MachineTokenInvalid. Tuttavia, a livello di client, il codice di errore 111 viene convertito in codice di errore 3324. </p> <p>L'amministratore del server licenze DRM deve verificare se il server licenze del cliente è mai stato in grado di recuperare i file Adobe CRL. Se il cliente utilizza Tomcat, il cliente può controllare la<span class="filepath"> directory tomcat/temp/</span> per verificare se sono presenti 4 file CRL. </p> 
    <ul id="ul_23B7F1A104AF49E79EA87DB8E15E337E"> 
      <li id="li_855D87F251184FE688A8D5FA0F6C9EF5">Se i file si trovano in questa directory, fare doppio clic sui file in Esplora risorse di Windows e nell'applicazione visualizzatore CRL determinare se uno dei file è scaduto. </li> 
      <li id="li_58EC4EDA2B5146188A0FF7B33C91E2FD">Se non ci sono file in tomcat/temp/, si può presumere che il server licenze non sia mai stato in grado di raggiungere il server Adobe CRL a causa di un problema di firewall/routing. Per ulteriori informazioni, consultate Regole <a href="https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_secure_deployment_guidelines.pdf" format="http" scope="external"> del firewall.</a></li>
    </ul> </p> <p>Se i file CRL non sono disponibili o sono scaduti, è necessario verificare se è possibile raggiungere il server licenze. Aprite un server di controllo di rete sul server licenze del cliente, riavviate il server e tentate il client di richiedere una licenza al server. Potete osservare il traffico di rete per verificare se le chiamate agli endpoint URL seguenti hanno esito positivo: <p>Suggerimento:  È inoltre possibile immettere i seguenti URL CRL in un browser per verificare se è possibile scaricare manualmente ciascun file. </p> 
    <ul id="ul_9B65C7ABBDEC4AC9BF3755FFD3587971"> 
      <li id="li_6867A9050E8D421C9138AC853D1784C9"><a href="https://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl" format="http" scope="external"> crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl</a> </li> 
      <li id="li_6431689260554EAFAFDA2EC31798DCB5"><a href="https://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl" format="http" scope="external"> crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl</a> </li> 
      <li id="li_2939674D0F854ADEB67E45FD216288A2"><a href="https://crl2.adobe.com/Adobe/FlashAccessRootCA.crl" format="http" scope="external"> crl2.adobe.com/Adobe/FlashAccessRootCA.crl</a> </li> 
      <li id="li_96386E00BE9D4CB99D100057A5F7C6DD">crl3.adobe.com/AdobeSystemsIncorporated</li> 
    </ul> </p> <p>Se le regole del firewall sono aperte e non si verificano errori 3324 correnti, potrebbe essersi verificato un problema di rete temporaneo. Controllate i registri del server del cliente, che si trovano probabilmente nella directory <span class="codeph"> /tomcat/logs/</span> , per determinare se si è verificato un errore quando il server licenze ha tentato di recuperare gli elenchi di revoca dei certificati. <p>Importante:  È possibile che si verifichi un errore quando un numero elevato (o una frammentazione) di client segnala un errore 3324 a un problema di rete temporanea durante il rinnovo di un file CRL. Quando è stato risolto il problema della rete, sono stati risolti anche i 3324 problemi. </p> </p> <p>Se tutti e 4 i file CRL sono presenti nella directory <span class="filepath"> tomcat/temp/</span> e i client ottengono ancora 3324 codici di errore, potrebbero verificarsi problemi di accesso ai file CRL. Per risolvere questo problema, è possibile esaminare i registri ed eliminare i file CRL esistenti. </p> <p>Se non si verificano problemi con il server, richiedere all'utente di reimpostare come descritto in 3322. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Errori di danneggiamento dell'archivio server</b> </td> 
   <td colname="col2"> </td> 
   <td colname="col3"> </td> 
</tr> 
  <tr> 
   <td colname="col1"> 3325 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CorruptServerStateStore </span> </td> 
   <td colname="col3"> <p>I file utilizzati dal client DRM sono stati modificati in modo imprevisto. <span class="codeph"> subErrorId</span> contiene un errore di riga o specifico del client. </p> 
    <ul id="ul_860D2402DA61460AB0D938F1116F6D64"> 
     <li id="li_CF368C43452B4265B62ADA3E223894BA">Il software del distributore deve riprovare a eseguire l'operazione, perché AdobeCP ha eliminato internamente lo store del server che ha commesso l'errore e un nuovo tentativo dovrebbe riuscire. Se il tentativo non riesce, registrate il problema. </li> 
     <li id="li_51A5803A1F754970BB4EBD6494F5DC96">Se i tentativi non riescono a raggiungere un tasso superiore al tasso di errore previsto per i dischi rigidi della base utenti, inoltrate il problema ad Adobe. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3326 </td> 
   <td colname="col2"><span class="codeph"> AAXS_StoreTamperingDetected </span> </td> 
   <td colname="col3"> Chiama <span class="codeph"> DRMManager.resetDRM</span>. <p>L'archivio licenze è stato alterato/danneggiato e non può più essere utilizzato. </p> <p>Il software del distributore deve guidare l'utente a reimpostare come descritto in 3322. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3327 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ClockTamperingDetected </span> </td> 
   <td colname="col3"> Correggere l'orologio o acquisire di nuovo la licenza <span class="codeph"> Authn/Lic/Domain</span> . </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Errori server autenticazione/licenza/dominio</b> </td> 
   <td colname="col2"> </td> 
   <td colname="col3"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3328 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerErrorTryagain </span> </td> 
   <td colname="col3"> <p>Si tratta di un errore lato server in cui il server non è stato in grado di completare la richiesta dal client. Questo errore può verificarsi quando, ad esempio, il server è occupato, HTTP/500, il server non dispone della chiave necessaria per decifrare la richiesta e così via. </p> <p>Sul client non c'è modo di determinare cosa sia andato storto. Il cliente deve esaminare i registri del server di Adobe Access, in genere denominati <span class="codeph"> AdobeFlashAccess.log</span>, per determinare gli errori. Nel registro è sempre presente una traccia dello stack descrittiva per indicare il problema. <span class="codeph"> subErrorId</span> contiene un errore di riga o specifico del server. </p> <p>Il distributore deve consultare i registri del server per identificare il server che invia l'errore. Per gli errori 3328 con codice di errore secondario 101, il server non è in grado di decifrare la richiesta. Il cliente deve verificare che i certificati del server di licenza/trasporto installati sul server licenze corrispondano e corrispondano ai certificati utilizzati durante la creazione del pacchetto. </p> <p>Inoltre, se i clienti utilizzano l'implementazione di riferimento, devono assicurarsi che non ci siano errori di battitura nel file <span class="codeph"> flashaccess-refimpl.properties</span> in cui sono specificati i certificati primario e aggiuntivo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3329 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ApplicationSpecificError </span> </td> 
   <td colname="col3"> <p>Il codice di errore secondario specifico dell'applicazione non è noto a Flash Access. <span class="codeph"> subErrorId</span> contiene un errore specifico del server dal server licenze personalizzato degli editori. Il server ha restituito un errore nello spazio dei nomi specifico dell'applicazione. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3330 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DemandAuthentication </span> </td> 
   <td colname="col3"> <p>Questo errore si verifica quando il contenuto è configurato per chiedere ai client di eseguire l'autenticazione prima di ottenere le licenze. </p> 
    <ul id="ul_712D29B8B5A6401FB014C4A283918E32"> 
     <li id="li_2D56905EB50D4FDEAD69CA8EAE38AD1A">Il software del distributore deve autenticare l'utente e quindi acquisire nuovamente la licenza. <p>Se il servizio non intende utilizzare l'autenticazione, registrare l'identificazione del contenuto che sta causando l'errore. </p> </li> 
     <li id="li_B3BCF899B8BE41C7A4F7CF84B0503483">Questo errore non deve richiedere un'escalation, a meno che il contenuto non debba essere configurato per richiedere l'autenticazione. <p>In questo caso, ricreate il pacchetto del contenuto offensivo con il criterio appropriato. Se il contenuto è incluso correttamente, consultate Criteri di diagnostica/discrepanze di licenza. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Errori di applicazione della licenza non riportati sopra</b> </td> 
   <td colname="col2"> </td> 
   <td colname="col3"> </td> 
</tr> 
  <tr> 
   <td colname="col1"> 3331 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ContentNotyetInvalid </span> </td> 
   <td colname="col3"> <p>La licenza acquisita non è ancora valida. Per risolvere il problema, verificare se l'orologio client non è impostato correttamente. Per impostare l'orologio client, ricompilare il contenuto o modificare la configurazione del server licenze. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3332 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CachedLicenseExpired </span> </td> 
   <td colname="col3"> Riacquisire la licenza dal server. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3333 </td> 
   <td colname="col2"><span class="codeph"> AAXS_PlaybackWindowExpired </span> </td> 
   <td colname="col3"> <p>È necessario notificare agli utenti che non possono riprodurre il contenuto fino alla scadenza del criterio. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3334 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidDRMPlatform </span> </td> 
   <td colname="col3"> <p>A questa piattaforma non è consentito riprodurre il contenuto perché, ad esempio, il provider di contenuti ha configurato Adobe Access per negare il contenuto ad Adobe Access su una piattaforma o una licenza condivisa con un dominio è associato a un token di dominio condiviso che è destinato a una partizione diversa. </p> <p>CDM potrebbe generare questo errore se il contenuto non è stato incluso nel pacchetto utilizzando un'appropriata certificazione del packager (con funzionalità CDM). </p> <p>Se il contenuto è incluso in un pacchetto con un certificato PHDS/PHLS non corretto, il contenuto potrebbe funzionare in Chrome ma non in altri browser (o viceversa). <p>Suggerimento:  Questo perché Chrome utilizza diversi certificati PHDS/PHLS. </p>Per confermare quale certificato viene utilizzato, scaricate i dettagli dei metadati del contenuto e cercate i certificati <i></i>dei destinatari. Per ulteriori informazioni, consultate <a href="https://adobeprimetime.zendesk.com/agent/tickets/2891" format="https" scope="external"> https://adobeprimetime.zendesk.com/agent/tickets/2891</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3335 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidDRMVersion </span> </td> 
   <td colname="col3"> Aggiornamento all’ultima versione di TVSDK per Android. <p>Per risolvere il problema, effettuare una delle seguenti operazioni: 
     <ul id="ul_BF1742948BC9461CB8686DE70124D3CD"> 
      <li id="li_690D440C94CC45A0AE55EC319B1C4C23">Aggiornamento AIR </li> 
      <li id="li_CDD20251C881466E88BE7BBB53D61EBC">Per Flash Player, aggiornate il modulo AdobeCP e riprovate a riprodurre. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3336 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidRuntimePlatform </span> </td> 
   <td colname="col3"> <p>A questa piattaforma non è consentito riprodurre il contenuto perché, ad esempio, il provider di contenuti ha configurato Accesso per negare il contenuto a FP/AIR su una piattaforma. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3337 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidRuntimeVersion </span> </td> 
   <td colname="col3"> Aggiornamento all’ultima versione di TVSDK per Android. <p>Ciò si verifica se il contenuto o il server è configurato per negare la riproduzione a una particolare versione dei runtime Flash o AIR. </p> 
    <ul id="ul_B0732D941256483CABBDD30C9BF43249"> 
     <li id="li_72782B1D638F48C0B87084689FB9C798">Se l'utente si trova in un sistema operativo in cui è possibile aggiornare Flash, il software del distributore deve richiedere all'utente di aggiornare Flash e riprovare. In caso contrario, consigliare all'utente di utilizzare un computer diverso. </li> 
     <li id="li_1E3FD93CE39E43F2B7D961299B1211DA">Se si sospetta l'errore 3337, identificare se si verifica per contenuto specifico e ricompilare tale contenuto. Se il contenuto è incluso correttamente, consultate Criteri di diagnostica/discrepanze di licenza </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3338 </td> 
   <td colname="col2"><span class="codeph"> AAXS_UnknownConnectionType </span> </td> 
   <td colname="col3"> <p>Impossibile rilevare il tipo di connessione e il criterio richiede l'attivazione di Protezione output. Questo problema è previsto solo se il contenuto è incluso nel pacchetto e richiede una protezione dell'uscita digitale o analogica. </p> <p>Un problema riscontrato nelle versioni di Flash Player precedenti alla 11.8.800.168 causava occasionalmente l'errore 3338 nel contenuto per il quale il criterio indicava che la protezione del contenuto era <span class="codeph"> USE IF DISPONIBILE</span>. Questo problema è stato risolto nella versione 11.8.800.168 e successive. </p> 
    <ul id="ul_4B6CA26A53F84838B5B95400925464D4"> 
     <li id="li_CBD890F467E449EBB5116E1561252058">Il software del distributore seleziona una variante del contenuto che non richiede protezione dell'output (ad esempio, variante SD di un flusso HD). <p>Se l'errore 3338 si verifica sul contenuto <span class="codeph"> USE_IF_AVAILABLE </span> , controllare il numero di versione del lettore. Se la versione del lettore è inferiore a 11.8.800.168, consigliate all'utente di aggiornare Flash Player. Se l'errore 3338 si verifica sulle versioni successive alla 11.8.800.168, individuare il contenuto che ha causato l'errore. </p> </li> 
     <li id="li_62886C1D96264B129928A7E29E6C70E1">Il distributore deve verificare quale contenuto sta causando questo errore e verificare che il criterio del contenuto stia impostando <span class="codeph"> NO_PROTECTION</span> o <span class="codeph"> USE_IF_AVAILABLE</span> per le uscite analogiche e digitali. <p>Se il contenuto viene inserito inavvertitamente in un pacchetto con <span class="codeph"> NO_OUTPUT</span> o <span class="codeph"> OUTPUT</span>, ricreate il pacchetto del contenuto. Se il contenuto è incluso correttamente, consultate Criteri di diagnostica/discrepanze di licenza. In caso contrario, eseguite l'inoltro fino ad Adobe. </p> </li> 
    </ul> <p>Per ulteriori informazioni, vedere <a href="https://forums.adobe.com/message/5518688" format="https" scope="external"> Come ottenere errori 3338 imprevisti quando il criterio DRM è impostato su USE_IF_AVAILABLE?</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3339 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoAnalogPlaybackAllowed </span> </td> 
   <td colname="col3"> Impossibile riprodurre su dispositivo analogico. Per risolvere il problema, collegare un dispositivo digitale. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3340 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoAnalogProtectionAvail </span> </td> 
   <td colname="col3"> Impossibile riprodurre il contenuto perché la periferica di visualizzazione esterna analogica collegata (monitor/TV) non dispone delle funzionalità corrette (ad esempio, il dispositivo non dispone di Macrovision o ACP). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3341 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoDigitalPlaybackAllowed </span> </td> 
   <td colname="col3"> Impossibile riprodurre il contenuto su un dispositivo digitale. <p>Importante:  Questo problema non dovrebbe verificarsi in un ambiente di produzione, perché gli editori di contenuti non dovrebbero consentire la riproduzione digitale. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3342 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoDigitalProtectionAvail </span> </td> 
   <td colname="col3"> Il dispositivo di visualizzazione digitale esterno (monitor/TV) collegato non dispone delle funzionalità corrette. Ad esempio, il dispositivo non dispone di HDCP. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3343 </td> 
   <td colname="col2"><span class="codeph"> AAXS_IntegrityVerificationFailed </span> </td> 
   <td colname="col3"> <p>Non applicabile per Android. </p> <p>Questo errore si verifica inizialmente dopo il rilascio di una nuova versione di Flash. Si verifica perché Flash è stato aggiornato mentre Flash era aperto, il che mette Flash in uno stato non corretto fino al riavvio del browser. </p> 
    <ul id="ul_A0AC4A77550E40409A04BD33748EA987"> 
     <li id="li_F41C1ABD838D41ABB0DF65093E664A29">Il software del distributore deve completare le seguenti attività: 
      <ul id="ul_79B2AB1372074D448F129851AA24F985"> 
       <li id="li_B93EDD263D78434FAF198A01938D3508">Consiglia all'utente di chiudere o chiudere tutti i browser e quindi riaprirlo. </li> 
       <li id="li_ADFBCFA66AD849E18DB390455458528E">Verificate che la versione di Flash sia corrente. <p>Se la versione non è aggiornata, consigliate al cliente di eseguire l'aggiornamento, chiudere tutte le schede nel browser e riaprire. </p> </li> 
      </ul> </li> 
     <li id="li_281B54582B5949AEA7D166246917EE41">Se dopo il riavvio corretto del browser si verifica un errore, eseguite l'escalation ad Adobe. <p>Quando viene rilasciata una nuova versione, si consiglia di contattare il supporto Adobe per verificare se il problema relativo agli aggiornamenti in background è stato risolto. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3344 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MissingAdobeCPMoModule </span> </td> 
   <td colname="col3"> Non applicabile per Android. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3345 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DRMNoAccessError </span> </td> 
   <td colname="col3"> <p>Non applicabile per Android. </p> <p>Questo errore si verifica quando parte di Flash o AIR non è stata installata correttamente. </p> <p>Il software del distributore deve effettuare una delle seguenti operazioni: 
     <ul id="ul_D1188E2D4FDF4BD89A04F5629D75D981"> 
      <li id="li_B33FBCA5D4534D668B86A5E93DB3A809">Chiedete all'utente di disinstallare e reinstallare AIR. </li> 
      <li id="li_B7D2388E9FA84C26AF1C87B48AF9EF16">Per Flash Player, chiamate <span class="codeph"> System.update</span>. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3346 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MigrationFailed </span> </td> 
   <td colname="col3"> 
    <ul id="ul_518AD4931CC64EB3A962DD451E6C5067"> 
     <li id="li_3C44F0740B08490E9C62D89C40B57DC2">Il software del distributore deve effettuare una delle seguenti operazioni: 
      <ul id="ul_7D90526684BF4EB2BBADCF598AA13086"> 
       <li id="li_D15B4BEDAF7340F6B9BC886DF6E346EC">Se AIR, chiamate <span class="codeph"> DRMManager.resetDRMVouchers()</span> </li> 
       <li id="li_40A51D35408249CFA28DBC49FDA3408B">Se Flash è inutilizzabile a causa degli errori 3322 o 3346 del codice di errore, gli utenti devono andare a <a href="https://forums.adobe.com/message/5535907#5535907" format="http" scope="external"> https://forums.adobe.com/message/5535907#5535907</a> e seguire le istruzioni dell'articolo Adobe per ripristinare programmaticamente l'archivio licenze DRM. </li> 
      </ul> </li> 
     <li id="li_0464471E4A094C80BF2986694341921A">Se l'errore si verifica frequentemente, il distributore deve fornire ad Adobe i dettagli relativi alla versione del lettore di frequenze e alla versione del browser. </li> 
    </ul> <p>Per ulteriori informazioni, consultate i seguenti articoli del forum: 
     <ul id="ul_44E0077FEAA749CC9549BF3846065304"> 
      <li id="li_2BE3B2443380415DA73B7AA3B6547B31"><a href="https://forums.adobe.com/message/5520902" format="https" scope="external"> Errore DRM 3322/3346/3368 in Chrome (problemi della barra Info)</a> </li> 
      <li id="li_4E5C7414756644E1AB78BE7B8112228C"><a href="https://forums.adobe.com/message/5535911" format="https" scope="external"> Errore 3322 o 3346 dopo la modifica dell'hardware</a> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3347 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InsufficienteDeviceCapabilites </span> </td> 
   <td colname="col3"> <p>Il significato principale di questo errore è che la licenza ha un vincolo che il certificato DRM del cliente indica che non può soddisfare. Quando viene emesso il certificato DRM client, vengono definite le seguenti "funzionalità hardware": 
     <ul id="ul_1EB6F1469C244CF0BA52C212495C053D"> 
      <li id="li_646043CE045C4DE2BBC939E1F4963DFE"><b>Bus</b>accessibile non utente. Se <b>true</b>, il supporto decrittografato non scorre mai attraverso un bus o nella memoria principale, dove un'applicazione può accedervi. <p>Se <b>false</b>, il contenuto potrebbe essere accessibile all'applicazione dopo la decrittazione. </p> </li> 
      <li id="li_02AAECAF4D35447BA10554541B46DE67"><b>Radice hardware di affidabilità</b>. Se <b>true</b>, tutto il software caricato al momento dell'avvio sul dispositivo è stato convalidato rispetto a una chiave o un digest che è disponibile solo nell'hardware. <p>Entrambi questi vincoli vengono controllati sul lato client quando la licenza viene aperta rispetto al certificato DRM per il client e l'errore è immediato. Tali vincoli possono essere controllati anche sul lato server prima di rilasciare la licenza. </p> </li> 
     </ul> </p> <p>Il significato secondario di questo errore è che la licenza ha impostato il criterio "Applicazione Jailbreak" e sul dispositivo è stata rilevata un'interruzione di jailbreak. Questo controllo viene eseguito periodicamente sul lato client e non può essere controllato sul lato server. </p> <p>I distributori possono aggiornare i criteri e rimuovere le restrizioni. Per i criteri di funzionalità dei dispositivi, esegui il comando di aggiornamento dei criteri con il flag <span class="codeph"> -devCapabilitiesV1</span> e senza argomenti. Per l'imposizione dell'arresto, imposta <span class="codeph"> policy.forcejailbreak=false</span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3348 </td> 
   <td colname="col2"><span class="codeph"> AAXS_HardStopIntervalExpired </span> </td> 
   <td colname="col3"> Intervallo arresto rigido scaduto. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3349 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerVersionToHigh </span> </td> 
   <td colname="col3"> Il server è in esecuzione in una versione superiore alla versione più recente supportata dal client. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3350 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerVersionToLow </span> </td> 
   <td colname="col3"> Il server è in esecuzione in una versione inferiore alla versione minima supportata dal client. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3351 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainTokenInvalid </span> </td> 
   <td colname="col3"> Token di dominio non valido. Per risolvere questo problema, registratevi nuovamente con il dominio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3352 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainTokenTooOld </span> </td> 
   <td colname="col3"> Il token di dominio è precedente al token richiesto dalla licenza. Per risolvere il problema, registratevi nuovamente con il dominio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3353 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainTokenToNew </span> </td> 
   <td colname="col3"> Il token di dominio è più recente del token richiesto dalla licenza. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3354 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainTokenExpired </span> </td> 
   <td colname="col3"> Token di dominio scaduto. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3355 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainJoinFailed </span> </td> 
   <td colname="col3"> Iscrizione al dominio non riuscita. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3356 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoCorresponsoRoot </span> </td> 
   <td colname="col3"> Impossibile trovare una licenza radice per una licenza foglia V3. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3357 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoInvalidEmbeddedLicense </span> </td> 
   <td colname="col3"> Nessuna licenza incorporata valida trovata. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3358 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoACPProtectionAvail </span> </td> 
   <td colname="col3"> Impossibile riprodurre perché il dispositivo analogico connesso non dispone di protezione ACP. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3359 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoCGMSAProtectionAvail </span> </td> 
   <td colname="col3"> Impossibile riprodurre perché il dispositivo analogico connesso non dispone di protezione CGMS-A. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3360 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainRegistrationRequired </span> </td> 
   <td colname="col3"> Il contenuto richiede la registrazione del dominio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3361 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NotRegisteredToDomain </span> </td> 
   <td colname="col3"> Il computer non è registrato nel dominio per i metadati specificati. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3362 </td> 
   <td colname="col2"><span class="codeph"> AAXS_OperationTimeoutError </span> </td> 
   <td colname="col3"> L'operazione asincrona ha richiesto più tempo di <span class="codeph"> maxOperationTimeout</span>. Restituito solo da iOS DRMNative Framework. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3363 </td> 
   <td colname="col2"><span class="codeph"> AAXS_UnsupportedIOSPlaylistError </span> </td> 
   <td colname="col3"> La playlist M3U8 passata conteneva contenuto non supportato. Restituito solo da iOS DRMNative Framework. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3364 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoDeviceId </span> </td> 
   <td colname="col3"> <p>Il framework ha richiesto l'ID dispositivo, ma il valore restituito era vuoto. </p> <p>L'utente non deve selezionare la casella di controllo <span class="uicontrol"> Consenti identificatori per il contenuto</span> protetto nelle impostazioni di Chrome. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3365 </td> 
   <td colname="col2"><span class="codeph"> AAXS_IncognitoModeNotAllowed </span> </td> 
   <td colname="col3"> <p>Questa combinazione di browser/piattaforma non consente la riproduzione protetta da DRM in modalità Incognito. </p> <p>Il software del distributore deve consigliare all'utente di uscire dalla modalità Incognito o utilizzare un browser diverso. Per ulteriori informazioni, consultate Errore <a href="https://forums.adobe.com/thread/1266622" format="https" scope="external"> DRM 3365 causa e risoluzione</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3366 </td> 
   <td colname="col2"><span class="codeph"> AAXS_BadParameter </span> </td> 
   <td colname="col3"> <p>Il runtime host ha chiamato la libreria di Access con un parametro errato. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3367 </td> 
   <td colname="col2"><span class="codeph"> AAXS_BadSignature </span> </td> 
   <td colname="col3"> Firma manifesto m3u8 non riuscita. Restituito solo da iOS DRMNative Framework o AVE. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3368 </td> 
   <td colname="col2"><span class="codeph"> AAXS_UserSettingsNoAccess</span> </td> 
   <td colname="col3"> <p>L'utente ha annullato l'operazione o ha immesso impostazioni che impediscono l'accesso al sistema. </p> <p>Questo errore viene restituito solo quando la versione SWF è 19 o successiva. Per compatibilità con le versioni precedenti, viene generato 3321 quando il file SWF è della versione 18 o precedente. </p> <p>Il software del distributore deve guidare l'utente in una spiegazione di come consentire l'accesso ai plug-in non sandbox. Per ulteriori informazioni, consultate <a href="https://helpx.adobe.com/adobe-access/kb/error-3321.html" format="html" scope="external"> Accesso alla funzione di unsandbox di Google Chrome negato</a> e Errore <a href="https://forums.adobe.com/message/5520902" format="https" scope="external"> DRM 3322/3346/3368 in Chrome (problemi della barra informazioni)</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3369 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InterfaceNotAvailable</span> </td> 
   <td colname="col3"> <p>L'interfaccia del browser richiesta non è disponibile. Questo problema si verifica solo su Pepper. Potrebbe verificarsi una mancata corrispondenza tra il plug-in Flash e la versione del browser. </p> <p>Il software del distributore deve guidare l'utente a garantire che disponga della versione più recente del browser installato. </p> <p> Se le incidenze di questo errore aumentano e corrispondono al rilascio di un aggiornamento del browser, eseguite l'inoltro ad Adobe. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3370 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ContentIdSettingsNoAccess</span> </td> 
   <td colname="col3"> <p>L'utente ha disabilitato l'impostazione <span class="uicontrol"> Consenti identificatori per il contenuto</span> protetto. </p> <p>Suggerimento:  Questo errore veniva visualizzato con le versioni Pepper 13.0.0.x o successive. </p> <p>Il software del distributore deve guidare l'utente nell'attivazione dell'impostazione <span class="uicontrol"> Consenti identificatori per il contenuto</span> protetto. </p> <p>Il team operativo del distributore deve guidare l'utente nell'attivazione dell'impostazione <span class="uicontrol"> Consenti identificatori per il contenuto</span> protetto. </p> <p>Per ulteriori informazioni, consultate <a href="https://forums.adobe.com/message/6518323#6518323" format="https" scope="external"> https://forums.adobe.com/message/6518323#6518323</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3371 </td> 
   <td colname="col2"><span class="codeph"> Vincoli AAXS_NoOPConstraintInPixel</span><span class="codeph"></span> </td> 
   <td colname="col3"> <p>Risoluzione non valida basata sui vincoli di protezione dell'output contenuti nella licenza. </p> <p>Il software del distributore deve visualizzare un messaggio di errore. Chiedete all'utente di segnalare il problema al distributore con un titolo di contenuto. </p> <p>Il distributore deve creare nuovamente un pacchetto con un criterio valido. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3372 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ResolutionLargeThanMaxResolution</span> </td> 
   <td colname="col3"> <p>La risoluzione del contenuto è maggiore della risoluzione massima specificata nel vincolo di protezione dell'output. </p> <p>Se il team operativo del distributore visualizza questo errore nei propri registri, deve rivedere i criteri di protezione dell'output basati sulla risoluzione e, se necessario, rigenerare il pacchetto del contenuto. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3373 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MinorErr_DisplayResolutionLargeThanConstrain</span> </td> 
   <td colname="col3"> <p>La risoluzione del contenuto è maggiore della risoluzione specificata dal vincolo di protezione dell'output attualmente attivo. </p> <p>Se il team operativo del distributore visualizza questo errore nei propri registri, deve rivedere i criteri di protezione dell'output basati sulla risoluzione e, se necessario, rigenerare il pacchetto del contenuto. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3374 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MinorErr_ClientCommProcessFailed</span> </td> 
   <td colname="col3"> <p>Errore durante l'elaborazione delle comunicazioni lato client, ad esempio generazione di richieste, elaborazione delle risposte, token di autenticazione non valido e così via. </p> <p>Se il team operativo del distributore visualizza questo errore nei propri registri, deve rivedere i criteri di protezione dell'output basati sulla risoluzione e, se necessario, rigenerare il contenuto. </p> </td> 
  </tr> 
 </tbody> 
</table>

## NATIVE_ERROR: Valori di riproduzione video {#section_7079501250C2487499639F92EC774525}

L&#39;interfaccia Video Encoder dell&#39;AVE restituisce le notifiche di riproduzione video nell&#39;oggetto `NATIVE_ERROR` metadata.

<table id="table_5EEB1F60E5854452A8B0BABBE9B32651"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>Valore per la chiave di metadati NATIVE_ERROR_CODE</b></th> 
   <th colname="col2" class="entry"><b>Valore per la chiave di metadati NATIVE_ERROR_NAME</b></th> 
   <th colname="col3" class="entry"><b>Descrizione</b></th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> -1 </td> 
   <td colname="col2"><span class="codeph"> END_OF_PERIOD</span> </td> 
   <td colname="col3"> Fine del periodo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 0 </td> 
   <td colname="col2"><span class="codeph"> SUCCESSO</span> </td> 
   <td colname="col3"> Operazione completata. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 1 </td> 
   <td colname="col2"> <span class="codeph"> ASYNC_OPERATION_IN_PROGRESS</span> </td> 
   <td colname="col3"> Operazione asincrona. La richiesta di operazione è stata effettuata. Le informazioni sul successo/fallimento saranno disponibili in seguito. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 2 </td> 
   <td colname="col2"><span class="codeph"> EOF</span> </td> 
   <td colname="col3"> Operazione non possibile a causa della condizione di fine del file (EOF). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3 </td> 
   <td colname="col2"><span class="codeph"> DECODER_FAILED</span> </td> 
   <td colname="col3"> Il decodificatore non è riuscito in fase di esecuzione. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 4 </td> 
   <td colname="col2"><span class="codeph"> DEVICE_OPEN_ERROR</span> </td> 
   <td colname="col3"> Impossibile aprire il decodificatore hardware. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 5 </td> 
   <td colname="col2"><span class="codeph"> FILE_NOT_FOUND </span> </td> 
   <td colname="col3"> Impossibile individuare la risorsa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 6 </td> 
   <td colname="col2"><span class="codeph"> GENERIC_ERROR </span> </td> 
   <td colname="col3"> Errore generico. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 7 </td> 
   <td colname="col2"><span class="codeph"> IRRECOVERABLE_ERROR </span> </td> 
   <td colname="col3"> Una condizione di errore per la quale il motore video non è in grado di eseguire il ripristino. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 8 </td> 
   <td colname="col2"><span class="codeph"> LOST_CONNECTION_RECOVERABLE </span> </td> 
   <td colname="col3"> Errore di rete, tentativo di ripristino. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 9 </td> 
   <td colname="col2"><span class="codeph"> NO_FIXED_SIZE </span> </td> 
   <td colname="col3"> Impossibile determinare la dimensione della risorsa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 10 </td> 
   <td colname="col2"><span class="codeph"> NOT_IMPLEMENTED </span> </td> 
   <td colname="col3"> Funzionalità non implementata. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 11 </td> 
   <td colname="col2"><span class="codeph"> OUT_OF_MEMORY </span> </td> 
   <td colname="col3"> Memoria insufficiente. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 12 </td> 
   <td colname="col2"><span class="codeph"> PARSE_ERROR </span> </td> 
   <td colname="col3"> Errore durante l'analisi del file multimediale. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 13 </td> 
   <td colname="col2"><span class="codeph"> SIZE_UNKNOWN </span> </td> 
   <td colname="col3"> La risorsa ha una dimensione, ma è sconosciuta. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 14 </td> 
   <td colname="col2"><span class="codeph"> UNDER_FLOW </span> </td> 
   <td colname="col3"> Condizione di underflow. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 15 </td> 
   <td colname="col2"><span class="codeph"> UNSUPPORTED_CONFIG </span> </td> 
   <td colname="col3"> Configurazione non supportata. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 16 </td> 
   <td colname="col2"><span class="codeph"> UNSUPPORTED_OPERATION </span> </td> 
   <td colname="col3"> Operazione non supportata. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 17 </td> 
   <td colname="col2"><span class="codeph"> WAITING_FOR_INIT </span> </td> 
   <td colname="col3"> Non ancora inizializzato. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 18 </td> 
   <td colname="col2"><span class="codeph"> INVALID_PARAMETER </span> </td> 
   <td colname="col3"> Parametro non valido. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 19 </td> 
   <td colname="col2"><span class="codeph"> INVALID_OPERATION</span> </td> 
   <td colname="col3"> Operazione non consentita. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 20 </td> 
   <td colname="col2"><span class="codeph"> OP_ONLY_ALLOWED_IN_PAUSED_STATE</span> </td> 
   <td colname="col3"> L'operazione è consentita solo in pausa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 21 </td> 
   <td colname="col2"><span class="codeph"> OP_INVALID_WITH_AUDIO_ONLY_FILE</span> </td> 
   <td colname="col3"> L'operazione non può essere utilizzata solo sui file audio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 22 </td> 
   <td colname="col2"><span class="codeph"> PREVIOUS_STEP_SEEK_IN_PROGRESS</span> </td> 
   <td colname="col3"> L'operazione di ricerca precedente è ancora in corso. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 23 </td> 
   <td colname="col2"><span class="codeph"> SOURCE_NOT_SPECIFIED </span> </td> 
   <td colname="col3"> Risorsa non specificata. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 24 </td> 
   <td colname="col2"><span class="codeph"> RANGE_ERROR</span> </td> 
   <td colname="col3"> Il valore specificato non è compreso nell'intervallo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 25 </td> 
   <td colname="col2"><span class="codeph"> INVALID_SEEK_TIME</span> </td> 
   <td colname="col3"> Tempo di ricerca non valido. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 26 </td> 
   <td colname="col2"><span class="codeph"> FILE_STRUCTURE_INVALID</span> </td> 
   <td colname="col3"> Il file specificato non è conforme alla sintassi prevista. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 27 </td> 
   <td colname="col2"><span class="codeph"> COMPONENT_CREATION_FAILURE</span> </td> 
   <td colname="col3"> Impossibile creare un componente essenziale. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 28 </td> 
   <td colname="col2"><span class="codeph"> DRM_INIT_ERROR</span> </td> 
   <td colname="col3"> Impossibile creare il contesto DRM. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 29 </td> 
   <td colname="col2"><span class="codeph"> CONTAINER_NOT_SUPPORTED </span> </td> 
   <td colname="col3"> Tipo di contenitore non supportato. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 30 </td> 
   <td colname="col2"><span class="codeph"> SEEK_FAILED</span> </td> 
   <td colname="col3"> Ricerca non riuscita. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 31 </td> 
   <td colname="col2"><span class="codeph"> CODEC_NOT_SUPPORTED</span> </td> 
   <td colname="col3"> Codec non supportato. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 32 </td> 
   <td colname="col2"><span class="codeph"> NETWORK_UNAVAILABLE</span> </td> 
   <td colname="col3"> Rete non disponibile. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 33 </td> 
   <td colname="col2"><span class="codeph"> NETWORK_ERROR</span> </td> 
   <td colname="col3"> Errore durante il recupero dei dati dalla rete. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 34 </td> 
   <td colname="col2"><span class="codeph"> OVERFLOW</span> </td> 
   <td colname="col3"> Overflow. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 35 </td> 
   <td colname="col2"><span class="codeph"> VIDEO_PROFILE_NOT_SUPPORTED</span> </td> 
   <td colname="col3"> Profilo video non supportato. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 36 </td> 
   <td colname="col2"><span class="codeph"> PERIOD_NOT_LOADED</span> </td> 
   <td colname="col3"> È stata tentata un'operazione su un periodo HOLD o su un periodo non ancora caricato. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 37 </td> 
   <td colname="col2"><span class="codeph"> INVALID_REPLACE_DURATION</span> </td> 
   <td colname="col3"> La durata di sostituzione specificata non è valida o si estende oltre la fine del flusso. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 38 </td> 
   <td colname="col2"><span class="codeph"> CALLED_FROM_WRONG_THREAD</span> </td> 
   <td colname="col3"> L'API non può essere chiamata dal thread sbagliato. Principalmente, per gli elementi API che dovrebbero essere richiamati solo dal thread principale. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 39 </td> 
   <td colname="col2"><span class="codeph"> FRAGMENT_READ_ERROR</span> </td> 
   <td colname="col3"> Errore di lettura del frammento. Nessun failover presente. Il motore tenterà di leggere il frammento successivo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 40 </td> 
   <td colname="col2"><span class="codeph"> ABORTO</span> </td> 
   <td colname="col3"> L'operazione è stata interrotta da una chiamata Abort o Destroy esplicita. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 41 </td> 
   <td colname="col2"><span class="codeph"> UNSUPPORTED_HLS_VERSION</span> </td> 
   <td colname="col3"> Impossibile riprodurre questa versione del supporto HLS. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 42 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_FAIL_OVER</span> </td> 
   <td colname="col3"> Impossibile eseguire il failover. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 43 </td> 
   <td colname="col2"><span class="codeph"> HTTP_TIME_OUT</span> </td> 
   <td colname="col3"> Timeout del download HTTP. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 44 </td> 
   <td colname="col2"><span class="codeph"> NETWORK_DOWN </span> </td> 
   <td colname="col3"> La connessione di rete dell'utente non è attiva. La riproduzione potrebbe arrestarsi in qualsiasi momento e riprenderà quando la connessione sarà disponibile. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 45 </td> 
   <td colname="col2"><span class="codeph"> NO_USABLE_BITRATE_PROFILE</span> </td> 
   <td colname="col3"> Nessun profilo di bitrate utilizzabile trovato nel flusso. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 46 </td> 
   <td colname="col2"><span class="codeph"> BAD_MANIFEST_SIGNATURE</span> </td> 
   <td colname="col3"> Il manifesto ha una firma errata. Il test di firma del manifesto non è riuscito. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 47 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_LOAD_PLAYLIST</span> </td> 
   <td colname="col3"> Impossibile caricare una playlist. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 48 </td> 
   <td colname="col2"><span class="codeph"> REPLACEMENT_FAILED</span> </td> 
   <td colname="col3"> La sostituzione specificata in un'API Insert non è riuscita. Ciò significa che l'inserimento è riuscito ma non è stato sostituito. La sostituzione potrebbe non riuscire se il manifesto da sostituire è stato rimosso dalla timeline. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 49 </td> 
   <td colname="col2"><span class="codeph"> SWITCH_TO_ASYMMETRIC_PROFILE</span> </td> 
   <td colname="col3"> DRM sta passando a un profilo asimmetrico. Tutti i profili devono essere allineati in base alla durata. In caso contrario, l'avviso verrà visualizzato e potrebbero verificarsi salti durante la riproduzione. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 50 </td> 
   <td colname="col2"><span class="codeph"> LIVE_WINDOW_MOVED_BACKWARD</span> </td> 
   <td colname="col3"> La finestra Live deve essere spostata solo in avanti. In caso contrario, verrà visualizzato questo avviso e la finestra non verrà letta. A causa di ciò, durante la riproduzione potrebbero verificarsi salti (o interruzioni/pause lunghe). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 51 </td> 
   <td colname="col2"><span class="codeph"> CURRENT_PERIOD_EXPIRED</span> </td> 
   <td colname="col3"> La finestra Live si è spostata oltre il periodo corrente. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 52 </td> 
   <td colname="col2"><span class="codeph"> CONTENT_LENGTH_MISMATCH</span> </td> 
   <td colname="col3"> La lunghezza del contenuto indicata dal server HTTP non corrisponde alla dimensione effettiva del supporto. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 53 </td> 
   <td colname="col2"><span class="codeph"> PERIOD_HOLD</span> </td> 
   <td colname="col3"> Il lettore multimediale non è in grado di leggere ulteriormente perché ha raggiunto il tempo impostato dall'API setHoldAt. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 54 </td> 
   <td colname="col2"><span class="codeph"> LIVE_HOLD </span> </td> 
   <td colname="col3">Il lettore multimediale non è in grado di caricare i segmenti perché ha raggiunto la fine della finestra dal vivo. Il caricamento del segmento riprenderà quando il server aggiungerà nuovi supporti alla finestra dal vivo. Questo stato viene generalmente raggiunto se: 
    <ul id="ul_FCFF658EDA4144E59970B317D6DEB624"> 
     <li id="li_2F6EEEB782D54CD999BC7CC7C0B78B48">Il <span class="codeph"> bufferTime</span> è troppo alto (uguale o superiore alla durata della finestra attiva). </li> 
     <li id="li_25CE97115ED64E44AA89977FB5F0DCF7">Una combinazione di una o più API di inserimento/cancellazione ha sostituito più supporti rispetto all'aggiunta. </li> 
     <li id="li_1B14716B2157492AB1859306D1250523">Il periodo successivo è un periodo live con una sostituzione di supporti in sospeso (a causa della chiamata API InsertBy) </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 55 </td> 
   <td colname="col2"><span class="codeph"> BAD_MEDIA_INTERLEAVING </span> </td> 
   <td colname="col3"> L'interfoliazione audio e video nel supporto non viene eseguita correttamente. Si tratta di un errore di package. L'avviso viene inviato quando la differenza supera i due secondi. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 56 </td> 
   <td colname="col2"><span class="codeph"> DRM_NOT_AVAILABLE</span> </td> 
   <td colname="col3"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 57 </td> 
   <td colname="col2"><span class="codeph"> PLAYBACK_NOT_AUTHORIZED</span> </td> 
   <td colname="col3"> La riproduzione HLS non è stata abilitata in Flash Player. Consulta AuthorizedFeatures.enableHLSPlayback. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 58 </td> 
   <td colname="col2"><span class="codeph"> BAD_MEDIA_SAMPLE_FOUND</span> </td> 
   <td colname="col3"> Il decodificatore ha ricevuto un campione errato che non può essere decodificato. In genere non si tratta di un errore fatale, ma indica che potrebbero verificarsi dei problemi nell’audio/video. Troppe istanze di questo errore indicano una codifica non valida o un file non valido. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 59 </td> 
   <td colname="col2"><span class="codeph"> RANGE_SPANS_READ_HEAD</span> </td> 
   <td colname="col3"> Dopo l'avvio della riproduzione, l'intervallo Inserisci/Sostituisci non deve contenere la testina di lettura. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 60 </td> 
   <td colname="col2"><span class="codeph"> POSTROLL_WITH_LIVE_NOT_ALLOWED</span> </td> 
   <td colname="col3"> Gli inserimenti post-roll non sono consentiti su un supporto live. Tuttavia, sono consentiti dopo che il server contrassegna il supporto come completo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 61 </td> 
   <td colname="col2"><span class="codeph"> INTERNAL_ERROR</span> </td> 
   <td colname="col3"> Una questione molto rara che non dovrebbe mai accadere. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 62 </td> 
   <td colname="col2"><span class="codeph"> SPS_PPS_FOUND_OUTSIDE_AVCC</span> </td> 
   <td colname="col3"> Il flusso non segue la raccomandazione del package di inserire sempre H264 SPS/PPS in un AVCC. È possibile che si verifichino problemi di ricerca/riproduzione. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 63 </td> 
   <td colname="col2"><span class="codeph"> PARAL_REPLACEMENT</span> </td> 
   <td colname="col3"> La sostituzione specificata in un'API Insert è stata eseguita solo in parte. Questo accade quando replaceDuration si estende sulla durata della timeline. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 64 </td> 
   <td colname="col2"><span class="codeph"> RENDITION_M3U8_ERROR</span> </td> 
   <td colname="col3"> Errore durante il caricamento della playlist della rappresentazione. Questo è solo per AVE, non per Flash Player. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 65 </td> 
   <td colname="col2"><span class="codeph"> NULL_OPERATION</span> </td> 
   <td colname="col3"> L'operazione non ha alcun effetto. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 66 </td> 
   <td colname="col2"><span class="codeph"> SEGMENT_SKIPPED_ON_FAILURE</span> </td> 
   <td colname="col3"> Il segmento non può essere riprodotto e viene ignorato in caso di errore. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 67 </td> 
   <td colname="col2"><span class="codeph"> INCOMPATIBLE_RENDER_MODE</span> </td> 
   <td colname="col3"> Modalità di rendering non compatibile. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 68 </td> 
   <td colname="col2"><span class="codeph"> PROTOCOL_NOT_SUPPORTED </span> </td> 
   <td colname="col3"> Il protocollo Web utilizzato nell'URL non è supportato. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 69 </td> 
   <td colname="col2"><span class="codeph"> PARSE_ERROR_INCOMPATIBLE_VERSION</span> </td> 
   <td colname="col3"> Errore durante l'analisi del file multimediale. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 70 </td> 
   <td colname="col2"><span class="codeph"> MANIFEST_FILE_UNEXPECTEDLY_CHANGED</span> </td> 
   <td colname="col3"> Il file manifesto è stato modificato in modo imprevisto. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 71 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_SPLIT_TIMELINE</span> </td> 
   <td colname="col3"> Impossibile eseguire un'operazione di divisione su una timeline. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 72 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_ERASE_TIMELINE</span> </td> 
   <td colname="col3"> Impossibile eseguire un'operazione di cancellazione su una timeline. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 73 </td> 
   <td colname="col2"><span class="codeph"> DID_NOT_GET_NEXT_FRAGMENT</span> </td> 
   <td colname="col3"> Impossibile ottenere il frammento successivo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 74 </td> 
   <td colname="col2"><span class="codeph"> NO_TIMELINE</span> </td> 
   <td colname="col3"> Nessuna timeline presente in una struttura dati interna. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 75 </td> 
   <td colname="col2"><span class="codeph"> LISTENER_NOT_FOUND</span> </td> 
   <td colname="col3"> Nessun listener trovato in una struttura dati interna. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 76 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_START_ERROR</span> </td> 
   <td colname="col3"> Impossibile avviare l'audio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 77 </td> 
   <td colname="col2"><span class="codeph"> NO_AUDIO_SINK</span> </td> 
   <td colname="col3"> Nessun lavello audio presente in una struttura dati interna. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 78 </td> 
   <td colname="col2"><span class="codeph"> FILE_OPEN_ERROR</span> </td> 
   <td colname="col3"> Impossibile aprire il file. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 79 </td> 
   <td colname="col2"><span class="codeph"> FILE_WRITE_ERROR</span> </td> 
   <td colname="col3"> Impossibile scrivere in un file. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 80 </td> 
   <td colname="col2"><span class="codeph"> FILE_READ_ERROR</span> </td> 
   <td colname="col3"> Impossibile leggere da un file. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 81 </td> 
   <td colname="col2"><span class="codeph"> ID3PARSE_ERROR</span> </td> 
   <td colname="col3"> Errore durante l'analisi dei dati ID3. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 82 </td> 
   <td colname="col2"><span class="codeph"> SECURITY_ERROR </span> </td> 
   <td colname="col3"> Caricamento del contenuto non riuscito a causa di restrizioni di protezione. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 83 </td> 
   <td colname="col2"><span class="codeph"> TIMELINE_TOO_SHORT</span> </td> 
   <td colname="col3"> La durata della timeline è troppo breve. Se si tratta di un flusso live, possono verificarsi frequenti buffering. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 84 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_ONLY_STREAM_START</span> </td> 
   <td colname="col3"> Lo streaming è stato commutato in un flusso solo audio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 85 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_ONLY_STREAM_END</span> </td> 
   <td colname="col3"> Lo streaming è stato commutato da solo audio a un flusso con video. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 87 </td> 
   <td colname="col2"><span class="codeph"> KEY_NOT_FOUND </span> </td> 
   <td colname="col3"> Impossibile trovare la chiave. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 88 </td> 
   <td colname="col2"><span class="codeph"> INVALID_KEY</span> </td> 
   <td colname="col3"> La chiave non è valida. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 89 </td> 
   <td colname="col2"> <span class="codeph"> KEY_SERVER_NOT_FOUND</span> </td> 
   <td colname="col3"> Il server delle chiavi non restituisce una chiave. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 90 </td> 
   <td colname="col2"> <span class="codeph"> MAIN_MANIFEST_UPDATE_TO_BE_HANDLED</span> </td> 
   <td colname="col3"> Impossibile gestire l'aggiornamento del manifesto principale. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 91 </td> 
   <td colname="col2"> <span class="codeph"> UNREPORTED_TIME_DISCONTINUITY_FOUND</span> </td> 
   <td colname="col3"> Discontinuità dell'ora non segnalata (PTS) trovata. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 92 </td> 
   <td colname="col2"> <span class="codeph"> UNMATCHED_AV_DISCONTINUITY_FOUND</span> </td> 
   <td colname="col3"> Discontinuità audio e video non corrispondente rilevata. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 93 </td> 
   <td colname="col2"><span class="codeph"> TRICKPLAY_ENDED_DUE_TO_ERROR</span> </td> 
   <td colname="col3">Si è verificato un errore durante la riproduzione del file multimediale in modalità <i>trucco</i> . La modalità di riproduzione dei mattoni è terminata e il flusso viene messo in pausa. Chiamate <span class="codeph"> Play()</span> per riprodurre il supporto in modalità normale. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 95 </td> 
   <td colname="col2"><span class="codeph"> LIVE_WINDOW_MOVED_AHEAD</span> </td> 
   <td colname="col3"> Il giocatore è fuori dalla finestra dal vivo e deve cercare di recuperare. </td> 
  </tr> 
 </tbody> 
</table>

## NATIVE_ERROR: Valori Crypto {#section_39365E545CAC49B9A4D4678657BB2155}

Il modulo di crittografia del motore video Adobe restituisce queste notifiche nell&#39;oggetto `NATIVE_ERROR` metadata.

| **Valore per la chiave di metadati NATIVE_ERROR_CODE** | **Valore per la chiave di metadati NATIVE_ERROR_NAME** | **Significato** |
|---|---|---|
| 300 | `CRYPTO_ALGORITHM_NOT_SUPPORTED` | L&#39;algoritmo utilizzato non è supportato. |
| 301 | `CRYPTO_ERROR_CORRUPTED_DATA` | I dati sono danneggiati. |
| 302 | `CRYPTO_ERROR_BUFFER_TOO_SMALL` | Buffer troppo piccolo. |
| 303 | `CRYPTO_ERROR_BAD_CERTIFICATE` | Certificato non valido. |
| 304 | `CRYPTO_ERROR_DIGEST_UPDATE` | Aggiornamento digest. |
| 305 | `CRYPTO_ERROR_DIGEST_FINISH` | Finitura digest. |
| 306 | `CRYPTO_ERROR_BAD_PARAMETER` | Parametro non valido. |
