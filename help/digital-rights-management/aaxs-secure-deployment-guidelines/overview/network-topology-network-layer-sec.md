---
title: Sicurezza a livello di rete
description: Sicurezza a livello di rete
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---


# Sicurezza a livello di rete{#network-layer-security}

Le vulnerabilità relative alla sicurezza della rete costituiscono una delle prime minacce per qualsiasi server applicativo rivolto a Internet o Intranet. Questa sezione descrive il processo di indurimento degli host sulla rete rispetto a queste vulnerabilità. Si occupa della segmentazione della rete, dell&#39;indurimento dello stack del protocollo di controllo della trasmissione/protocollo Internet (TCP/IP) e dell&#39;uso di firewall per la protezione dell&#39;host.

Questa tabella descrive le tecniche comuni che riducono le vulnerabilità relative alla sicurezza della rete.

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La segmentazione deve esistere in almeno due livelli con l'application server utilizzato per eseguire Adobe Access posizionato dietro il firewall interno. Separare la rete esterna dalla rete DMZ che contiene i server web, che a loro volta devono essere separati dalla rete interna. Usa i firewall per implementare i livelli di separazione. Dividi in categorie e controlla il traffico che passa attraverso ciascun livello di rete per garantire che sia consentito solo il minimo assoluto di dati richiesti. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Indirizzi IP privati </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Utilizza NAT (Network Address Translation) con indirizzi IP privati RFC 1918 sui server delle applicazioni Adobe Access. Assegna indirizzi IP privati (10.0.0.0/8, 172.16.0.0/12 e 192.168.0.0/16) per rendere più difficile per un aggressore indirizzare il traffico da e verso un host interno NAT attraverso Internet. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Firewall </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Utilizza i seguenti criteri per selezionare una soluzione firewall: </p> <p class="- topic/p "> 
     <ul class="- topic/ul " id="ul-wjf-lhz-n4"> 
      <li class="- topic/li " id="li-8031632160F44037B092988183139202"> <p class="- topic/p ">Implementa firewall che supportano i server proxy e/o l’ispezione dello stato invece di semplici soluzioni di filtraggio dei pacchetti. </p> </li> 
      <li class="- topic/li " id="li-B65CBB92113E4503B79EB194C34FCA50"> <p class="- topic/p ">Utilizzare un firewall che supporta un paradigma di sicurezza in cui è possibile negare tutti i servizi, tranne quelli esplicitamente consentiti. </p> </li> 
      <li class="- topic/li " id="li-5CE4C7B65D84410DB4BE966FD8922993"> <p class="- topic/p ">Implementa una soluzione firewall con doppio percorso o con più percorsi. Questa architettura fornisce il massimo livello di sicurezza e aiuta a evitare che utenti non autorizzati bypassino la sicurezza del firewall. </p> </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

