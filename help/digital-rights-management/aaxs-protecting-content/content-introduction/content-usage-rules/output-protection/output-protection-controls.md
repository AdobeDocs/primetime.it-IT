---
title: Controlli di protezione dell'output
description: Controlli di protezione dell'output
copied-description: true
exl-id: e27e49f9-9bc3-493f-a9ba-efe623694942
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---

# Controlli di protezione dell&#39;output {#output-protection-controls}

**Controlla se l&#39;output su dispositivi di rendering esterni è protetto. Specificare le uscite analogiche e digitali in modo indipendente.**

Controlla se l&#39;output su dispositivi di rendering esterni deve essere limitato. Per periferica esterna si intende qualsiasi periferica video o audio non incorporata nel computer. L&#39;elenco delle periferiche esterne esclude i display integrati, ad esempio nei notebook. Le restrizioni dell&#39;uscita analogica e digitale possono essere specificate in modo indipendente.

Sono disponibili le seguenti opzioni/livelli di applicazione:

<table frame="all" colsep="0" rowsep="1" id="adobetable_fvw_5fx_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Opzione </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Supportato in dispositivi analogici </p> </th> 
   <th colname="3" class="- topic/entry entry"> <p class="- topic/p ">Supportato in dispositivi digitali </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Obbligatorio</b> — È necessario abilitare la protezione dell'output Analog Copy Protection (ACP) o Copy Generation Management System - Analog (CGMS-A) per riprodurre i contenuti su una periferica esterna. I client di accesso Adobe devono abilitare la protezione dell'output utilizzando ACP o CGMS-A. Sui dispositivi che supportano entrambi, i client Adobe Access 3.0 tenteranno di abilitare entrambi. Tuttavia, per riprodurre il contenuto è necessario abilitarne solo uno. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SÌ </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">SÌ </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">ACP richiesto</b> — È necessaria la protezione dell'output ACP. La riproduzione non è consentita su CGMS-A. I client di Adobe Access 2.0 non supportano questa opzione. Se questa opzione è impostata, un client Adobe Access 2.0 si comporta come se fosse stata specificata l'opzione "No Playback" (Nessuna riproduzione). </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SÌ </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">CGMS-A richiesto</b> — È necessaria la protezione dell'output CGMS-A. Riproduzione non consentita su ACP. I client di Adobe Access 2.0 non supportano questa opzione. Se questa opzione è impostata, un client Adobe Access 2.0 si comporta come se fosse stata specificata l'opzione "No Playback" (Nessuna riproduzione). </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SÌ </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Usa se disponibile</b> — Se disponibile, tentare di abilitare la protezione dell'output ACP e CGMS-A e di consentire la riproduzione, se non disponibile. I client Adobe Access 3.0 tenteranno di abilitare sia ACP che CGMS-A, se possibile. I client di Accesso Adobe 2.0 tenteranno di abilitare solo ACP o CGMS-A. Ad esempio, il client Adobe Access tenterà di abilitare ACP o CGMS-A. Se il tentativo ha esito positivo, l’altra opzione non sarà abilitata. Se il tentativo non riesce, viene eseguito un secondo tentativo per abilitare l’altra opzione. Anche se entrambi i tentativi non vanno a buon fine, il contenuto verrà riprodotto comunque. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SÌ </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">SÌ </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Usa ACP se disponibile</b> — Se disponibile, tentare di abilitare la protezione dell'output ACP, ma consentire la riproduzione se non disponibile. La protezione non è disponibile su CGMS-A. I client di Adobe Access 2.0 non supportano questa opzione. Se questa opzione è impostata, un client Adobe Access 2.0 si comporta come se fosse stata specificata l'opzione "Nessuna protezione". </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SÌ </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Usa CGMS-A se disponibile </b>— Se disponibile, tentare di attivare la protezione dell'output CGMS-A, ma consentire la riproduzione se non disponibile. La protezione non è disponibile su ACP. I client di Adobe Access 2.0 non supportano questa opzione. Se questa opzione è impostata, un client Adobe Access 2.0 si comporta come se fosse stata specificata l'opzione "Nessuna protezione". </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SÌ </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Nessuna protezione</b> — Le uscite analogiche e digitali non supportano la protezione dell'uscita. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SÌ </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">SÌ </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Nessuna riproduzione</b> - Non consentire la riproduzione su un dispositivo esterno per le uscite analogiche e digitali. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SÌ </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">SÌ </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>Anche se queste regole vengono applicate in modo coerente su tutte le piattaforme, attualmente è possibile attivare in modo sicuro la protezione dell’output solo sulle piattaforme Windows. Su altre piattaforme (come Macintosh e Linux) non sono disponibili funzioni di sistema operativo di supporto per applicazioni di terze parti.

Caso d’uso di esempio: alcuni contenuti potrebbero applicare controlli di protezione dell’output e il livello di protezione può essere impostato dal distributore di contenuti. Se si specifica &quot;Required&quot; e si tenta la riproduzione su un Macintosh, il client non riproduce il contenuto su dispositivi esterni. Tuttavia, il contenuto verrà riprodotto su monitor interni.

Se si specifica &quot;Required&quot; e si tenta la riproduzione su Linux, il client non riproduce il contenuto su alcun dispositivo perché non è possibile distinguere tra dispositivi interni ed esterni.

Se si specifica &quot;Usa se disponibile&quot;, la protezione dell&#39;output viene attivata ove possibile. Ad esempio, sui computer Windows che supportano il protocollo COPP (Certified Output Protection Protocol), il contenuto viene trasmesso con protezione dell&#39;output a uno schermo esterno. Questo esempio è talvolta noto come &quot;controllo di output selezionabile&quot;.
