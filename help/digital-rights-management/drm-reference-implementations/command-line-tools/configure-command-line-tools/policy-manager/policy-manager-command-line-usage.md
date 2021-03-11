---
title: Utilizzo della riga di comando di Policy Manager
description: Utilizzo della riga di comando di Policy Manager
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '1226'
ht-degree: 0%

---


# Utilizzo della riga di comando di Policy Manager {#policy-manager-command-line-usage}

```
java -jar AdobePolicyManager.jar  
<i class="+ topic ph hi-d="" i "="">
  command filename [options] 
</i class="+ topic>
```

**Tabella 1: Comandi**

| Comando | Descrizione |
|---|---|
| `new` | Crea un nuovo criterio DRM |
| `detail` | Descrive un criterio DRM esistente |
| `update` | Aggiorna i criteri DRM esistenti |

**Tabella 2: Opzioni**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_q5h_cpy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Opzione della riga di comando </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descrizione </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c file di configurazione  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica il nome e il percorso del file di configurazione. </p> <p class="- topic/p ">Se non si specifica un nome o una posizione, DRM Policy Manager cerca <span class="filepath"> flashaccesstools.properties </span> nella directory di lavoro corrente. </p> <p>Nota:  Le opzioni specificate nella riga di comando hanno la precedenza sulle opzioni specificate nel file di configurazione. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se il file di destinazione esiste, puoi sovrascrivere il file senza che venga richiesto di farlo. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Non chiedere se il file di destinazione deve essere sovrascritto. Se il file di destinazione esiste e <span class="codeph"> -o </span> non è impostato, si verifica un errore. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -root  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica che il criterio DRM dispone di una licenza radice. </p> <p class="- topic/p ">Questa opzione non è disponibile per gli aggiornamenti. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e data  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La data prima della validità delle licenze. </p> <p>È possibile specificare la data in formato <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-gg </span> o <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-gg-h24:min:sec </span>. Ad esempio, 2008-12-1 o 2008-12-1-00:00:00 per la mezzanotte del 1° dicembre 2008. </p> <p> 
     <ul id="ul_D5DB5044756D4BD6A734813971598425"> 
      <li id="li_B6BD62A524384060A9DDA14FF50936FA">Il valore deve essere maggiore del valore di <span class="codeph"> -s </span> se presente. </li> 
      <li id="li_C3C5AD0231A240EC9AC57685B9206E8D">Non è possibile applicare questa opzione con <span class="codeph"> -r </span>. </li> 
      <li id="li_3790E2F829A149979BF44E0914CFF431">Per rimuovere la data di fine quando si aggiorna un criterio DRM, applicare <span class="codeph"> -e </span> senza specificare una data. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r minuti  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Durata in minuti della validità del contenuto protetto. </p> <p class="- topic/p ">Il criterio DRM diventa valido quando il contenuto è protetto con il packager. </p> <p> 
     <ul id="ul_4690A0E4677A4DF6A006B7FCBD46F1BE"> 
      <li id="li_D1F098D44B494EE7A8647C0B62D5ACFA">Il valore deve essere non negativo. </li> 
      <li id="li_ADFDCB01EEE04B37AFA42886AAEF47EB">Non è possibile applicare questa opzione insieme a <span class="codeph"> -e </span>. </li> 
      <li id="li_E80563E68BEB43FC9E29A694594CAE01">Per rimuovere o eliminare la durata quando si aggiorna un criterio DRM, applicare <span class="codeph"> -r </span> senza specificare alcun minuto. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -s data  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Data di validità delle licenze. </p> <p>È possibile specificare la data nel formato <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-gg </span> o <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-gg-h24:min:sec </span>. Ad esempio, <span class="codeph"> 2008-12-1 </span> o <span class="codeph"> 2008-1-00:00:00 </span> per la mezzanotte del 1° dicembre 2008. </p> <p> 
     <ul id="ul_D52B337F547F4E7AB87FE025236CA930"> 
      <li id="li_DBAE380972434DB1A4EF20D399038AB8">Il valore deve essere minore del valore di <span class="codeph"> -e </span>, se presente. </li> 
      <li id="li_2899EC5559CF44319A4AC4ECD90A5B9A">Non è possibile applicare questa opzione insieme a <span class="codeph"> -r </span>. </li> 
      <li id="li_19861B1A64E44B95B649948EAB3E4085">Per rimuovere o eliminare la data di inizio quando si aggiorna un criterio DRM, utilizzare <span class="codeph"> -s </span> senza specificare una data. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -w [&lt;minutes&gt;[,enableHS|disableHS]  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Finestra di riproduzione, ovvero il numero di minuti che il contenuto può essere visualizzato dalla prima riproduzione. </p> <p>Se non specificato, o se si utilizza <span class="codeph"> -w </span> senza specificare un numero di minuti, non vi è alcuna limitazione della finestra di riproduzione. Il valore deve essere non negativo. </p> <p>Il flag opzionale <span class="codeph"> enableHS </span> o <span class="codeph"> disableHS </span> indica se abilitare o disabilitare l'arresto rigido. Il flag indica se il contesto di decrittografia viene distrutto alla fine della finestra di riproduzione (abilitato) o meno (disabilitato). </p> <p>Ad esempio, per specificare che il contenuto può essere visualizzato solo per 60 minuti e richiede un arresto rigido: 
     <codeblock>
       -w&amp;nbsp;60,enableHS 
     </codeblock> </p> <p>Nota:  <i>Il blocco rigido</i> non è attualmente supportato in Flash Player, Android e iOS. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l minuti  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La durata del caching delle licenze è il tempo in minuti in cui una licenza può essere memorizzata nella cache del License Store del cliente dopo che la licenza è stata rilasciata dal server. Il valore deve essere non negativo. </p> <p>È possibile specificare <span class="codeph"> -l 0 </span> per indicare che la memorizzazione in cache delle licenze non è consentita. Per il caching delle licenze illimitato, specifica <span class="codeph"> -l </span> senza alcun minuto. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -data di scadenza  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Data di fine memorizzazione nella cache della licenza. </p> <p class="- topic/p ">Indica la data finale in cui il cliente può memorizzare in cache le licenze nell’archivio licenze del cliente dopo che il server DRM di Primetime ha rilasciato la licenza. </p> <p>Puoi specificare la data nei seguenti formati: 
     <ul id="ul_112DE7248A9C48B19520A3AA9E5D1F03"> 
      <li id="li_01C5400E78B84A3B8955972FBA875AAC"> <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-gg  </span> </li> 
      <li id="li_AA13B1EFA07A4542A3DB41FA3320B143"> <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-gg-h24:min:sec  </span> </li> 
     </ul>Ad esempio, <span class="codeph"> 2008-12-1 </span> o <span class="codeph"> 2008-1-00:00:00 </span> per la mezzanotte del 1° dicembre 2008. È necessario applicare <span class="codeph"> -l </span> senza specificare alcun minuto per il caching delle licenze illimitato. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -authNS  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Spazio dei nomi di autenticazione. </p> <p class="- topic/p ">Se si applica questa opzione, il client deve immettere un nome utente e una password emessi dall'autorità specificata. </p> <p>Non è possibile applicare questa opzione insieme a <span class="codeph"> -x </span>. </p> <p>Questa opzione non è consentita per gli aggiornamenti. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -x  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Consenti accesso anonimo. </p> <p class="- topic/p ">Non è possibile applicare questa opzione insieme a <span class="codeph"> -authNS </span>. </p> <p class="- topic/p ">Questa opzione non è consentita per gli aggiornamenti. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -air pubId  </span>[:  <span class="+ topic/ph pr-d/codeph codeph"> appId  </span>[:[  <span class="+ topic/ph pr-d/codeph codeph"> min  </span>]:[  <span class="+ topic/ph pr-d/codeph codeph"> max  </span>]]] </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Un elenco consentiti di applicazioni AIR in grado di riprodurre contenuti protetti. </p> <p class="- topic/p ">È possibile applicare questa opzione per limitare quali editori, applicazioni e versioni possono accedere al contenuto protetto con questa policy DRM. </p> <p class="- topic/p ">Se non si specifica <i class="+ topic/ph hi-d/i ">appId</i>, sono consentite tutte le applicazioni per l'editore <i class="+ topic/ph hi-d/i ">pubId</i>. </p> <p>Nota:  I numeri di versione <i class="+ topic/ph hi-d/i ">min</i> e <i class="+ topic/ph hi-d/i ">max</i> sono facoltativi. </p> <p class="- topic/p ">È possibile specificare più opzioni <span class="codeph"> -air </span> per consentire più applicazioni. Se non si specifica un'applicazione AIR o SWF, tutte le applicazioni possono accedere a questo contenuto. Durante un aggiornamento, per rimuovere o eliminare tutte le voci dall’elenco, applica <span class="codeph"> -air </span> senza gli argomenti rimanenti . </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmBlacklist nome  </span> <i class="+ topic/ph hi-d/i ">/ </i> <span class="+ topic/ph pr-d/codeph codeph"> coppie  </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> di valori  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">I client DRM con restrizioni all’accesso ai contenuti protetti. </p> <p class="- topic/p ">Il valore supporta coppie nome:valore separate da virgola nel seguente formato: </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> os | release= stringValue  </span> </p> <p class="- topic/p ">Ad esempio, <span class="codeph"> os=Win,release=2.0.1 </span>. Durante un aggiornamento, per rimuovere tutte le voci dall'elenco, applicare <span class="codeph"> -drmBlacklist </span> senza gli argomenti rimanenti. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmLevel int  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica che i client DRM devono avere un livello di sicurezza minimo assegnato per accedere al contenuto protetto. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opAnalogico NO_PROTECTION | USE_IF_AVAILABLE | RICHIESTO | NO_PLAYBACK | REQUIRED_ACP | REQUIRED_CGMSA | USE_IF_AVAILABLE_ACP | USE_IF_AVAILABLE_CGMSA  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Vincoli di protezione dell'uscita analogica </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opDigital NO_PROTECTION | USE_IF_AVAILABLE | RICHIESTO | NO_PLAYBACK  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Vincoli di protezione dell'output digitale </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeBlacklist nome  </span> <i class="+ topic/ph hi-d/i ">/ </i> <span class="+ topic/ph pr-d/codeph codeph"> coppie  </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> di valori  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">I runtime dell’applicazione con restrizioni all’accesso ai contenuti protetti. </p> <p class="- topic/p ">Il valore supporta coppie nome:valore separate da virgola nel seguente formato: </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> os | domanda | release= stringValue  </span> </p> <p class="- topic/p ">Ad esempio, <span class="codeph"> os=Win,release=2.0.1,application=AIR </span>. Durante un aggiornamento, per rimuovere tutte le voci dall'elenco, applica <span class="codeph"> -runtimeBlacklist </span> senza gli argomenti rimanenti . </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeLevel int  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica che i runtime dell'applicazione devono avere un livello di protezione minimo specificato per accedere al contenuto protetto. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -url swf  </span> </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf file= swf_file  </span>,  <span class="+ topic/ph pr-d/codeph codeph"> time= max_time_to_verify  </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Un elenco consentiti di applicazioni SWF autorizzate a riprodurre contenuto protetto. </p> <p class="- topic/p ">È possibile specificare più opzioni <span class="codeph"> -swf </span> per consentire più applicazioni. Se non si specificano applicazioni AIR o SWF, tutte le applicazioni possono accedere a questo contenuto. </p> <p>Durante un aggiornamento, per rimuovere tutte le voci dall’elenco, applica <span class="codeph"> -swf </span> senza gli argomenti rimanenti . Se si desidera identificare un SWF in base al suo valore hash, è necessario specificare il file SWF per il quale calcolare l’hash e il tempo massimo per consentire il completamento della verifica SWF (in secondi). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -k name= value  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica la chiave/i valori personalizzati che si desidera aggiungere a un criterio DRM. </p> <p class="- topic/p ">Puoi specificare più opzioni <span class="codeph"> -k </span>. Durante l'aggiornamento, è possibile applicare <span class="codeph"> -k </span> senza gli argomenti rimanenti se si desidera rimuovere tutte le proprietà. L'interpretazione o la gestione dei dati è gestita dal server di licenza DRM di Primetime. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -p name= value  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Aggiunge una proprietà personalizzata che viene visualizzata nella licenza generata per ogni client. </p> <p class="- topic/p ">È possibile specificare più opzioni <span class="codeph"> -p </span> per aggiungere più proprietà. Durante un aggiornamento, è necessario applicare <span class="codeph"> -p </span> senza gli argomenti rimanenti se si desidera rimuovere tutte le proprietà. L'interpretazione o la gestione di tali dati è gestita dall'implementazione dell'applicazione client. </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> <span class="codeph"> -opOTA whitelist=&lt;connection types=""&gt; </span> </span> </td> 
   <td colname="2" class="- topic/entry "> Limiti di protezione dell'uscita dell'aria (OTA). Il campo <span class="codeph"> whitelist </span> specifica i tipi di connessione da elenco consentiti e il formato di &lt;tipi di connessione&gt; è <span class="codeph"> [type(,type)*] </span>, dove type può essere uno dei seguenti: MIRACAST, AEROPORTO, WIDI, DLNA </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opResolution  &lt;filename&gt; </span> </td> 
   <td colname="2" class="- topic/entry "> <p>Vincoli di protezione dell'output basati sulla risoluzione definiti nel file specificato. </p> <p>La codifica di questo file è JSON. La grammatica per la formattazione si trova in <i>Informazioni sulla protezione dell'output basata sulla risoluzione</i>. </p> </td> 
  </tr> 
 </tbody> 
</table>

**Esempi**

Per creare un criterio che consenta l’accesso anonimo al contenuto, utilizzare il file delle proprietà di configurazione:

```
java -jar libs\AdobePolicyManager.jar new policy_test.pol -x -c my_configuration.properties
```
