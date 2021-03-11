---
title: Controlli di protezione dell'uscita
description: Controlli di protezione dell'uscita
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---


# Controlli di protezione dell&#39;uscita {#output-protection-controls}

**Controlla se l&#39;output su dispositivi di rendering esterni è protetto. Specificare in modo indipendente le uscite analogiche e digitali.**

Controlla se l&#39;output su dispositivi di rendering esterni deve essere limitato. Per dispositivo esterno si intende qualsiasi dispositivo video o audio non incorporato nel computer. L&#39;elenco dei dispositivi esterni esclude i display integrati, ad esempio nei computer portatili. Le limitazioni dell&#39;uscita analogica e digitale possono essere specificate in modo indipendente.

Sono disponibili le seguenti opzioni/livelli di applicazione:

<table frame="all" colsep="0" rowsep="1" id="adobetable_fvw_5fx_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Opzione </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Supportato in dispositivi analogici </p> </th> 
   <th colname="3" class="- topic/entry entry"> <p class="- topic/p ">Supportato nei dispositivi digitali </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Obbligatorio</b> : per riprodurre i contenuti su un dispositivo esterno, è necessario abilitare la protezione dall'uscita analogica (CGMS-A) o il sistema di gestione della generazione di copie analogiche (ACP). I client Adobe Access devono abilitare la protezione dell’output utilizzando ACP o CGMS-A. Sui dispositivi che supportano entrambi, i client Adobe Access 3.0 tenteranno di abilitare entrambi. Tuttavia, per riprodurre il contenuto è necessario abilitare solo uno. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SÌ </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">SÌ </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">ACP Obbligatorio</b> : è necessaria la protezione della produzione ACP. Riproduzione non consentita su CGMS-A. I client di Adobe Access 2.0 non supportano questa opzione. Se impostato, un client Adobe Access 2.0 si comporta come se fosse stata specificata l'opzione "No Playback". </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SÌ </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">CGMS-A Obbligatorio</b> : è richiesta la protezione dell'uscita CGMS-A. Riproduzione non consentita su ACP. I client di Adobe Access 2.0 non supportano questa opzione. Se impostato, un client Adobe Access 2.0 si comporta come se fosse stata specificata l'opzione "No Playback". </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SÌ </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Usa se disponibile</b>  - Prova ad abilitare la protezione dell'output ACP e CGMS-A se disponibile e consenti la riproduzione se non disponibile. I client Adobe Access 3.0 tenteranno di abilitare sia ACP che CGMS-A, se possibile. I client Adobe Access 2.0 tentano solo di abilitare ACP o CGMS-A. Ad esempio, il client Adobe Access tenterà di abilitare ACP o CGMS-A. Se il tentativo ha esito positivo, l’altra opzione non sarà abilitata. Se il tentativo non riesce, verrà effettuato un secondo tentativo per abilitare l’altra opzione. Anche se entrambi i tentativi falliscono, il contenuto verrà comunque riprodotto. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SÌ </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">SÌ </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Utilizza ACP se disponibile</b>  - Prova ad abilitare la protezione dell'output ACP se disponibile, ma consenti la riproduzione se non disponibile. La protezione non è disponibile su CGMS-A. I client di Adobe Access 2.0 non supportano questa opzione. Se impostato, un client Adobe Access 2.0 si comporta come se fosse stata specificata l'opzione "Nessuna protezione". </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SÌ </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Usa CGMS-A se disponibile  </b>— Prova ad abilitare la protezione dell'output CGMS-A se disponibile, ma consenti la riproduzione se non disponibile. La protezione non è disponibile su ACP. I client di Adobe Access 2.0 non supportano questa opzione. Se impostato, un client Adobe Access 2.0 si comporta come se fosse stata specificata l'opzione "Nessuna protezione". </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SÌ </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Nessuna protezione</b> : nessuna abilitazione alla protezione dell'output viene applicata alle uscite analogiche e digitali. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SÌ </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">SÌ </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Nessuna riproduzione</b>  - Non consentire la riproduzione su dispositivi esterni per le uscite analogiche e digitali. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SÌ </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">SÌ </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>Sebbene queste regole siano applicate in modo coerente in tutte le piattaforme, al momento è solo possibile attivare in modo sicuro la protezione dell&#39;output sulle piattaforme Windows. Su altre piattaforme (come Macintosh e Linux) non sono disponibili funzioni di supporto del sistema operativo per applicazioni di terze parti.

Esempio di utilizzo: Alcuni contenuti possono applicare controlli di protezione dell&#39;output e il livello di protezione può essere impostato dal distributore dei contenuti. Se si specifica &quot;Obbligatorio&quot; e si tenta la riproduzione su un Macintosh, il client non riproduce il contenuto su dispositivi esterni. I contenuti verranno comunque riprodotti sui monitor interni.

Se si specifica &quot;Obbligatorio&quot; e si tenta la riproduzione su Linux, il client non riproduce il contenuto su alcun dispositivo perché non è possibile distinguere tra dispositivi interni ed esterni.

Se si specifica &quot;Usa se disponibile&quot;, la protezione dell&#39;output viene attivata laddove possibile. Ad esempio, nei computer Windows che supportano il protocollo di protezione dell&#39;output certificato (COPP), il contenuto viene trasmesso con protezione dell&#39;output a uno schermo esterno. Questo esempio è talvolta noto come &quot;controllo dell&#39;output selezionabile&quot;.
