---
seo-title: Controlli di protezione dell'uscita
title: Controlli di protezione dell'uscita
uuid: 1f4cc617-7f14-4952-8e61-6acbdf01d10e
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c

---


# Controlli di protezione dell&#39;uscita {#output-protection-controls}

**Controllare se l&#39;output su dispositivi di rendering esterni è protetto. Specificare le uscite analogiche e digitali in modo indipendente.**

Controlla se l&#39;output su dispositivi di rendering esterni deve essere limitato. Per dispositivo esterno si intende qualsiasi dispositivo video o audio non incorporato nel computer. Nell&#39;elenco dei dispositivi esterni sono esclusi gli schermi integrati, ad esempio nei computer portatili. Le restrizioni relative all&#39;uscita analogica e digitale possono essere specificate in modo indipendente.

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
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Obbligatorio</b> — La protezione dell'uscita analogica per la copia (ACP) o il sistema di gestione della generazione di copie (CGMS-A) deve essere attivata per poter riprodurre il contenuto su un dispositivo esterno. I client Adobe Access devono abilitare la protezione dell'output tramite ACP o CGMS-A. Sui dispositivi che supportano entrambi, i client Adobe Access 3.0 tenteranno di abilitare entrambi. Tuttavia, per riprodurre il contenuto è necessario abilitare solo uno. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SÌ </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">SÌ </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">ACP richiesto</b> — È richiesta la protezione dell'output ACP. La riproduzione non è consentita su CGMS-A. I client Adobe Access 2.0 non supportano questa opzione. Se impostato, un client Adobe Access 2.0 si comporta come se fosse stata specificata l'opzione "Nessuna riproduzione". </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SÌ </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">CGMS-A richiesto</b> — È necessaria la protezione dell'uscita CGMS-A. La riproduzione non è consentita su ACP. I client Adobe Access 2.0 non supportano questa opzione. Se impostato, un client Adobe Access 2.0 si comporta come se fosse stata specificata l'opzione "Nessuna riproduzione". </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SÌ </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Usa se disponibile</b> : Cercate di abilitare la protezione dell'output ACP e CGMS-A se disponibile e di consentire la riproduzione se non disponibile. I client Adobe Access 3.0 tenteranno di abilitare sia ACP che CGMS-A, se possibile. I client Adobe Access 2.0 tentano di abilitare solo ACP o CGMS-A. Ad esempio, il client Adobe Access tenterà di abilitare ACP o CGMS-A. Se il tentativo ha esito positivo, l'altra opzione non sarà abilitata. Se il tentativo non riesce, verrà effettuato un secondo tentativo per abilitare l'altra opzione. Anche se entrambi i tentativi non riescono, il contenuto verrà comunque riprodotto. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SÌ </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">SÌ </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Usa ACP se disponibile</b> — Se disponibile, provate a abilitare la protezione dell'output ACP, ma consentite la riproduzione se non disponibile. La protezione non è disponibile su CGMS-A. I client Adobe Access 2.0 non supportano questa opzione. Se impostato, un client Adobe Access 2.0 si comporta come se fosse stata specificata l'opzione "Nessuna protezione". </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SÌ </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Usa CGMS-A se disponibile </b>— Tentate di abilitare la protezione dell'output CGMS-A se disponibile, ma consentite la riproduzione se non disponibile. La protezione non è disponibile sugli ACP. I client Adobe Access 2.0 non supportano questa opzione. Se impostato, un client Adobe Access 2.0 si comporta come se fosse stata specificata l'opzione "Nessuna protezione". </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SÌ </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Nessuna protezione</b> — Per le uscite analogiche e digitali non viene applicata alcuna abilitazione alla protezione dell'uscita. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SÌ </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">SÌ </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Nessuna riproduzione</b> - Non consentire la riproduzione su dispositivi esterni per le uscite analogiche e digitali. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SÌ </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">SÌ </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Sebbene queste regole siano applicate in modo coerente su tutte le piattaforme, al momento è possibile attivare la protezione dell&#39;output solo in modo sicuro sulle piattaforme Windows. Su altre piattaforme (come Macintosh e Linux) non sono disponibili funzioni del sistema operativo supportate per le applicazioni di terze parti.

Esempio di utilizzo: Alcuni contenuti possono applicare controlli di protezione dell&#39;output e il livello di protezione può essere impostato dal distributore dei contenuti. Se si specifica &quot;Obbligatorio&quot; e si tenta di riprodurre il contenuto su un Macintosh, il client non riproduce il contenuto su dispositivi esterni. Tuttavia, i contenuti verranno riprodotti sui monitor interni.

Se si specifica &quot;Obbligatorio&quot; e si tenta di riprodurre su Linux, il client non riproduce il contenuto su alcun dispositivo perché non è possibile distinguere tra dispositivi interni ed esterni.

Se si specifica &quot;Usa se disponibile&quot;, la protezione dell&#39;output viene attivata laddove possibile. Ad esempio, sui computer Windows che supportano il protocollo COPP (Certified Output Protection Protocol), il contenuto viene trasmesso con protezione dell&#39;output a uno schermo esterno. Questo esempio è talvolta noto come &quot;controllo di output selezionabile&quot;.
