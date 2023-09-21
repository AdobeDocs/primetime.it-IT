---
title: Utilizzo della riga di comando
description: Utilizzo della riga di comando
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 0%

---

# Utilizzo della riga di comando {#command-line-usage}

Prima di utilizzare Policy Manager, assicurati di soddisfare i requisiti elencati in Requisiti.

Policy Manager è in [!DNL \Reference Implementation\Command Line Tools] sul DVD. Per eseguire lo strumento, utilizzare la sintassi seguente:

```
java -jar AdobePolicyManager.jar  
<i class="+ topic ph hi-d="" i "="">
  command filename [options] 
</i class="+ topic>
```

La tabella seguente contiene le descrizioni delle azioni della riga di comando mostrate nella sintassi precedente:

| Azione della riga di comando | Descrizione |
|---|---|
| `new` | Crea un nuovo criterio. |
| `detail` | Descrive un criterio esistente. |
| `update` | Aggiorna un criterio esistente. |

Nella tabella seguente vengono descritte le opzioni della riga di comando che è possibile specificare insieme alla sintassi precedente:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_q5h_cpy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Opzione della riga di comando </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descrizione </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c file di configurazione </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica la posizione del file di configurazione. Se questa opzione non viene utilizzata, Policy Manager cercherà <span class="filepath"> flashaccesstools.properties </span> nella directory di lavoro. Le opzioni specificate nella riga di comando hanno la precedenza su quelle presenti nel file di configurazione. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se il file di destinazione esiste già, sovrascriverlo senza chiedere conferma. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Non chiedere se il file di destinazione deve essere sovrascritto. Se il file di destinazione esiste già e <span class="codeph"> -o </span> non è impostato, verrà restituito un errore. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -root </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica che il criterio dispone di una licenza root. Aggiornamenti non consentiti. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e data </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Data prima della quale le licenze saranno valide. Specifica come <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-gg </span> o <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-gg-h24:min:sec </span>. Ad esempio, 2008-12-1 o 2008-12-1-00:00:00 per mezzanotte del 1 dicembre 2008. Il valore deve essere maggiore del valore di <span class="codeph"> -s </span>, se presente. Questa opzione non può essere utilizzata con <span class="codeph"> -r </span>. Per rimuovere la data di fine durante l’aggiornamento di un criterio, utilizza <span class="codeph"> -e </span> senza specificare una data. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r minuti </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La durata (minuti) di validità del contenuto protetto con questo criterio, a partire dal momento in cui il contenuto è protetto con il packager. Il valore non deve essere negativo. Questa opzione non può essere utilizzata con <span class="codeph"> -e </span>. Per rimuovere la durata durante l’aggiornamento di un criterio, utilizza <span class="codeph"> -r </span> senza specificare un numero di minuti. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -s data </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Data dopo la quale le licenze saranno valide. Specifica come <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-gg </span> o <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-gg-h24:min:sec </span>. Ad esempio, 2008-12-1 o 2008-12-1-00:00:00 per mezzanotte del 1 dicembre 2008. Il valore deve essere minore del valore di <span class="codeph"> -e </span>, se presente. Questa opzione non può essere utilizzata con <span class="codeph"> -r </span>. Per rimuovere la data di inizio durante l’aggiornamento di un criterio, utilizza <span class="codeph"> -s </span> senza specificare una data. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -w minuti </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Finestra di riproduzione (il numero di minuti in cui il contenuto può essere visualizzato, a partire dalla prima riproduzione). Se questa opzione non è specificata o se <span class="codeph"> -w </span> viene utilizzato senza specificare il numero di minuti, non vi sono limiti alla finestra di riproduzione. Il valore non deve essere negativo. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l minuti </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La durata della memorizzazione nella cache della licenza, in minuti, è l'intervallo di tempo in cui una licenza potrà essere memorizzata nella cache dell'archivio licenze del client dopo che la licenza è stata rilasciata dal server. Il valore non deve essere negativo. Specifica <span class="codeph"> -l 0 </span> per indicare che il caching delle licenze non è consentito. Utilizzare <span class="codeph"> -l </span> senza specificare un numero di minuti per il caching illimitato delle licenze. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -data di fine </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La data di fine del caching delle licenze (la data dopo la quale le licenze non possono essere memorizzate nella cache nell’archivio licenze del client, dopo che la licenza è stata rilasciata dal server). Specifica come <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-gg </span><i class="+ topic/ph hi-d/i "> </i>o<i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-gg-h24:min:sec </span>. Ad esempio, 2008-12-1 o 2008-12-1-00:00:00 per mezzanotte del 1 dicembre 2008. Utilizzare <span class="codeph"> -l </span> senza specificare un numero di minuti per il caching illimitato delle licenze. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -authNS </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Spazio dei nomi di autenticazione. Se specificato, il client deve eseguire l'autenticazione con un nome utente e una password emessi dall'autorità specificata. Questa opzione non può essere utilizzata con <span class="codeph"> -x </span>. Non è consentito per gli aggiornamenti. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -x </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Consenti accesso anonimo. Questa opzione non può essere utilizzata con <span class="codeph"> -authNS </span>. Non è consentito per gli aggiornamenti. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -air pubId </span>[: <span class="+ topic/ph pr-d/codeph codeph"> appId </span>[:[ <span class="+ topic/ph pr-d/codeph codeph"> min </span>]:[ <span class="+ topic/ph pr-d/codeph codeph"> max </span>]] </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Un elenco consentiti di applicazioni AIR che consentono di riprodurre contenuti protetti. Utilizzare questa opzione per limitare quali editori, applicazioni e versioni possono accedere a contenuti protetti con questo criterio. </p> <p class="- topic/p ">Se <i class="+ topic/ph hi-d/i ">appId</i> non è specificato, tutte le applicazioni per publisher <i class="+ topic/ph hi-d/i ">pubId</i> sono consentiti. </p> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">min</i> e <i class="+ topic/ph hi-d/i ">max</i> I numeri di versione sono facoltativi. </p> <p class="- topic/p ">Più <span class="codeph"> -aria </span> è possibile specificare opzioni per consentire più applicazioni. Se non è specificata alcuna applicazione AIR o SWF, tutte le applicazioni possono accedere a questo contenuto. Durante un aggiornamento, utilizzare -air senza gli argomenti rimanenti per rimuovere tutte le voci dall'elenco. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmNome blacklist </span> <i class="+ topic/ph hi-d/i ">/</i> <span class="+ topic/ph pr-d/codeph codeph"> valore </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> coppie </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Ai client DRM è stato impedito l'accesso al contenuto protetto. Il valore è costituito da coppie nome:valore separate da virgola con il seguente formato: </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> sistema operativo | release= stringValue </span> </p> <p class="- topic/p ">Ad esempio: <span class="codeph"> os=Win,release=2.0.1 </span>. Durante un aggiornamento, utilizza <span class="codeph"> -drmBlacklist </span> senza gli argomenti rimanenti per rimuovere tutte le voci dall'elenco. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmLevel int </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica che i client DRM devono disporre del livello di protezione minimo specificato per accedere al contenuto protetto. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opAnalog NO_PROTECTION | USE_IF_AVAILABLE | OBBLIGATORIO | NO_PLAYBACK | ACP_REQUIRED | CGMS-A_REQUIRED | USE_ACP_IF_AVAILABLE | USE_CGMS-A_IF_AVAILABLE </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Vincoli di protezione dell'uscita analogica. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opDigital NO_PROTECTION | USE_IF_AVAILABLE | OBBLIGATORIO | NO_PLAYBACK </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Vincoli di protezione dell'output digitale. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> Nome -runtimeBlacklist </span> <i class="+ topic/ph hi-d/i ">/</i> <span class="+ topic/ph pr-d/codeph codeph"> valore </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> coppie </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Ai runtime dell’applicazione non è consentito accedere al contenuto protetto. Il valore è costituito da coppie nome:valore separate da virgola con il seguente formato: </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> sistema operativo | domanda | release= stringValue </span> </p> <p class="- topic/p ">Ad esempio: <span class="codeph"> os=Win,release=2.0.1,application=AIR </span>. Durante un aggiornamento, utilizza <span class="codeph"> -runtimeBlacklist </span> senza gli argomenti rimanenti per rimuovere tutte le voci dall'elenco. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeLevel int </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica che i runtime dell'applicazione devono disporre del livello di protezione minimo specificato per accedere al contenuto protetto. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> URL -swf </span> </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf file= file_swf </span>, <span class="+ topic/ph pr-d/codeph codeph"> time= max_time_to_verify </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Un elenco consentiti di applicazioni SWF autorizzate a riprodurre contenuti protetti. È possibile specificare più opzioni -swf per consentire l'utilizzo di più applicazioni. Se non è specificata alcuna applicazione AIR o SWF, tutte le applicazioni possono accedere a questo contenuto. Durante un aggiornamento, utilizzare -swf senza gli argomenti rimanenti per rimuovere tutte le voci dall'elenco. Per identificare un SWF in base al suo valore hash, specifica il file SWF per il quale calcolare l’hash e il tempo massimo (in secondi) per consentire il completamento della verifica SWF. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -k name= valore </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica la chiave o i valori personalizzati da aggiungere al criterio. Più <span class="codeph"> -k </span> è possibile specificare le opzioni. Durante l’aggiornamento, utilizza <span class="codeph"> -k </span> senza gli argomenti rimanenti per rimuovere tutte le proprietà. L'interpretazione o la gestione di questi dati dipende interamente dall'implementazione del server licenze di accesso Adobe. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -p name= valore </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Aggiunge una proprietà personalizzata, che verrà visualizzata nella licenza generata per ciascun client. Più <span class="codeph"> -p </span> è possibile specificare opzioni per aggiungere più proprietà. Durante un aggiornamento, utilizza <span class="codeph"> -p </span> senza gli argomenti rimanenti per rimuovere tutte le proprietà. L’interpretazione o la gestione di tali dati dipende interamente dall’implementazione dell’applicazione client. </p> </td> 
  </tr> 
 </tbody> 
</table>
