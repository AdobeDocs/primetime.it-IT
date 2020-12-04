---
seo-title: Protezione dei livelli di rete
title: Protezione dei livelli di rete
uuid: bd53bccf-1130-4189-97ec-4259bd25762f
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---


# Protezione del livello di rete{#network-layer-security}

Le vulnerabilità di sicurezza della rete sono tra le prime minacce a qualsiasi server applicazioni rivolto a Internet o Intranet. Questa sezione descrive il processo di indurimento degli host sulla rete rispetto a tali vulnerabilità. Si occupa della segmentazione della rete, del protocollo di controllo della trasmissione/del protocollo Internet (TCP/IP) e dell&#39;uso di firewall per la protezione dell&#39;host.

Nella tabella seguente sono illustrate le tecniche più comuni per ridurre le vulnerabilità di sicurezza della rete.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-djf-lhz-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Tecnica </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descrizione </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Zone demilitarizzate (DMZ) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La segmentazione deve esistere in almeno due livelli con il server applicazione utilizzato per eseguire  Accesso Adobe posizionato dietro il firewall interno. Separare la rete esterna dalla rete perimetrale che contiene i server Web, che a sua volta deve essere separata dalla rete interna. Usate i firewall per implementare i livelli di separazione. Categorizzare e controllare il traffico che passa attraverso ciascun livello di rete per garantire che sia consentito solo il minimo assoluto di dati richiesti. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Indirizzi IP privati </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Utilizzate Network Address Translation (NAT) con gli indirizzi IP privati RFC 1918 sui server dell'applicazione di accesso  Adobe. Assegnate indirizzi IP privati (10.0.0.0/8, 172.16.0.0/12 e 192.168.0.0/16) per rendere più difficile per un utente malintenzionato indirizzare il traffico da e verso un host interno NAT attraverso Internet. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Firewall </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Utilizzate i seguenti criteri per selezionare una soluzione firewall: </p> <p class="- topic/p "> 
     <ul class="- topic/ul " id="ul-wjf-lhz-n4"> 
      <li class="- topic/li " id="li-8031632160F44037B092988183139202"> <p class="- topic/p ">Implementate firewall che supportano server proxy e/o ispezione dello stato invece di semplici soluzioni di filtraggio dei pacchetti. </p> </li> 
      <li class="- topic/li " id="li-B65CBB92113E4503B79EB194C34FCA50"> <p class="- topic/p ">Utilizzare un firewall che supporta un paradigma di protezione in cui è possibile negare tutti i servizi tranne quelli consentiti in modo esplicito. </p> </li> 
      <li class="- topic/li " id="li-5CE4C7B65D84410DB4BE966FD8922993"> <p class="- topic/p ">Implementate una soluzione firewall che sia a due o più host. Questa architettura fornisce il massimo livello di protezione e aiuta a impedire che utenti non autorizzati scavalchino la protezione del firewall. </p> </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

