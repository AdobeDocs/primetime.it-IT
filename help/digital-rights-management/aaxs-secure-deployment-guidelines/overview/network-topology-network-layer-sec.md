---
title: Protezione a livello di rete
description: Protezione a livello di rete
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# Protezione a livello di rete{#network-layer-security}

Le vulnerabilità relative alla sicurezza di rete sono tra le prime minacce per qualsiasi server applicazioni che si affaccia su Internet o su Intranet. Questa sezione descrive il processo di protezione degli host della rete da queste vulnerabilità. Affronta la segmentazione della rete, l&#39;irrigidimento dello stack TCP/IP (Transmission Control Protocol/Internet Protocol) e l&#39;uso di firewall per la protezione dell&#39;host.

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La segmentazione deve esistere in almeno due livelli con il server applicazioni utilizzato per eseguire Accesso Adobe posizionato dietro il firewall interno. Separare la rete esterna dalla DMZ che contiene i server web, che a sua volta deve essere separata dalla rete interna. Utilizzate i firewall per implementare i livelli di separazione. Categorizza e controlla il traffico che attraversa ogni livello di rete per garantire che sia consentito solo il minimo assoluto di dati richiesti. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Indirizzi IP privati </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Utilizza Network Address Translation (NAT) con indirizzi IP privati RFC 1918 sui server applicazioni Adobe Access. Assegna indirizzi IP privati (10.0.0.0/8, 172.16.0.0/12 e 192.168.0.0/16) per rendere più difficile per un utente malintenzionato indirizzare il traffico da e verso un host interno NAT tramite Internet. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Firewall </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Utilizzare i criteri seguenti per selezionare una soluzione firewall: </p> <p class="- topic/p "> 
     <ul class="- topic/ul " id="ul-wjf-lhz-n4"> 
      <li class="- topic/li " id="li-8031632160F44037B092988183139202"> <p class="- topic/p ">Implementa firewall che supportano i server proxy e/o l’ispezione con conservazione dello stato anziché semplici soluzioni di filtro dei pacchetti. </p> </li> 
      <li class="- topic/li " id="li-B65CBB92113E4503B79EB194C34FCA50"> <p class="- topic/p ">Utilizzare un firewall che supporti un paradigma di sicurezza in cui è possibile negare tutti i servizi ad eccezione di quelli esplicitamente consentiti. </p> </li> 
      <li class="- topic/li " id="li-5CE4C7B65D84410DB4BE966FD8922993"> <p class="- topic/p ">Implementare una soluzione firewall con doppia o multi-homed. Questa architettura offre il massimo livello di protezione e consente di evitare che utenti non autorizzati aggirino la protezione del firewall. </p> </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
