---
title: Uso della riga di comando
description: Uso della riga di comando
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '1026'
ht-degree: 0%

---


# Uso della riga di comando {#command-line-usage}

Prima di utilizzare Policy Manager, assicurati di soddisfare i requisiti elencati in Requisiti.

Policy Manager si trova nella directory [!DNL \Reference Implementation\Command Line Tools] del DVD. Per eseguire lo strumento, utilizzare la sintassi seguente:

```
java -jar AdobePolicyManager.jar  
<i class="+ topic ph hi-d="" i "="">
  command filename [options] 
</i class="+ topic>
```

La tabella seguente contiene le descrizioni delle azioni della riga di comando visualizzate nella sintassi precedente:

| Azione riga di comando | Descrizione |
|---|---|
| `new` | Crea un nuovo criterio. |
| `detail` | Descrive un criterio esistente. |
| `update` | Aggiorna un criterio esistente. |

La tabella seguente descrive le opzioni della riga di comando che è possibile specificare insieme alla sintassi precedente:

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica il percorso del file di configurazione. Se questa opzione non viene utilizzata, Policy Manager cercherà <span class="filepath"> flashaccesstools.properties </span> nella directory di lavoro. Le opzioni specificate nella riga di comando hanno la precedenza su quelle presenti nel file di configurazione. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se il file di destinazione esiste già, sovrascriverlo senza richiedere conferma. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Non chiedere se il file di destinazione deve essere sovrascritto. Se il file di destinazione esiste già e <span class="codeph"> -o </span> non è impostato, viene restituito un errore. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -root  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica che il criterio dispone di una licenza radice. Non sono consentiti aggiornamenti. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e data  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Data di validità dei titoli. Specificare come <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-gg </span> o <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-gg-h24:min:sec </span>. Ad esempio, 2008-12-1 o 2008-12-1-00:00:00 per la mezzanotte del 1° dicembre 2008. Il valore deve essere maggiore del valore di <span class="codeph"> -s </span>, se presente. Questa opzione non può essere utilizzata con <span class="codeph"> -r </span>. Per rimuovere la data di fine durante l’aggiornamento di un criterio, utilizza <span class="codeph"> -e </span> senza specificare una data. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r minuti  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La durata (minuti) valida del contenuto protetto con questo criterio, a partire dal momento in cui il contenuto è protetto con il packager. Il valore deve essere non negativo. Questa opzione non può essere utilizzata con <span class="codeph"> -e </span>. Per rimuovere la durata durante l'aggiornamento di un criterio, utilizza <span class="codeph"> -r </span> senza specificare un numero di minuti. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -s data  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Data di validità dei titoli. Specificare come <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-gg </span> o <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-gg-h24:min:sec </span>. Ad esempio, 2008-12-1 o 2008-12-1-00:00:00 per la mezzanotte del 1° dicembre 2008. Il valore deve essere minore del valore di <span class="codeph"> -e </span>, se presente. Questa opzione non può essere utilizzata con <span class="codeph"> -r </span>. Per rimuovere la data di inizio durante l'aggiornamento di un criterio, utilizza <span class="codeph"> -s </span> senza specificare una data. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -w minuti  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La finestra di riproduzione (il numero di minuti in cui è possibile visualizzare il contenuto, a partire dalla prima riproduzione). Se questa opzione non è specificata o se si utilizza <span class="codeph"> -w </span> senza specificare il numero di minuti, non vi è alcuna limitazione alla finestra di riproduzione. Il valore deve essere non negativo. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l minuti  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La durata del caching delle licenze in minuti, ossia l’ora in cui una licenza può essere memorizzata nella cache del relativo License Store dopo che la licenza è stata rilasciata dal server. Il valore deve essere non negativo. Specificare <span class="codeph"> -l 0 </span> per indicare che la memorizzazione in cache delle licenze non è consentita. Utilizza <span class="codeph"> -l </span> senza specificare un numero di minuti per la memorizzazione in cache illimitata delle licenze. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -data di scadenza  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La data di fine del caching delle licenze (la data successiva alla quale le licenze potrebbero non essere memorizzate nella cache del License Store del cliente, dopo il rilascio della licenza da parte del server). Specificare come <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-gg </span><i class="+ topic/ph hi-d/i "> </i>o<i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-gg-h24:min:sec </span>. Ad esempio, 2008-12-1 o 2008-12-1-00:00:00 per la mezzanotte del 1° dicembre 2008. Utilizza <span class="codeph"> -l </span> senza specificare un numero di minuti per la memorizzazione in cache illimitata delle licenze. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -authNS  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Spazio dei nomi di autenticazione. Se specificato, il client deve eseguire l'autenticazione con un nome utente e una password emessi dall'autorità specificata. Questa opzione non può essere utilizzata con <span class="codeph"> -x </span>. Non sono consentiti aggiornamenti. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -x  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Consenti accesso anonimo. Questa opzione non può essere utilizzata con <span class="codeph"> -authNS </span>. Non sono consentiti aggiornamenti. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -air pubId  </span>[:  <span class="+ topic/ph pr-d/codeph codeph"> appId  </span>[:[  <span class="+ topic/ph pr-d/codeph codeph"> min  </span>]:[  <span class="+ topic/ph pr-d/codeph codeph"> max  </span>]]] </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Un elenco consentiti di applicazioni AIR autorizzate a riprodurre contenuti protetti. Utilizza questa opzione per limitare quali editori, applicazioni e versioni possono accedere ai contenuti protetti da questo criterio. </p> <p class="- topic/p ">Se <i class="+ topic/ph hi-d/i ">appId</i> non è specificato, sono consentite tutte le applicazioni per l'editore <i class="+ topic/ph hi-d/i ">pubId</i>. </p> <p class="- topic/p "><i class="+ topic/ph hi-d/i "></i> i numeri  <i class="+ topic/ph hi-d/i "></i> minuscoli e massimi sono facoltativi. </p> <p class="- topic/p ">È possibile specificare più opzioni <span class="codeph"> -air </span> per consentire più applicazioni. Se non sono specificate applicazioni AIR o SWF, tutte le applicazioni possono accedere a questo contenuto. Durante un aggiornamento, utilizzare -air senza gli argomenti rimanenti per rimuovere tutte le voci dall'elenco. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmBlacklist nome  </span> <i class="+ topic/ph hi-d/i ">/ </i> <span class="+ topic/ph pr-d/codeph codeph"> coppie  </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> di valori  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">I client DRM non potevano accedere ai contenuti protetti. Il valore è costituito da coppie nome:valore separate da virgola con il seguente formato: </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> os | release= stringValue  </span> </p> <p class="- topic/p ">Ad esempio, <span class="codeph"> os=Win,release=2.0.1 </span>. Durante un aggiornamento, utilizzare <span class="codeph"> -drmBlacklist </span> senza gli argomenti rimanenti per rimuovere tutte le voci dall'elenco. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -drmLevel int  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica che i client DRM devono avere il livello di sicurezza minimo specificato per accedere al contenuto protetto. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opAnalogico NO_PROTECTION | USE_IF_AVAILABLE | RICHIESTO | NO_PLAYBACK | ACP_REQUIRED | CGMS-A_REQUIRED | USE_ACP_IF_AVAILABLE | USE_CGMS-A_IF_AVAILABLE  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Vincoli di protezione dell'uscita analogica. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -opDigital NO_PROTECTION | USE_IF_AVAILABLE | RICHIESTO | NO_PLAYBACK  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Vincoli di protezione dell'output digitale. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeBlacklist nome  </span> <i class="+ topic/ph hi-d/i ">/ </i> <span class="+ topic/ph pr-d/codeph codeph"> coppie  </span> <i class="+ topic/ph hi-d/i "> </i> <span class="+ topic/ph pr-d/codeph codeph"> di valori  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">I tempi di esecuzione dell'applicazione non consentivano l'accesso al contenuto protetto. Il valore è costituito da coppie nome:valore separate da virgola con il seguente formato: </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> os | domanda | release= stringValue  </span> </p> <p class="- topic/p ">Ad esempio, <span class="codeph"> os=Win,release=2.0.1,application=AIR </span>. Durante un aggiornamento, utilizzare <span class="codeph"> -runtimeBlacklist </span> senza gli argomenti rimanenti per rimuovere tutte le voci dall’elenco. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -runtimeLevel int  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Indica che i runtime dell'applicazione devono avere il livello di protezione minimo specificato per accedere al contenuto protetto. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -url swf  </span> </p> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -swf file= swf_file  </span>,  <span class="+ topic/ph pr-d/codeph codeph"> time= max_time_to_verify  </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Un elenco consentiti di applicazioni SWF autorizzate a riprodurre contenuto protetto. È possibile specificare più opzioni -swf per consentire più applicazioni. Se non sono specificate applicazioni AIR o SWF, tutte le applicazioni possono accedere a questo contenuto. Durante un aggiornamento, utilizzare -swf senza gli argomenti rimanenti per rimuovere tutte le voci dall'elenco. Per identificare un SWF in base al suo valore hash, specificare il file SWF per il quale calcolare l’hash e il tempo massimo necessario per consentire il completamento della verifica SWF (in secondi). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -k name= value  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica la chiave o i valori personalizzati da aggiungere al criterio. È possibile specificare più opzioni <span class="codeph"> -k </span>. Durante l'aggiornamento, utilizzare <span class="codeph"> -k </span> senza gli argomenti rimanenti per rimuovere tutte le proprietà. L'interpretazione o la gestione di questi dati dipende completamente dall'implementazione del server licenze di Adobe Access. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -p name= value  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Aggiunge una proprietà personalizzata che verrà visualizzata nella licenza generata per ciascun client. È possibile specificare più opzioni <span class="codeph"> -p </span> per aggiungere più proprietà. Durante un aggiornamento, utilizzare <span class="codeph"> -p </span> senza gli argomenti rimanenti per rimuovere tutte le proprietà. L'interpretazione o la gestione di tali dati dipende interamente dall'attuazione dell'applicazione del cliente. </p> </td> 
  </tr> 
 </tbody> 
</table>

