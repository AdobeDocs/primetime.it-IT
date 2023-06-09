---
title: Dettagli della notifica NATIVE_ERROR
description: Dettagli della notifica NATIVE_ERROR
copied-description: true
exl-id: 08121879-d5a6-4224-b08d-9e66fe4d185a
source-git-commit: 1bc2f6c230c262babf2958c32fee31afcad04c2f
workflow-type: tm+mt
source-wordcount: '6868'
ht-degree: 2%

---

# Dettagli della notifica NATIVE_ERROR {#details-for-the-native-error-notification}

Quando TVSDK gestisce un errore nativo, restituisce alcuni o tutti i seguenti valori chiave di metadati come stringhe.

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
   <td colname="col2"> <p>Codice di errore nativo dall'AVE. </p> <p>Tali codici rappresentano i seguenti: 
     <ul id="ul_1F33D523DDFE4CE8B4F0DC279FF7E4F8"> 
      <li id="li_07A2D9BEE6364935A61EF3BD4AB6DE27">Errori DRM (codici da 3300 a 3367). Sono identici ai codici di errore equivalenti del Flash Player </li> 
      <li id="li_433BA22DE3504AEEB623598BB4F939FA">Errori di riproduzione video (da -1 a 89) </li> 
      <li id="li_B347CB151DB94DE0A1DDEB1B33D2DABA">Errori di crittografia (da 300 a 307) </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ERRORE_NATIVO</span> </td> 
   <td colname="col2">Breve descrizione della notifica (ad esempio: <span class="codeph"> AAXS_InvalidVoucher</span> o <span class="codeph"> DECODER_FAILED</span>). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DESCRIZIONE</span> </td> 
   <td colname="col2"> Descrizione lunga della notifica (ad esempio, operazione di risoluzione annuncio non riuscita). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> PSDK_ERROR_CODE</span> </td> 
   <td colname="col2"><span class="codeph"> com.adobe.mediacore.PSDKErrorCode</span> valore numerico sotto forma di stringa (ad esempio, "13"). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> PSDK_ERROR</span> </td> 
   <td colname="col2"><span class="codeph"> com.adobe.mediacore.PSDKErrorCode</span> come stringa (ad esempio, <span class="codeph"> kECNetworkError</span>). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AVVISO</span> </td> 
   <td colname="col2"> Descrizione dell’avvertenza. </td> 
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
   <td colname="col2"> Errore minore dal modulo DRM. </td> 
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
   <td colname="col1"><b>Caricamento del manifesto dell’annuncio non riuscito</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_URL</span> </td> 
   <td colname="col2"> URL del contenuto che non è stato possibile caricare. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_TYPE</span> </td> 
   <td colname="col2">Tipo di annuncio (una costante del <span class="codeph"> MediaResource.Type</span> enum). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_DURATION</span> </td> 
   <td colname="col2"> Durata annuncio in millisecondi. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_ID</span> </td> 
   <td colname="col2"> ID assegnato all’annuncio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Errori di file</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DOWNLOAD_ERROR</span> </td> 
   <td colname="col2"> Descrizione dell'errore durante il download del file multimediale. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> URL</span> </td> 
   <td colname="col2"> URL del file da scaricare. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> MANIFEST_ERROR</span> </td> 
   <td colname="col2"> Descrizione dell'errore durante il download del file manifesto. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> CONTENT_ERROR</span> </td> 
   <td colname="col2">Descrizione dell’errore durante il frammento (ad esempio, <span class="codeph"> ts</span>) scarica. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Errori di traccia audio</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AUDIO_TRACK_NAME</span> </td> 
   <td colname="col2"> Nome della traccia audio non caricata, come specificato nel manifesto. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AUDIO_TRACK_LANGUAGE</span> </td> 
   <td colname="col2"> Lingua della traccia audio, come specificato nel manifesto. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Cerca errori</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DESIRED_SEEK_PERIOD</span> </td> 
   <td colname="col2"> ID del periodo (numero intero). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DESIRED_SEEK_POSITION</span> </td> 
   <td colname="col2"> <p>Posizione cercata (in millisecondi) (doppio). </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Varie</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AUDITUDE_ERROR_CODE</span> </td> 
   <td colname="col2"> Codice di errore di Auditude (numero). </td> 
  </tr> 
 </tbody> 
</table>

## NATIVE_ERROR: valori DRM {#section_D240082B93D34902A18C3923C1C717B3}

L&#39;interfaccia Video Encoder del motore video di Adobe restituisce queste notifiche DRM nel `NATIVE_ERROR` oggetto metadati.

Quando si segnalano gli errori DRM a Adobe, assicurarsi di includere `NATIVE_SUBERROR_CODE` e `DRM_ERROR_STRING` per assistenza nella risoluzione dei problemi.

>[!TIP]
>
>Questo elenco fornisce informazioni specifiche per TVSDK sugli errori. Per le descrizioni complete, vedi [Riferimento ActionScript per gli errori di runtime ActionScript per Adobe Flash Platform](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/runtimeErrors.html#3300).

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
     <li id="li_348FC0F38B11417994119B61C9244076">Quali sono le funzioni del software del distributore: 
      <ul id="ul_7AFD45CF92454BA4927783FAA628FBC4"> 
       <li id="li_0D9CCE61612643648C12DCDDD252E52A">Se utilizzi Google Chrome e sei in modalità di navigazione in incognito e la versione del Flash Player è inferiore a 11.6, questo errore potrebbe verificarsi. <p>Consigliamo al lettore di controllare il numero di versione del browser e consigliare all’utente di uscire dalla modalità in incognito. </p> </li> 
       <li id="li_1DC6B755BD0840D48BEC92568FD330BA">Richiedere nuovamente la licenza. <p>Se la richiesta ha esito positivo, non è necessario registrare o inoltrare la richiesta. Se la richiesta non ha esito positivo, registra il contenuto che ha causato l’errore. <span class="codeph"> subErrorId</span> se presente, contiene un errore di riga. </p> </li> 
      </ul> </li> 
     <li id="li_060B5D60C9BB419CBFA7B062FBCF2632">Cosa deve fare il distributore: 
      <ul id="ul_FADB29DBF0DA4A0E8E54134AEB7DCD8A"> 
       <li id="li_FC5B1C04D21E4AECB0EBD9ADD3198504">Se i nuovi tentativi non hanno esito positivo in configurazioni diverse da Chrome con Flash inferiore alla versione 11.6, potrebbe essersi verificato un errore nella confezione. </li> 
       <li id="li_A720ECE591254021879B335B81B1F76D">Verifica se il problema è specifico di un determinato contenuto e crea un nuovo pacchetto. </li> 
      </ul> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3301 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AuthenticationFailed</span> </td> 
   <td colname="col3"> <p>Autenticazione o autorizzazione del client non riuscita. </p> 
    <ul id="ul_BE77AC1848FB4C09B6318359ACF1B8EE"> 
     <li id="li_6FB37D317D174E8488C5070D20CD241C">Il software del distributore deve intraprendere tutte le azioni necessarie per ristabilire le credenziali dell'utente o guidare l'utente ad acquisire l'accesso al contenuto. </li> 
     <li id="li_BE071D59805B42D38E3E7650BC936417">Il distributore deve verificare che il meccanismo di autorizzazione e autenticazione del distributore funzioni correttamente. <p>Se i distributori non prevedono di utilizzare le funzioni di autenticazione o autorizzazione, devono verificare se la policy del contenuto offensivo richiede l’autenticazione e vedere Diagnostica delle discrepanze tra policy e licenze. </p> </li> 
    </ul> <p>Per ulteriori informazioni su questo codice di errore, vedi <a href="https://forums.adobe.com/thread/1277149" format="https" scope="external"> Cause e risoluzione dell'errore DRM 3301</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3302 </td> 
   <td colname="col2"><span class="codeph"> AAXS_RequireSSL</span> </td> 
   <td colname="col3"> <p>In Access 4.0 e versioni successive, questo errore viene generato in iOS quando l'URL della chiave remota non utilizza HTTPS come schema. HTTPS è obbligatorio. </p> 
    <ul id="ul_3D47777BBCA14B67B107FBBE3E37E40C"> 
     <li id="li_7F7BBB27AE754CC39ABAAF9269739C49">Se il distributore utilizza una versione precedente ad Access v4 o la versione almeno 4 ma la piattaforma non è iOS, il software del distributore dovrebbe registrare l’errore. <p>L’errore viene generato solo su iOS. </p> </li> 
     <li id="li_D83C427D2A0D47408F723EF7195070B6">Se il software del distributore è almeno Adobe Access versione 4 e la piattaforma è iOS, i distributori devono modificare l’URL del server della chiave remota che utilizzano in HTTPS. <p>Se utilizzavano solo HTTP, i distributori potrebbero dover impostare un server HTTPS. In caso contrario, i distributori devono inviare le informazioni registrate ad Adobe e inoltrare il problema. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3303 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ContentExpired</span> </td> 
   <td colname="col3"> <p>Il contenuto che stai visualizzando è scaduto in base alle regole impostate dal provider di contenuti. subErrorId contiene un errore specifico del client o un errore di riga. </p> <p> 
     <ul id="ul_1E4B3B8AE87A4E79997553BB2A0E52B9"> 
      <li id="li_EE3F2EEBF73743B9A38E4FCB7531E275">Il software del distributore deve tentare di riacquisire la licenza dal server una sola volta per determinare se è disponibile una nuova licenza non scaduta. <p>Se non è disponibile alcuna licenza o la licenza è scaduta, consentire all'utente di acquisire una nuova licenza o informare l'utente che il contenuto non può essere visualizzato.Se il contenuto è stato compilato con un criterio che ha una data di scadenza/fine, i registri del server licenze segnalano <span class="codeph"> Eccezione PolicyEvaluation</span> e dichiarano che la Data di fine del criterio è scaduta (codice di errore server 303). Controllare i file di registro del server per verificare. </p> <p>Se possibile, i clienti devono controllare la policy utilizzata durante la creazione dell’imballaggio per verificare se è scaduta. Lo strumento da riga di comando Java è: <code> java&nbsp;-jar&nbsp;libs/AdobePolicyManager.jar&nbsp;&nbsp;&nbsp;detail&nbsp;demo.pol</code> </p> </li> 
      <li id="li_50DBE680D8F04E7DA3E29C65A93188E7">Il distributore deve confermare se le date di scadenza della licenza sono configurate come previsto. </li> 
     </ul> </p> <p>Per ulteriori informazioni su questo codice di errore, vedi <a href="https://forums.adobe.com/thread/1300813" format="https" scope="external"> 3303 (Contenuto scaduto) con AMS/FMS che utilizza un Live Stream?</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3304 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AuthorizationFailed</span> </td> 
   <td colname="col3">Per ulteriori informazioni su questo codice di errore, vedi <a href="https://forums.adobe.com/thread/1277149" format="https" scope="external"> Cause e risoluzione dell'errore DRM 3301</a>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3305 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerConnectionFailed</span> </td> 
   <td colname="col3"> <p>Timeout della connessione ai server licenze o di dominio a causa di un ritardo della rete o della modalità offline del client. Normalmente subErrorId contiene codice di ritorno HTTP. </p> 
    <ul id="ul_938C7D8F07F64B4FA71A09DDF37E2E64"> 
     <li id="li_6648EA0049094E369BD9AE9CCA6B148D">Il software del distributore deve tentare una connessione di rete a un server funzionante. <p>Se il tentativo non riesce, richiedere all'utente di riconnettersi alla rete. Se il tentativo ha esito positivo, registralo. </p> </li> 
     <li id="li_2ECA2C04BA08449DA3AD79A52EFAA229">Il distributore deve verificare che tutte le licenze e i server di dominio in uso siano online e visibili dalla rete del client. </li> 
    </ul> <p>Per ulteriori informazioni su questo codice di errore, vedi <a href="https://forums.adobe.com/thread/1284947" format="https" scope="external"> DRM 3305 [ServerConnectionFailed] cause e risoluzione</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3306 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ClientUpdateRequire</span> </td> 
   <td colname="col3"> Utilizza una versione più recente di TVSDK per Android. <p>Il client corrente non è in grado di completare l'azione richiesta, ma un client aggiornato potrebbe essere in grado di completare la richiesta. </p> <p>Questo può avere diverse cause: 
     <ul id="ul_2EC4D42D5273439FA1AFDA1A2578B3D6"> 
      <li id="li_FCA926F5FAED4E7190BE855545AB6ACF">È stato utilizzato un dominio condiviso non disponibile in questo client. Questo è probabilmente il caso quando la riproduzione funziona su Chrome, ma non su qualsiasi altro browser e viceversa. <p> <p>Suggerimento: Chrome utilizza una chiave PHDS/PHLS diversa rispetto agli altri browser. Per ulteriori informazioni, consulta <a href="https://adobeprimetime.zendesk.com/agent/tickets/2891" format="https" scope="external"> https://adobeprimetime.zendesk.com/agent/tickets/2891</a>. </p> </p> </li> 
      <li id="li_3B633FB699234DCEA136E9BE3CC3386D">L’applicazione sta tentando di aggiungere più sessioni DRMS quando viene eseguita su una versione di iOS precedente alla 5.0. </li> 
      <li id="li_F7ED993AF0B941A7A27216B4D587A999">La versione dei metadati è 3 o successiva se è supportata solo la versione 2. </li> 
     </ul> </p> 
     <ul id="ul_EE4AE6AD4F1745A5B5623E53B599DB62"> 
      <li id="li_7A83869D4262443DA35FA1DF8D3097DD">Il software del distributore deve avvisare l'utente e interrompere l'operazione. <p>Se il software è in grado di determinare se un aggiornamento è disponibile, indirizzare l'utente a tale aggiornamento nel modo appropriato per la piattaforma. </p> </li> 
      <li id="li_AF9C2711FDE54DA196EB9D2864632000">Se il problema si verifica a causa di un dominio condiviso, il distributore dovrà verificare con Adobe se è disponibile una libreria o un runtime aggiornato. <p>Per il runtime di Flash, il distributore può forzare direttamente l’aggiornamento nella propria applicazione. Nel caso di una libreria, il distributore dovrà ottenere una libreria aggiornata, ricreare l’applicazione e distribuirla ai propri utenti. </p> <p>Se il problema si verifica a causa di più sessioni DRMS, il distributore dovrà aggiornare la propria applicazione per controllare il numero di versione di iOS prima di aggiungere più sessioni DRMS. Oppure possono limitare la distribuzione della loro applicazione ad iOS v5 e versioni successive. </p> <p>se il problema si verifica perché la versione dei metadati è successiva alla versione 2, è probabile che i metadati siano danneggiati. Possono provare a ricostruire i metadati e guardare i risultati. Se il problema persiste, segnalalo e passa all’Adobe. </p> </li> 
     </ul> <p>Per ulteriori informazioni su questo codice di errore, vedi <a href="https://forums.adobe.com/thread/1266675" format="https" scope="external"> Come risolvere un codice di errore DRMErrorEvent 3306</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3307 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InternalFailure</span> </td> 
   <td colname="col3"> <p>Questo in genere rappresenta un bug nel codice di accesso Adobe ed è imprevisto, a meno che non ci sia un bug noto, come di seguito. subErrorId contiene un errore specifico del client o un errore di riga. </p> 
    <ul id="ul_79F4A9655A2148519B1E9509C41F78C3"> 
     <li id="li_0E093AB4D6BD489B852279E6C1525A15">Se il browser è Chrome su Windows e la versione del Flash è 11.6 (SWF versione 19 o successiva), il software del distributore deve presupporre che l’utente abbia premuto <span class="uicontrol"> Rifiuta</span> sull’infobar e trattare come se fosse un 3368. </li> 
     <li id="li_0215D1089B344861A2C0A73E1067CFEF">Se si verifica 3307 quando il browser non è Chrome o la versione del Flash non è 11.6, il distributore deve effettuare l'escalation ad Adobe. </li> 
    </ul> <p>Importante: <span class="codeph"> 3307:1107296344 (FailedToGetBrokerHandle)</span> potrebbe verificarsi con le versioni 24-28 del browser Chrome. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3308 </td> 
   <td colname="col2"><span class="codeph"> AAXS_WrongLicenseKey</span> </td> 
   <td colname="col3"> <p>Questo errore viene generato ogni volta che la licenza in uso contiene la chiave errata per decrittografare il contenuto. subErrorId contiene un errore specifico del client o un errore di riga. </p> <p>Sembrano esserci solo due modi per generare questo bug: 
    <ul id="ul_1C955BD74C7843809D1B5A0CDCA5ED7B"> 
     <li id="li_18F0A7FDA6584887AD9DB3EDE54080D8">Il cliente ha modificato gli Adobi standard per la generazione di licenze (ad esempio, il framework Java del server concessionario di licenze). <p>In questo caso, la licenza contiene una chiave non valida che potrebbe non corrispondere ad alcun contenuto. </p> </li> 
     <li id="li_21D04ED1F1FA464785BC297D385766FF">Il cliente ha rilasciato più licenze con lo stesso ID licenza. <p>In questo caso, sul client sono disponibili più licenze che corrispondono ai metadati del contenuto e il codice di accesso ha selezionato quella errata per l’utilizzo. </p> </li> 
    </ul> </p> 
    <ul id="ul_64AEE62BE36946F290067CF475A36ECA"> 
     <li id="li_9EEB2B11A4DA41E78C5840D8FAA81F0D">Il software del distributore deve tentare di riacquistare la licenza dal server. 
      <ul id="ul_ACADC5518B054D0A853AEED2B675DB23"> 
       <li id="li_394835C8731048A5BF7D9370AC12448C">Se non è disponibile alcuna licenza o la licenza è scaduta, fornisci un flusso di lavoro che consenta all’utente di acquisire una nuova licenza, oppure informa l’utente che il contenuto non può essere guardato e segnala il problema. </li> 
       <li id="li_3FE50518BE53405F9563FA620F7EAD5F">Se si tratta di un contenuto associato a un dominio (per AIR), fornisci all’utente la possibilità di aggiungere il dominio. </li> 
      </ul> </li> 
     <li id="li_C80B353C1AEA4E9398241420CB491E84">Il distributore deve: 
      <ul id="ul_B5C50009374C4EED9B2B050B48F5F0F6"> 
       <li id="li_D5E6B760E0BC4B5C949ED1544B398838">Verificare che non siano state personalizzate le parti di rilascio delle licenze del server licenze di accesso. </li> 
       <li id="li_AA8F4E4B6DDD40BA8807C0920A92186B">Verificare che vengano rilasciati ID di licenza univoci per tutte le licenze. </li> 
       <li id="li_A2C53FE779AC4FDDB65E00A2C4F43EC4">Intensifica il problema con Adobe. </li> 
      </ul> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3309 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CorruptedAdditionalHeader </span> </td> 
   <td colname="col3"> <p>Ciò si verifica se l’intestazione è più grande di 65536 byte. </p> 
    <ul id="ul_82C0F688519B4F43A764D59A891F1903"> 
     <li id="li_E66AC9149A0649E88A79C5289C12C395">Il software del distributore dovrebbe registrare quale parte del contenuto ha causato l'errore. </li> 
     <li id="li_1C5916A33E7B4DC9968105B9BD20A727">Il distributore deve confermare che l’errore è riproducibile con parti specifiche di contenuto. Riconfezionare il contenuto danneggiato. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3310 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AppIDMismatch </span> </td> 
   <td colname="col3">L’applicazione Android non corrisponde a quella in uso. <p>L’applicazione AIR o Flash SWF corretta non è in uso. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3311 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AppVersionMismatch </span> </td> 
   <td colname="col3"> Non in uso. Questo problema potrebbe ancora essere generato dallo stack versione 1.x in AIR. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3312 </td> 
   <td colname="col2"><span class="codeph"> AAXS_LicenseIntegrity </span> </td> 
   <td colname="col3"> Per risolvere il problema, scaricare nuovamente la licenza dal server. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3313 </td> 
   <td colname="col2"><span class="codeph"> AAXS_WriteMicrosafeFailed </span> </td> 
   <td colname="col3"> <p>Questo problema si verifica quando il sistema non è in grado di scrivere nel file system. <span class="codeph"> subErrorId</span> contiene un errore specifico del client o un errore di riga. </p> <p>In Microsoft Windows, l’errore 3313 potrebbe essere generato da Active X o NPAPI Plug Flash Player quando il contenuto crittografato ha un licenseID o un policyID troppo lungo. Ciò è dovuto alla lunghezza massima del percorso in Windows. (Il plugin Pepper non ha questo problema.) </p> <p>Vedi 3549660 di Watson </p> 
    <ul id="ul_DFD527D1E1224A439766DF7BED878E3B"> 
     <li id="li_FAF8FD98A4E8478CA7A92F770676ADFC">Il software del distributore deve richiedere all'utente di confermare che la directory utente non è bloccata né su un volume pieno o bloccato. </li> 
     <li id="li_6D1136EA750A459BBECEEE5F73F527BB">Se il distributore utilizza AIR, anziché il Flash, il problema potrebbe essere causato da una limitazione della lunghezza del percorso. <p>I distributori devono abbreviare il nome della loro applicazione AIR in modo da indicare qualcosa di ragionevole. Inoltre, pubblica di nuovo i contenuti con un tag <span class="codeph"> licenseID</span> e un <span class="codeph"> policyID</span>. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3314 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CorruptedDRMMetadata </span> </td> 
   <td colname="col3"> <p>Questo errore indica spesso che il contenuto è stato compilato con certificati PKI di prova e che il lettore è stato compilato con PKI di produzione o viceversa. subErrorId contiene un errore specifico del client o un errore di riga. </p> 
    <ul id="ul_A122EF304CAF48A8B4DA1E3F4413E29B"> 
     <li id="li_A9A1A5B23E884C22A71E2DE7535FEB3B">Il software del distributore dovrebbe registrare quale parte del contenuto ha causato l'errore. </li> 
     <li id="li_7AD7F13A4B1B4998A7E49664E7645815">Il distributore deve confermare che l’errore è riproducibile con specifici contenuti. <p>Potrebbe essere necessario creare un nuovo pacchetto del contenuto danneggiato. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3315 </td> 
   <td colname="col2"><span class="codeph"> AAXS_PermissionDenied </span> </td> 
   <td colname="col3"> <p>Esistono bug noti in cui questo codice di errore viene generato quando si intende utilizzare un 3305. Per ulteriori informazioni, consulta <a href="https://forums.adobe.com/thread/1284947" format="https" scope="external"> DRM 3305 [ServerConnectionFailed] cause e risoluzione</a>. </p> <p>Il SWF remoto caricato da AIR non può accedere alle funzionalità di Flash Access. Questo codice di errore può essere generato anche se si verifica un errore di sicurezza durante l'accesso alla rete. Ad esempio, il server di destinazione non è il client a cui connettersi utilizzando il file crossdomain.xml oppure il file crossdomain.xml non è raggiungibile. </p> <p>Per ulteriori informazioni, consulta <a href="https://forums.adobe.com/thread/1266592" format="https" scope="external"> Errore DRM 3315, possibile causa principale e risoluzione</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3316 </td> 
   <td colname="col2"><span class="codeph"> AXS_NOTUSED_MOVE </span> </td> 
   <td colname="col3"> Era <span class="codeph"> ADOBECPSHIM_MinorErr_MissingAdobeCPModule</span>. Spostato a 3344 a causa di un conflitto con il codice di errore del Flash. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3317 </td> 
   <td colname="col2"><span class="codeph"> AAXS_LoadAdobeCPFailed non riuscito </span> </td> 
   <td colname="col3"> <p>Importante: si tratta di un errore raro che in genere non si verifica in un ambiente di produzione. </p> <p>Se l'errore si verifica, è possibile effettuare una delle seguenti operazioni: 
     <ul id="ul_BC435E61623444BB98A86216531DC892"> 
      <li id="li_FA433D0758B642D2AFDCF04906B3FE18">Se utilizzi AIR, reinstallalo. </li> 
      <li id="li_F08D9AAFF46244F8842DEE5FD9CBBE0A">Se si utilizza Flash Player, scaricare <span class="codeph"> AdobeCP</span> moduli. </li> 
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
   <td colname="col2"><span class="codeph"> AAXS_I15nNon riuscito </span> </td> 
   <td colname="col3"> <p>Il processo di provisioning del client con le chiavi non è riuscito. subErrorId contiene un errore di riga o specifico del client o del server. </p> 
    <ul id="ul_98D919B9060A441AACB6106F6D8E8DA7"> 
     <li id="li_DCAB00A8AC4A426CBBD377374B3F71AE">Il software del distributore deve ritentare l'operazione almeno una volta. <p>Se utilizzi Google Chrome su Windows, fornisci una spiegazione su come consentire l’accesso al plug-in che non è in una sandbox. Accesso alla sandbox di Google Chrome negato</a>. </p> </li> 
     <li id="li_7FB7681FE32D444BB1BDBA3E5953A2C3">Il distributore deve completare una delle seguenti attività: 
      <ul id="ul_486B64F187C44AE3B4775953A6142836"> 
       <li id="li_095B1D4CD051427CB2BFA7082B454056">Se l’errore è coerente tra le piattaforme, devi segnalare il problema con un Adobe. </li> 
       <li id="li_0C6EB7B912FA41E59657216498DA3515">Se l’errore è limitato a Chrome su Windows, indica all’utente di consentire l’accesso al plug-in non in modalità sandbox. </li> 
      </ul> <p>I distributori devono aggiornare il proprio SWF alla versione 19 o successiva e, in caso di errore Chrome-specifico 3321, viene generato un errore 3368. L'errore 3368 può essere gestito più specificamente dal software del distributore. Questa modifica è stata introdotta nella versione 26.0.1410.43 del canale stabile di Chrome. </p> <p>Suggerimento: errore <span class="codeph"> 3321:1090519056</span> potrebbe verificarsi con le versioni di Flash Player da 11.1 a 11.6. Si consiglia di eseguire l'aggiornamento alla versione più recente del Flash Player. </p> </li> 
    </ul> <p>Per ulteriori informazioni, consulta <a href="https://forums.adobe.com/thread/1277138" format="https" scope="external"> Errore DRM 3321 cause e risoluzione</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Errori di danneggiamento dell’archivio globale</b> </td> 
   <td colname="col2"> </td> 
   <td colname="col3"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3322 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DeviceBindingFailed </span> </td> 
   <td colname="col3"> <p>Il dispositivo non corrisponde alla configurazione presente al momento dell'inizializzazione. subErrorId contiene un errore di riga o specifico del client. </p> <p>Il software del distributore deve eseguire una delle seguenti operazioni: 
     <ul id="ul_444401051A2E407B95BC44491E9BB71C"> 
      <li id="li_93493EA05DB44CB1AEC368663F1ABA8D"> <p>Se il dispositivo non utilizza il Flash Player e utilizza AIR, iOS e così via, chiama <span class="codeph"> DRMManager.resetDRMVouchers()</span>. </p> <p>Se il problema si verifica su iOS in una fase di sviluppo, chiedi allo sviluppatore di confermare se il problema viene osservato quando si passa da una build scaricata da sistemi di distribuzione di terze parti pre-release (ad esempio, HockeyApp) a una build locale da Xcode. Gli attributi di un’installazione precedente non vengono completamente sovrascritti quando si passa da una build distribuita da HockeyApp a una build da Xcode. Questa situazione potrebbe attivare l'errore 3322. </p> <p>Per risolvere questo problema, lo sviluppatore deve rimuovere la build precedente dal dispositivo prima di installare la nuova build. </p> </li> 
      <li id="li_A5C9633F11584C788A2D9A23CC18FA6D">Se il dispositivo utilizza il Flash Player ed è inutilizzabile da codici di errore 3322 o 3346, vedere le istruzioni di Adobe relative alla reimpostazione programmatica dell'archivio licenze DRM <a href="https://forums.adobe.com/message/5535907#5535907" format="https" scope="external"> Errore DRM 3322/3346/3368 in Chrome (problemi della barra informazioni)</a>. </li> 
     </ul> </p> <p>Questo errore non dovrebbe verificarsi frequentemente. Negli ambienti aziendali che utilizzano profili in roaming, se un utente visualizzava contenuti protetti da DRM, la probabilità che si verifichi l’errore 3322 aumenta quando l’utente accede da computer diversi. Se possibile, il distributore deve cercare di ottenere queste informazioni dall'utente. </p> <p>Se l’errore si verifica frequentemente, passa a Adobe. È necessario notificare all'Adobe se il ripristino dell'archivio licenze ha risolto il problema o meno e indicare all'Adobe quali browser si è verificato l'errore. </p> <p>Per ulteriori informazioni, consulta i seguenti articoli: 
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
     <li id="li_D2693CD8EFEF46108828BA17E3F54FF6">Il software del distributore deve guidare l'utente a reimpostare nello stesso modo di 3322. </li> 
     <li id="li_0149B82436B64E28AC2B8C9B0EB09898">Se la frequenza degli errori del GlobalStore è superiore a quella prevista per i dischi rigidi della base utente, portare il problema all'Adobe. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3324 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MachineTokenInvalid </span> </td> 
   <td colname="col3"> Reimpostare l'archiviazione locale DRM per questa applicazione. Chiamare DRMManager.resetDRM. <p>È possibile che il server licenze non sia in grado di connettersi al server Elenco di revoche di certificati (CRL) per aggiornare i file CRL oppure che il computer client richieda una licenza o un'autenticazione revocata dal server licenze. </p> <p>Nei registri del server, il codice di errore 111 è MachineTokenInvalid. Tuttavia, a livello di client, il codice di errore 111 viene convertito nel codice di errore 3324. </p> <p>L'amministratore del server licenze DRM deve verificare se il server licenze del cliente è stato in grado di recuperare i file CRL di Adobe. Se il cliente utilizza Tomcat, può controllare<span class="filepath"> tomcat/temp/</span> per verificare se sono presenti 4 file CRL. </p> 
    <ul id="ul_23B7F1A104AF49E79EA87DB8E15E337E"> 
      <li id="li_855D87F251184FE688A8D5FA0F6C9EF5">Se i file si trovano in questa directory, fare doppio clic sui file in Esplora risorse e nell'applicazione del visualizzatore CRL, verificare se uno dei file è scaduto. </li> 
      <li id="li_58EC4EDA2B5146188A0FF7B33C91E2FD">Se in tomcat/temp/ non sono presenti file, si può supporre che questo server licenze non sia mai stato in grado di raggiungere il server CRL di Adobe a causa di un problema di firewall/routing. Per ulteriori informazioni, consulta <a href="https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_secure_deployment_guidelines.pdf" format="http" scope="external"> Regole del firewall.</a></li>
    </ul> </p> <p>Se i file CRL non sono disponibili o sono scaduti, è necessario confermare se è possibile raggiungere il server licenze. Aprire uno sniffer di rete sul server licenze del cliente, riavviare il server e richiedere a un client di richiedere una licenza al server. Puoi osservare il traffico di rete per verificare se le chiamate ai seguenti endpoint URL hanno esito positivo: <p>Suggerimento: puoi anche immettere i seguenti URL CRL in un browser per verificare se è possibile scaricare manualmente ogni file. </p> 
    <ul id="ul_9B65C7ABBDEC4AC9BF3755FFD3587971"> 
      <li id="li_6867A9050E8D421C9138AC853D1784C9"><a href="https://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl" format="http" scope="external"> crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl</a> </li> 
      <li id="li_6431689260554EAFAFDA2EC31798DCB5"><a href="https://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl" format="http" scope="external"> crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl</a> </li> 
      <li id="li_2939674D0F854ADEB67E45FD216288A2"><a href="https://crl2.adobe.com/Adobe/FlashAccessRootCA.crl" format="http" scope="external"> crl2.adobe.com/Adobe/FlashAccessRootCA.crl</a> </li> 
      <li id="li_96386E00BE9D4CB99D100057A5F7C6DD">crl3.adobe.com/AdobeSystemsIncorporated FlashAccessRuntime/LatestCRL.crl</li> 
    </ul> </p> <p>Se le regole del firewall sono aperte e non sono presenti errori 3324 correnti, potrebbe essersi verificato un problema di rete temporaneo. Controlla i registri del server del cliente, che sono probabilmente in <span class="codeph"> /tomcat/logs/</span> per determinare se si è verificato un errore quando il server licenze ha tentato di recuperare gli elenchi di revoche di certificati. <p>Importante: potrebbe verificarsi un errore quando un numero elevato (o un burst) di client segnala un errore 3324 a un problema di rete temporaneo durante il rinnovo di un file CRL. Quando il problema di rete è stato risolto, sono stati risolti anche i problemi 3324. </p> </p> <p>Se tutti e 4 i file CRL sono presenti in <span class="filepath"> tomcat/temp/</span> e i client ricevono ancora codici di errore 3324, potrebbero verificarsi problemi di accesso ai file CRL. Per risolvere il problema, è possibile esaminare i registri ed eliminare i file CRL esistenti. </p> <p>Se non si verificano problemi con il server, richiedere all'utente di eseguire la reimpostazione come descritto in 3322. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Errori di danneggiamento dell’archivio server</b> </td> 
   <td colname="col2"> </td> 
   <td colname="col3"> </td> 
</tr> 
  <tr> 
   <td colname="col1"> 3325 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CorruptServerStateStore </span> </td> 
   <td colname="col3"> <p>I file utilizzati dal client DRM sono stati modificati in modo imprevisto. <span class="codeph"> subErrorId</span> contiene un errore di riga o specifico per il client. </p> 
    <ul id="ul_860D2402DA61460AB0D938F1116F6D64"> 
     <li id="li_CF368C43452B4265B62ADA3E223894BA">Il software del distributore dovrebbe riprovare, poiché AdobeCP ha eliminato internamente l’archivio server problematico e un nuovo tentativo dovrebbe riuscire. Se il nuovo tentativo non riesce, segnala il problema. </li> 
     <li id="li_51A5803A1F754970BB4EBD6494F5DC96">Se i nuovi tentativi non riescono a una velocità superiore alla percentuale di errore prevista per i dischi rigidi della base utente, inoltra il problema ad Adobe. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3326 </td> 
   <td colname="col2"><span class="codeph"> AAXS_StoreTamperingDetected </span> </td> 
   <td colname="col3"> Chiamata <span class="codeph"> DRMManager.resetDRM</span>. <p>L’archivio licenze è stato manomesso/danneggiato e non può più essere utilizzato. </p> <p>Il software del distributore deve guidare l'utente a reimpostare nello stesso modo descritto in 3322. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3327 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ClockTamperingDetected </span> </td> 
   <td colname="col3"> Correggi l'orologio o acquisisci <span class="codeph"> Authn/Lic/Domain</span> di nuovo la licenza. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Errori server di autenticazione/licenza/dominio</b> </td> 
   <td colname="col2"> </td> 
   <td colname="col3"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3328 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerErrorTryAgain </span> </td> 
   <td colname="col3"> <p>Si tratta di un errore lato server in cui il server non è riuscito a completare la richiesta dal client. Questo errore può verificarsi quando, ad esempio, il server è occupato, HTTP/500, il server non dispone della chiave necessaria per decrittografare la richiesta e così via. </p> <p>Sul client non è possibile determinare cosa è andato storto. Il cliente deve rivedere i registri del server di accesso di Adobe, che in genere vengono chiamati <span class="codeph"> AdobeFlashAccess.log</span>, per determinare l'errore. Nel registro è sempre presente una traccia dello stack descrittiva per indicare il problema. <span class="codeph"> subErrorId</span> contiene un errore di riga o specifico per il server. </p> <p>Il distributore deve esaminare i registri del server per identificare quale server sta inviando questo errore. Per gli errori 3328 con codice di errore secondario 101, il server non può decrittografare la richiesta. Il cliente deve verificare che i certificati del server licenze/trasporto installati nel server licenze corrispondano e corrispondano ai certificati utilizzati durante la creazione del pacchetto. </p> <p>Inoltre, se i clienti utilizzano l’implementazione di riferimento, devono assicurarsi che non vi siano errori di battitura nel <span class="codeph"> flashaccess-refimpl.properties</span> file in cui sono specificati i certificati principali e aggiuntivi. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3329 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ApplicationSpecificError </span> </td> 
   <td colname="col3"> <p>Il codice di errore secondario specifico dell'applicazione non è noto al Flash Access. <span class="codeph"> subErrorId</span> contiene un errore specifico del server di licenze personalizzate per gli editori. Il server ha restituito un errore nello spazio dei nomi specifico dell'applicazione. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3330 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NeedAuthentication </span> </td> 
   <td colname="col3"> <p>Questo errore si verifica quando il contenuto è configurato per richiedere ai client di eseguire l’autenticazione prima di ottenere le licenze. </p> 
    <ul id="ul_712D29B8B5A6401FB014C4A283918E32"> 
     <li id="li_2D56905EB50D4FDEAD69CA8EAE38AD1A">Il software del distributore deve autenticare l'utente e quindi acquisire nuovamente la licenza. <p>Se il servizio non intende utilizzare l’autenticazione, registra l’identificazione del contenuto che sta causando questo errore. </p> </li> 
     <li id="li_B3BCF899B8BE41C7A4F7CF84B0503483">Questo errore non deve richiedere un'escalation, a meno che il contenuto non debba essere configurato per richiedere l'autenticazione. <p>In questo caso, crea un nuovo pacchetto del contenuto offensivo con le policy appropriate. Se il contenuto è confezionato correttamente, consulta Diagnostica delle discrepanze di criteri/licenze. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Errori di imposizione licenze non trattati in precedenza</b> </td> 
   <td colname="col2"> </td> 
   <td colname="col3"> </td> 
</tr> 
  <tr> 
   <td colname="col1"> 3331 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ContentNotYetValid </span> </td> 
   <td colname="col3"> <p>La licenza acquisita non è ancora valida. Per risolvere il problema, verificare che l'orologio del client non sia impostato correttamente. Per impostare l'orologio del client, ricompilare il contenuto o modificare la configurazione del server licenze. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3332 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CachedLicenseExpired </span> </td> 
   <td colname="col3"> Riacquisire la licenza dal server. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3333 </td> 
   <td colname="col2"><span class="codeph"> AAXS_PlaybackWindowExpired </span> </td> 
   <td colname="col3"> <p>È necessario avvisare gli utenti che non possono riprodurre questo contenuto fino alla scadenza del criterio. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3334 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidDRMPlatform </span> </td> 
   <td colname="col3"> <p>Questa piattaforma non è autorizzata a riprodurre il contenuto perché, ad esempio, il provider di contenuti ha configurato l’accesso Adobe per negare il contenuto all’accesso Adobe su una piattaforma oppure una licenza condivisa legata al dominio è associata a un token di dominio condiviso destinato a una partizione diversa. </p> <p>CDM potrebbe generare questo errore se il contenuto non è stato incluso in un pacchetto utilizzando una certificazione Packager appropriata (con funzionalità CDM gestita). </p> <p>Se il contenuto viene compilato con un certificato PHDS/PHLS errato, potrebbe funzionare in Chrome ma non in altri browser (o viceversa). <p>Suggerimento: Chrome utilizza certificati PHDS/PHLS diversi. </p>Per confermare il certificato utilizzato, dump i dettagli dei metadati del contenuto e cerca il <i>certificati dei destinatari</i>. Per ulteriori informazioni, consulta <a href="https://adobeprimetime.zendesk.com/agent/tickets/2891" format="https" scope="external"> https://adobeprimetime.zendesk.com/agent/tickets/2891</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3335 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidDRMVersion </span> </td> 
   <td colname="col3"> Effettua l’aggiornamento alla versione più recente di TVSDK per Android. <p>Per risolvere il problema, completa una delle seguenti attività: 
     <ul id="ul_BF1742948BC9461CB8686DE70124D3CD"> 
      <li id="li_690D440C94CC45A0AE55EC319B1C4C23">Aggiornare AIR </li> 
      <li id="li_CDD20251C881466E88BE7BBB53D61EBC">Ad Flash Player, aggiorna il modulo AdobeCP e riprova la riproduzione. </li> 
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
   <td colname="col3"> Effettua l’aggiornamento alla versione più recente di TVSDK per Android. <p>Ciò si verifica se il contenuto o il server è configurato per negare la riproduzione a una particolare versione del Flash o dei runtime di AIR. </p> 
    <ul id="ul_B0732D941256483CABBDD30C9BF43249"> 
     <li id="li_72782B1D638F48C0B87084689FB9C798">Se l'utente utilizza un Flash operativo in cui è possibile eseguire l'aggiornamento, il software del distributore deve richiedere all'utente di eseguire l'aggiornamento del Flash e riprovare. In caso contrario, consigliare all'utente di utilizzare un computer diverso. </li> 
     <li id="li_1E3FD93CE39E43F2B7D961299B1211DA">Se si sospetta l’errore 3337s, identifica se si verifica per contenuto specifico e crea un nuovo pacchetto di tale contenuto. Se il contenuto è stato compilato correttamente, consulta Diagnostica delle discrepanze tra criteri e licenze </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3338 </td> 
   <td colname="col2"><span class="codeph"> AAXS_UnknownConnectionType </span> </td> 
   <td colname="col3"> <p>Impossibile rilevare il tipo di connessione e il criterio richiede l'attivazione della protezione dell'output. Questo problema è previsto solo se il contenuto viene collocato per richiedere la protezione dell'uscita digitale o analogica. </p> <p>Un problema nelle versioni del Flash Player precedenti alla versione 11.8.800.168 ha causato occasionalmente l’errore 3338 nei contenuti per i quali i criteri indicavano che la protezione dei contenuti è <span class="codeph"> USA SE DISPONIBILE</span>. Questo problema è stato risolto nelle versioni 11.8.800.168 e successive. </p> 
    <ul id="ul_4B6CA26A53F84838B5B95400925464D4"> 
     <li id="li_CBD890F467E449EBB5116E1561252058">Il software del distributore sceglie una variante del contenuto che non richiede la protezione dell'uscita (ad esempio una variante SD di un flusso HD). <p>Se l’errore 3338 si verifica il <span class="codeph"> USE_IF_AVAILABLE </span> contenuto, verifica il numero di versione del lettore. Se la versione del lettore è precedente alla 11.8.800.168, consigliare all'utente di aggiornare il Flash Player. Se si verifica l’errore 3338 nelle versioni precedenti alla 11.8.800.168, registra il contenuto che ha causato l’errore. </p> </li> 
     <li id="li_62886C1D96264B129928A7E29E6C70E1">Il distributore deve verificare quale contenuto è la causa di questo errore e verificare che il criterio del contenuto sia impostato <span class="codeph"> NO_PROTECTION</span> o <span class="codeph"> USE_IF_AVAILABLE</span> per le uscite analogiche e digitali. <p>Se il contenuto viene involontariamente fornito con <span class="codeph"> NO_OUTPUT</span> o <span class="codeph"> OBBLIGATORIO</span>, crea un nuovo pacchetto del contenuto. Se il contenuto è stato compilato correttamente, consulta la sezione Diagnostica delle discrepanze tra criteri e licenze. In caso contrario, passa all'Adobe. </p> </li> 
    </ul> <p>Per ulteriori informazioni, consulta <a href="https://forums.adobe.com/message/5518688" format="https" scope="external"> Si verificano errori 3338 imprevisti quando i criteri DRM sono impostati su USE_IF_AVAILABLE?</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3339 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoAnalogPlaybackAllowed </span> </td> 
   <td colname="col3"> Impossibile riprodurre su una periferica analogica. Per risolvere il problema, collegare un dispositivo digitale. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3340 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoAnalogProtectionAvail </span> </td> 
   <td colname="col3"> Impossibile riprodurre il contenuto. La periferica di visualizzazione esterna analogica collegata (monitor/TV) non dispone delle funzionalità corrette (ad esempio, la periferica non dispone di Macrovision o ACP). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3341 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoDigitalPlaybackAllowed </span> </td> 
   <td colname="col3"> Impossibile riprodurre il contenuto su un dispositivo digitale. <p>Importante: questo problema non deve verificarsi in un ambiente di produzione, perché gli editori di contenuti non devono impedire la riproduzione digitale. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3342 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoDigitalProtectionAvail </span> </td> 
   <td colname="col3"> Il dispositivo di visualizzazione digitale esterno collegato (monitor/TV) non dispone delle funzionalità corrette. Ad esempio, il dispositivo non dispone di HDCP. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3343 </td> 
   <td colname="col2"><span class="codeph"> AAXS_IntegrityVerificationFailed </span> </td> 
   <td colname="col3"> <p>Non applicabile per Android. </p> <p>Questo errore si verifica inizialmente dopo il rilascio di una nuova versione del Flash. Ciò si verifica perché il Flash è stato aggiornato mentre il Flash era aperto, il che mette il Flash in uno stato errato fino al riavvio del browser. </p> 
    <ul id="ul_A0AC4A77550E40409A04BD33748EA987"> 
     <li id="li_F41C1ABD838D41ABB0DF65093E664A29">Il software del distributore deve completare le seguenti attività: 
      <ul id="ul_79B2AB1372074D448F129851AA24F985"> 
       <li id="li_B93EDD263D78434FAF198A01938D3508">Consiglia all’utente di chiudere o chiudere tutti i browser e quindi riaprire. </li> 
       <li id="li_ADFBCFA66AD849E18DB390455458528E">Verificare se la versione del Flash è corrente. <p>Se la versione non è corrente, consigliare al cliente di eseguire l'aggiornamento, chiudere tutte le schede nel browser e riaprire. </p> </li> 
      </ul> </li> 
     <li id="li_281B54582B5949AEA7D166246917EE41">Se dopo il riavvio del browser si verifica un errore, effettua un'escalation fino all'Adobe. <p>Quando viene rilasciata una nuova versione, ti consigliamo di contattare il supporto Adobe per verificare se il problema degli aggiornamenti in background è stato risolto. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3344 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MissingAdobeCPModule </span> </td> 
   <td colname="col3"> Non applicabile per Android. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3345 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DRMNoAccessError </span> </td> 
   <td colname="col3"> <p>Non applicabile per Android. </p> <p>Questo errore si verifica quando parte del Flash o AIR non è stata installata correttamente. </p> <p>Il software del distributore deve effettuare una delle seguenti operazioni: 
     <ul id="ul_D1188E2D4FDF4BD89A04F5629D75D981"> 
      <li id="li_B33FBCA5D4534D668B86A5E93DB3A809">Chiedere all'utente di disinstallare e reinstallare AIR. </li> 
      <li id="li_B7D2388E9FA84C26AF1C87B48AF9EF16">Per Flash Player, chiama <span class="codeph"> System.update</span>. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3346 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MigrationFailed </span> </td> 
   <td colname="col3"> 
    <ul id="ul_518AD4931CC64EB3A962DD451E6C5067"> 
     <li id="li_3C44F0740B08490E9C62D89C40B57DC2">Il software del distributore deve effettuare una delle seguenti operazioni: 
      <ul id="ul_7D90526684BF4EB2BBADCF598AA13086"> 
       <li id="li_D15B4BEDAF7340F6B9BC886DF6E346EC">Se AIR, chiama <span class="codeph"> DRMManager.resetDRMVouchers()</span> </li> 
       <li id="li_40A51D35408249CFA28DBC49FDA3408B">Se il Flash non è utilizzabile a causa di un codice di errore 3322 o 3346, gli utenti devono passare a <a href="https://forums.adobe.com/message/5535907#5535907" format="http" scope="external"> https://forums.adobe.com/message/5535907#5535907</a> e seguire le istruzioni dell'Adobe per reimpostare a livello di programmazione l'archivio licenze DRM. </li> 
      </ul> </li> 
     <li id="li_0464471E4A094C80BF2986694341921A">Se questo errore si verifica di frequente, il distributore deve fornire i dettagli sulla versione del lettore di frequenza e sulla versione del browser da Adobe. </li> 
    </ul> <p>Per ulteriori informazioni, consulta i seguenti articoli del forum: 
     <ul id="ul_44E0077FEAA749CC9549BF3846065304"> 
      <li id="li_2BE3B2443380415DA73B7AA3B6547B31"><a href="https://forums.adobe.com/message/5520902" format="https" scope="external"> Errore DRM 3322/3346/3368 in Chrome (problemi della barra informazioni)</a> </li> 
      <li id="li_4E5C7414756644E1AB78BE7B8112228C"><a href="https://forums.adobe.com/message/5535911" format="https" scope="external"> Errore 3322 o 3346 dopo la modifica dell'hardware</a> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3347 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InsufficienteDeviceCapabilites </span> </td> 
   <td colname="col3"> <p>Il significato principale di questo errore è che la licenza ha un vincolo che il certificato DRM dei client indica che non può soddisfare. Le seguenti "funzionalità hardware" vengono definite al momento dell'emissione del certificato DRM client: 
     <ul id="ul_1EB6F1469C244CF0BA52C212495C053D"> 
      <li id="li_646043CE045C4DE2BBC939E1F4963DFE"><b>Bus non accessibile all'utente</b>. Se <b>true</b>, i supporti decrittografati non scorrono mai attraverso un bus o nella memoria principale in cui un’applicazione può accedervi. <p>Se <b>false</b>, il contenuto potrebbe essere accessibile all'applicazione dopo la decrittografia. </p> </li> 
      <li id="li_02AAECAF4D35447BA10554541B46DE67"><b>Directory principale hardware attendibile</b>. Se <b>true</b>, tutto il software caricato al momento dell'avvio sul dispositivo è stato convalidato in base a una chiave o a un digest disponibile solo nell'hardware. <p>Entrambi questi vincoli vengono controllati sul lato client quando la licenza viene aperta rispetto al certificato DRM per il client e l'errore è immediato. Questi vincoli possono essere controllati anche sul lato server prima di rilasciare la licenza. </p> </li> 
     </ul> </p> <p>Il significato secondario di questo errore è che la licenza ha il criterio "Jailbreak Enforcement" impostato e un jailbreak è stato rilevato sul dispositivo. Questo controllo viene eseguito periodicamente sul lato client e non può essere controllato sul lato server. </p> <p>I distributori possono aggiornare i criteri e rimuovere le restrizioni. Per i criteri di funzionalità per dispositivi, esegui il comando di aggiornamento dei criteri con <span class="codeph"> -devCapabilitiesV1</span> flag e nessun argomento. Per l'applicazione jailbreak, impostare <span class="codeph"> policy.enforceJailbreak=false</span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3348 </td> 
   <td colname="col2"><span class="codeph"> AAXS_HardStopIntervalExpired </span> </td> 
   <td colname="col3"> Intervallo di arresto rigido scaduto. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3349 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerVersionTooHigh </span> </td> 
   <td colname="col3"> Il server è in esecuzione con una versione superiore a quella supportata dal client. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3350 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerVersionTooLow </span> </td> 
   <td colname="col3"> Il server è in esecuzione con una versione inferiore alla versione minima supportata dal client. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3351 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainTokenInvalid </span> </td> 
   <td colname="col3"> Token di dominio non valido. Per risolvere questo problema, registrati di nuovo con il dominio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3352 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainTokenTooOld </span> </td> 
   <td colname="col3"> Il token di dominio è più vecchio del token richiesto dalla licenza. Per risolvere il problema, registrati di nuovo con il dominio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3353 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainTokenTooNew </span> </td> 
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
   <td colname="col3"> Aggiunta al dominio non riuscita. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3356 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoCorrespondingRoot </span> </td> 
   <td colname="col3"> Impossibile trovare una licenza radice per una licenza foglia V3. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3357 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoValidEmbeddedLicense </span> </td> 
   <td colname="col3"> Impossibile trovare una licenza incorporata valida. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3358 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoACPProtectionAvail </span> </td> 
   <td colname="col3"> Impossibile riprodurre. La periferica analogica collegata non dispone della protezione ACP. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3359 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoCGMSAProtectionAvail </span> </td> 
   <td colname="col3"> Impossibile riprodurre. La periferica analogica collegata non dispone della protezione CGMS-A. </td> 
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
   <td colname="col3"> L'operazione asincrona ha richiesto più tempo del <span class="codeph"> maxOperationTimeout</span>. Restituisce solo iOS DRMNative Framework. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3363 </td> 
   <td colname="col2"><span class="codeph"> AAXS_UnsupportedIOSPlaylistError </span> </td> 
   <td colname="col3"> La playlist M3U8 trasmessa conteneva contenuti non supportati. Restituisce solo iOS DRMNative Framework. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3364 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoDeviceId </span> </td> 
   <td colname="col3"> <p>Il framework ha richiesto l'ID dispositivo, ma il valore restituito è vuoto. </p> <p>L’utente non deve selezionare <span class="uicontrol"> Consenti identificatori per contenuto protetto</span> in Chrome. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3365 </td> 
   <td colname="col2"><span class="codeph"> AAXS_IncognitoModeNotAllowed </span> </td> 
   <td colname="col3"> <p>Questa combinazione browser/piattaforma non consente la riproduzione protetta da DRM in modalità di navigazione in incognito. </p> <p>Il software del distributore deve consigliare all'utente di uscire dalla modalità in incognito o di utilizzare un browser diverso. Per ulteriori informazioni, consulta <a href="https://forums.adobe.com/thread/1266622" format="https" scope="external"> Causa e risoluzione errore DRM 3365</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3366 </td> 
   <td colname="col2"><span class="codeph"> AAXS_BadParameter </span> </td> 
   <td colname="col3"> <p>Il runtime host ha chiamato la libreria di Access con un parametro non valido. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3367 </td> 
   <td colname="col2"><span class="codeph"> AAXS_BadSignature </span> </td> 
   <td colname="col3"> firma del manifesto m3u8 non riuscita. Restituito solo da iOS DRMNative Framework o AVE. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3368 </td> 
   <td colname="col2"><span class="codeph"> AAXS_UserSettingsNoAccess</span> </td> 
   <td colname="col3"> <p>L’utente ha annullato l’operazione o ha immesso impostazioni che impediscono l’accesso al sistema. </p> <p>Questo errore viene generato solo quando la versione di SWF è 19 o successiva. Per compatibilità con le versioni precedenti, 3321 viene generato quando il SWF è versione 18 o precedente. </p> <p>Il software del distributore deve guidare l'utente a una spiegazione di come consentire l'accesso al plug-in non in modalità sandbox. Accesso alla sandbox di Google Chrome negato</a> e <a href="https://forums.adobe.com/message/5520902" format="https" scope="external"> Errore DRM 3322/3346/3368 in Chrome (problemi della barra informazioni)</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3369 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InterfaceNotAvailable</span> </td> 
   <td colname="col3"> <p>Interfaccia browser richiesta non disponibile. Questo problema si verifica solo su Pepper. Potrebbe esserci una mancata corrispondenza tra il plug-in del Flash e la versione del browser. </p> <p>Il software del distributore deve guidare l'utente ad assicurarsi che abbia installato la versione più recente del browser. </p> <p> Se le incidenze di questo errore aumentano e corrisponde al rilascio di un aggiornamento del browser, effettua un inoltro a Adobe. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3370 </td> 
   <td colname="col2"><span class="codeph"> AXS_ContentIdSettingsNoAccess</span> </td> 
   <td colname="col3"> <p>L'utente ha disabilitato <span class="uicontrol"> Consenti identificatori per contenuto protetto</span> impostazione. </p> <p>Suggerimento: questo errore viene visualizzato con Pepper versione 13.0.0.x o successiva. </p> <p>Il software del distributore deve guidare l'utente nell'abilitazione <span class="uicontrol"> Consenti identificatori per contenuto protetto</span> impostazione. </p> <p>Il team operativo del distributore deve guidare l'utente nell'abilitazione <span class="uicontrol"> Consenti identificatori per contenuto protetto</span> impostazione. </p> <p>Per ulteriori informazioni, consulta <a href="https://forums.adobe.com/message/6518323#6518323" format="https" scope="external"> https://forums.adobe.com/message/6518323#6518323</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3371 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoOPConstraintInPixel</span><span class="codeph"> Vincoli</span> </td> 
   <td colname="col3"> <p>Risoluzione non valida in base ai vincoli di protezione dell'output nella licenza. </p> <p>Il software del distributore dovrebbe mostrare un messaggio di errore. Chiedere all’utente di segnalare il problema al distributore con un titolo di contenuto. </p> <p>Il distributore deve ricompilare il contenuto con un criterio valido. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3372 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ResolutionLargerThanMaxResolution</span> </td> 
   <td colname="col3"> <p>La risoluzione del contenuto è maggiore della risoluzione massima specificata nel vincolo di protezione dell'output. </p> <p>Se il team operativo del distributore rileva questo errore nei propri registri, deve rivedere il criterio di protezione dell’output basato sulla risoluzione e, se necessario, riconfezionare il contenuto. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3373 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MinorErr_DisplayResolutionLargerThanConstrain</span> </td> 
   <td colname="col3"> <p>La risoluzione del contenuto è maggiore della risoluzione specificata dal vincolo di protezione dell'output attualmente attivo. </p> <p>Se il team operativo del distributore rileva questo errore nei propri registri, deve rivedere il criterio di protezione dell’output basato sulla risoluzione e, se necessario, riconfezionare il contenuto. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3374 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MinorErr_ClientCommProcessFailed</span> </td> 
   <td colname="col3"> <p>Errore durante l’elaborazione delle comunicazioni lato client, ad esempio generazione di richieste, elaborazione di risposte, token di autenticazione non valido e così via. </p> <p>Se il team operativo del distributore rileva questo errore nei propri registri, deve rivedere il criterio di protezione dell’output basato sulla risoluzione e, se necessario, riconfezionare il contenuto. </p> </td> 
  </tr> 
 </tbody> 
</table>

## NATIVE_ERROR: valori di riproduzione video {#section_7079501250C2487499639F92EC774525}

L&#39;interfaccia Video Encoder di AVE restituisce queste notifiche di riproduzione video nel `NATIVE_ERROR` oggetto metadati.

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
   <td colname="col2"><span class="codeph"> FINE_PERIODO</span> </td> 
   <td colname="col3"> Fine del periodo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 0 </td> 
   <td colname="col2"><span class="codeph"> OPERAZIONE RIUSCITA</span> </td> 
   <td colname="col3"> Operazione completata. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 1 </td> 
   <td colname="col2"> <span class="codeph"> ASYNC_OPERATION_IN_PROGRESS</span> </td> 
   <td colname="col3"> Operazione asincrona. La richiesta di operazione è stata effettuata. Le informazioni di successo/errore saranno disponibili in seguito. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 2 </td> 
   <td colname="col2"><span class="codeph"> EOF</span> </td> 
   <td colname="col3"> Operazione non possibile a causa della condizione di fine file (EOF). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3 </td> 
   <td colname="col2"><span class="codeph"> DECODER_FAILED</span> </td> 
   <td colname="col3"> Errore del decodificatore in fase di esecuzione. </td> 
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
   <td colname="col3"> Condizione di errore da cui il motore video non può essere ripristinato. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 8 </td> 
   <td colname="col2"><span class="codeph"> LOST_CONNECTION_RECOVERY </span> </td> 
   <td colname="col3"> Errore di rete, tentativo di ripristino in corso. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 9 </td> 
   <td colname="col2"><span class="codeph"> NO_FIXED_SIZE </span> </td> 
   <td colname="col3"> Impossibile determinare la dimensione della risorsa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 10 </td> 
   <td colname="col2"><span class="codeph"> NOT_IMPLEMENTATO </span> </td> 
   <td colname="col3"> Funzionalità non implementata. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 11 </td> 
   <td colname="col2"><span class="codeph"> MEMORIA_ESAURITA </span> </td> 
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
   <td colname="col3"> Operazione consentita solo se in pausa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 21 </td> 
   <td colname="col2"><span class="codeph"> OP_INVALID_WITH_AUDIO_ONLY_FILE</span> </td> 
   <td colname="col3"> Impossibile utilizzare l'operazione su file solo audio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 22 </td> 
   <td colname="col2"><span class="codeph"> PREVIOUS_STEP_SEEK_IN_PROGRESS</span> </td> 
   <td colname="col3"> L’operazione di ricerca precedente è ancora in corso. </td> 
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
   <td colname="col2"><span class="codeph"> RETE_NON DISPONIBILE</span> </td> 
   <td colname="col3"> Rete non disponibile. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 33 </td> 
   <td colname="col2"><span class="codeph"> ERRORE_DI_RETE</span> </td> 
   <td colname="col3"> Errore nell’ottenere dati dalla rete. </td> 
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
   <td colname="col3"> Tentativo di operazione su un periodo di blocco o su un periodo non ancora caricato. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 37 </td> 
   <td colname="col2"><span class="codeph"> INVALID_REPLACE_DURATION</span> </td> 
   <td colname="col3"> La durata di sostituzione specificata non è valida o si estende oltre la fine del flusso. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 38 </td> 
   <td colname="col2"><span class="codeph"> CHIAMATO_DA_SBAGLIATO_THREAD</span> </td> 
   <td colname="col3"> Impossibile chiamare l'API dal thread errato. Principalmente, per gli elementi API che devono essere chiamati solo dal thread principale. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 39 </td> 
   <td colname="col2"><span class="codeph"> FRAGMENT_READ_ERROR</span> </td> 
   <td colname="col3"> Errore di lettura del frammento. Nessun failover presente. Il motore proverà a leggere il frammento successivo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 40 </td> 
   <td colname="col2"><span class="codeph"> INTERROTTO</span> </td> 
   <td colname="col3"> Operazione interrotta da una chiamata di interruzione o eliminazione esplicita. </td> 
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
   <td colname="col3"> La connessione di rete dell'utente non è attiva. La riproduzione potrebbe interrompersi in qualsiasi momento e riprenderà quando la connessione sarà disponibile. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 45 </td> 
   <td colname="col2"><span class="codeph"> NO_USABLE_BITRATE_PROFILE</span> </td> 
   <td colname="col3"> Nessun profilo di velocità in bit utilizzabile trovato nel flusso. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 46 </td> 
   <td colname="col2"><span class="codeph"> BAD_MANIFEST_SIGNATURE</span> </td> 
   <td colname="col3"> Il manifesto ha una firma non valida. Il test della firma del manifesto non è riuscito. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 47 </td> 
   <td colname="col2"><span class="codeph"> IMPOSSIBILE_CARICARE_PLAYLIST</span> </td> 
   <td colname="col3"> Impossibile caricare una playlist. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 48 </td> 
   <td colname="col2"><span class="codeph"> REPLACEMENT_FAILED</span> </td> 
   <td colname="col3"> Impossibile eseguire la sostituzione specificata in un'API di inserimento. Ciò significa che l'inserimento è riuscito, ma la sostituzione non è riuscita. La sostituzione potrebbe non riuscire se il manifesto da sostituire è stato rimosso dalla timeline. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 49 </td> 
   <td colname="col2"><span class="codeph"> SWITCH_TO_AYMMETRIC_PROFILE</span> </td> 
   <td colname="col3"> DRM sta passando a un profilo asimmetrico. È previsto che tutti i profili siano allineati in durata. In caso contrario, verrà visualizzato questo avviso e potrebbero verificarsi salti nella riproduzione. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 50 </td> 
   <td colname="col2"><span class="codeph"> LIVE_WINDOW_MOVE_BACKWARD</span> </td> 
   <td colname="col3"> La finestra Live deve essere spostata solo in avanti. In caso contrario, questo avviso verrà generato e la finestra non verrà letta. Per questo motivo, potrebbero verificarsi salti (o pause lunghe/di arresto) nella riproduzione. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 51 </td> 
   <td colname="col2"><span class="codeph"> CURRENT_PERIOD_EXPIRED</span> </td> 
   <td colname="col3"> La finestra Live è stata spostata oltre il periodo corrente. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 52 </td> 
   <td colname="col2"><span class="codeph"> CONTENT_LENGTH_MISMATCH</span> </td> 
   <td colname="col3"> La lunghezza del contenuto segnalata dal server HTTP non corrisponde alla dimensione effettiva del file multimediale. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 53 </td> 
   <td colname="col2"><span class="codeph"> PERIOD_HOLD</span> </td> 
   <td colname="col3"> Il lettore multimediale non è in grado di leggere ulteriormente perché ha raggiunto l’ora impostata dall’API setHoldAt. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 54 </td> 
   <td colname="col2"><span class="codeph"> LIVE_HOLD </span> </td> 
   <td colname="col3">Il lettore multimediale non è in grado di caricare i segmenti perché ha raggiunto la fine della finestra live. Il caricamento del segmento riprenderà quando il server aggiunge nuovi file multimediali alla finestra live. Questo stato viene generalmente raggiunto se: 
    <ul id="ul_FCFF658EDA4144E59970B317D6DEB624"> 
     <li id="li_2F6EEEB782D54CD999BC7CC7C0B78B48">Il <span class="codeph"> bufferTime</span> è troppo alto (uguale o superiore alla durata della finestra live). </li> 
     <li id="li_25CE97115ED64E44AA89977FB5F0DCF7">Una combinazione di una o più API di inserimento/cancellazione ha sostituito più supporti di quelli aggiunti. </li> 
     <li id="li_1B14716B2157492AB1859306D1250523">Il periodo successivo è un periodo live con una sostituzione dei contenuti multimediali in sospeso (a causa della chiamata API InsertBy) </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 55 </td> 
   <td colname="col2"><span class="codeph"> BAD_MEDIA_INTERLEAVING </span> </td> 
   <td colname="col3"> L'interfoliazione audio e video nel supporto non viene eseguita correttamente. Si tratta di un errore di packaging. L’avviso viene inviato quando la differenza supera i due secondi. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 56 </td> 
   <td colname="col2"><span class="codeph"> DRM_NOT_AVAILABLE</span> </td> 
   <td colname="col3"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 57 </td> 
   <td colname="col2"><span class="codeph"> PLAYBACK_NOT_AUTHORIZED</span> </td> 
   <td colname="col3"> La riproduzione HLS non è stata abilitata nel Flash Player. Consulta AuthorizedFeatures.enableHLSPlayback. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 58 </td> 
   <td colname="col2"><span class="codeph"> BAD_MEDIA_SAMPLE_FOUND</span> </td> 
   <td colname="col3"> Il decodificatore ha ricevuto un campione non valido che non può essere decodificato. In genere non si tratta di un errore irreversibile, ma indica che potrebbero verificarsi errori nell’audio/video. Troppe istanze di questo errore indicano una codifica non valida o un file non valido. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 59 </td> 
   <td colname="col2"><span class="codeph"> RANGE_SPANS_READ_HEAD</span> </td> 
   <td colname="col3"> Dopo l'avvio della riproduzione, l'intervallo Inserisci/Sostituisci non deve contenere l'intestazione di lettura. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 60 </td> 
   <td colname="col2"><span class="codeph"> POSTROLL_WITH_LIVE_NOT_ALLOWED</span> </td> 
   <td colname="col3"> Gli inserimenti post-roll non sono consentiti nei file multimediali live. Sono tuttavia consentiti dopo che il server ha contrassegnato il supporto come completo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 61 </td> 
   <td colname="col2"><span class="codeph"> INTERNAL_ERROR</span> </td> 
   <td colname="col3"> Un problema molto raro che non dovrebbe mai accadere. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 62 </td> 
   <td colname="col2"><span class="codeph"> SPS_PPS_FOUND_OUTSIDE_AVCC</span> </td> 
   <td colname="col3"> Il flusso non segue la raccomandazione di imballaggio di inserire sempre H264 SPS/PPS in un AVCC. Potrebbero essere visualizzati problemi di ricerca/riproduzione. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 63 </td> 
   <td colname="col2"><span class="codeph"> PARZIALE_SOSTITUZIONE</span> </td> 
   <td colname="col3"> La sostituzione specificata in un’API di inserimento è stata eseguita solo parzialmente. Ciò si verifica quando replaceDuration si estende sulla durata della sequenza temporale. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 64 </td> 
   <td colname="col2"><span class="codeph"> RAPPRESENTAZIONE_M3U8_ERROR</span> </td> 
   <td colname="col3"> Errore durante il caricamento della playlist della rappresentazione. Questo è solo per AVE, non per FlashPlayer. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 65 </td> 
   <td colname="col2"><span class="codeph"> NULL_OPERATION</span> </td> 
   <td colname="col3"> L'operazione non esegue alcuna operazione. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 66 </td> 
   <td colname="col2"><span class="codeph"> SEGMENT_SKIPPED_ON_FAILURE</span> </td> 
   <td colname="col3"> Il segmento non può essere riprodotto e viene saltato in caso di errore. </td> 
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
   <td colname="col3"> Impossibile eseguire un'operazione di divisione su una sequenza temporale. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 72 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_ERASE_TIMELINE</span> </td> 
   <td colname="col3"> Impossibile eseguire un'operazione di cancellazione su una sequenza temporale. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 73 </td> 
   <td colname="col2"><span class="codeph"> DID_NOT_GET_NEXT_FRAGMENT</span> </td> 
   <td colname="col3"> Impossibile ottenere il frammento successivo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 74 </td> 
   <td colname="col2"><span class="codeph"> NO_TIMELINE</span> </td> 
   <td colname="col3"> Nessuna timeline presente in una struttura di dati interna. </td> 
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
   <td colname="col3"> Nessun sink audio presente in una struttura di dati interna. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 78 </td> 
   <td colname="col2"><span class="codeph"> FILE_OPEN_ERROR</span> </td> 
   <td colname="col3"> Impossibile aprire il file. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 79 </td> 
   <td colname="col2"><span class="codeph"> FILE_WRITE_ERROR</span> </td> 
   <td colname="col3"> Impossibile scrivere su un file. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 80 </td> 
   <td colname="col2"><span class="codeph"> FILE_READ_ERROR</span> </td> 
   <td colname="col3"> Impossibile leggere da un file. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 81 </td> 
   <td colname="col2"><span class="codeph"> ID3PARSE_ERROR</span> </td> 
   <td colname="col3"> Errore nell’analisi dei dati ID3. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 82 </td> 
   <td colname="col2"><span class="codeph"> SECURITY_ERROR </span> </td> 
   <td colname="col3"> Caricamento del contenuto non riuscito a causa di restrizioni di protezione. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 83 </td> 
   <td colname="col2"><span class="codeph"> TIMELINE_TOO_SHORT</span> </td> 
   <td colname="col3"> La durata della sequenza temporale è troppo breve. Se si tratta di un flusso live, può verificarsi un buffering frequente. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 84 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_ONLY_STREAM_START</span> </td> 
   <td colname="col3"> Lo streaming è stato convertito in streaming solo audio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 85 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_ONLY_STREAM_END</span> </td> 
   <td colname="col3"> Lo streaming è stato cambiato da "solo audio" a "video". </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 87 </td> 
   <td colname="col2"><span class="codeph"> CHIAVE_NON_TROVATA </span> </td> 
   <td colname="col3"> Impossibile trovare la chiave. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 88 </td> 
   <td colname="col2"><span class="codeph"> INVALID_KEY</span> </td> 
   <td colname="col3"> Chiave non valida. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 89 </td> 
   <td colname="col2"> <span class="codeph"> KEY_SERVER_NOT_FOUND</span> </td> 
   <td colname="col3"> Il server chiavi non restituisce alcuna chiave. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 90 </td> 
   <td colname="col2"> <span class="codeph"> MAIN_MANIFEST_UPDATE_TO_BE_HANDLED</span> </td> 
   <td colname="col3"> Impossibile gestire l'aggiornamento del manifesto principale. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 91 </td> 
   <td colname="col2"> <span class="codeph"> UNREPORTS_TIME_DISCONTINUITY_FOUND</span> </td> 
   <td colname="col3"> È stata rilevata una discontinuità nell’ora non segnalata (PTS). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 92 </td> 
   <td colname="col2"> <span class="codeph"> UNMATCHED_AV_DISCONTINUITY_FOUND</span> </td> 
   <td colname="col3"> È stata rilevata una discontinuità audio e video senza corrispondenza. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 93 </td> 
   <td colname="col2"><span class="codeph"> TRICKPLAY_ENDED_DUE_TO_ERROR</span> </td> 
   <td colname="col3">Si è verificato un errore durante la riproduzione del contenuto multimediale in <i>riproduzione con trucco</i> modalità. La modalità di riproduzione dei brani viene terminata e il flusso viene messo in pausa. Chiamata <span class="codeph"> Play()</span> per riprodurre il supporto in modalità normale. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 95 </td> 
   <td colname="col2"><span class="codeph"> LIVE_WINDOW_MOVE_AHEAD</span> </td> 
   <td colname="col3"> Il giocatore è fuori dalla finestra dal vivo e deve cercare in avanti per recuperare. </td> 
  </tr> 
 </tbody> 
</table>

## NATIVE_ERROR: Crittografia dei valori {#section_39365E545CAC49B9A4D4678657BB2155}

Il modulo di crittografia del motore video Adobe restituisce queste notifiche nel `NATIVE_ERROR` oggetto metadati.

| **Valore per la chiave di metadati NATIVE_ERROR_CODE** | **Valore per la chiave di metadati NATIVE_ERROR_NAME** | **Significato** |
|---|---|---|
| 300 | `CRYPTO_ALGORITHM_NOT_SUPPORTED` | L’algoritmo in uso non è supportato. |
| 301 | `CRYPTO_ERROR_CORRUPTED_DATA` | Dati danneggiati. |
| 302 | `CRYPTO_ERROR_BUFFER_TOO_SMALL` | Buffer troppo piccolo. |
| 303 | `CRYPTO_ERROR_BAD_CERTIFICATE` | Certificato non valido. |
| 304 | `CRYPTO_ERROR_DIGEST_UPDATE` | Aggiornamento digest. |
| 305 | `CRYPTO_ERROR_DIGEST_FINISH` | Fine digest. |
| 306 | `CRYPTO_ERROR_BAD_PARAMETER` | Parametro non valido. |
