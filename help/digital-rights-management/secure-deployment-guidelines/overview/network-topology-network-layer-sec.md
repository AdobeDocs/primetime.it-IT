---
description: Le vulnerabilità relative alla sicurezza di rete sono tra le prime minacce per qualsiasi server applicazioni che si affaccia su Internet o su una rete Intranet e pertanto è necessario proteggere gli host della rete da tali vulnerabilità.
title: Protezione a livello di rete
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---

# Protezione a livello di rete{#network-layer-security}

Le vulnerabilità relative alla sicurezza di rete sono tra le prime minacce per qualsiasi server applicazioni che si affaccia su Internet o su una rete Intranet e pertanto è necessario proteggere gli host della rete da tali vulnerabilità.

Di seguito sono riportate alcune tecniche comuni che riducono le vulnerabilità relative alla sicurezza della rete:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_djf_lhz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Tecnica </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descrizione </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Zone demilitarizzate (DMZ) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La segmentazione deve esistere in almeno due livelli con il server applicazioni utilizzato per eseguire Adobe Primetime DRM quando Primetime DRM si trova dietro il firewall interno. È necessario separare la rete esterna dalla DMZ che include i server Web e i server Web devono essere separati dalla rete interna. Potete utilizzare i firewall per implementare questi livelli di separazione. </p> <p>Puoi classificare e controllare il traffico che attraversa ogni livello di rete per garantire che sia consentito solo il minimo assoluto di dati richiesti. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Indirizzi IP privati </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Utilizzare Network Address Translation (NAT) con indirizzi IP privati RFC 1918 sui server applicazioni DRM Primetime. Puoi assegnare indirizzi IP privati (10.0.0.0/8, 172.16.0.0/12 e 192.168.0.0/16) per rendere più difficile per un utente malintenzionato indirizzare il traffico da e verso un host interno NAT tramite Internet. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Firewall </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Di seguito sono riportati alcuni criteri da considerare durante la selezione di una soluzione firewall: </p> <p class="- topic/p "> 
     <ul class="- topic/ul " id="ul_wjf_lhz_n4"> 
      <li class="- topic/li " id="li_A620D0B635384590BA7804F9720D04D0">Implementa firewall che supportano i server proxy e/o l’ispezione con conservazione dello stato, anziché semplici soluzioni di filtro dei pacchetti. </li> 
      <li class="- topic/li " id="li_3E4F814A30C047539185C23F4F57C282">Utilizza un firewall che supporti un paradigma di sicurezza in cui puoi negare tutti i servizi, ad eccezione di quelli esplicitamente consentiti. </li> 
      <li class="- topic/li " id="li_96160B3F14C4425397F017AF93FABE32">Implementare una soluzione firewall con doppia o multi-homed. Questa architettura offre il massimo livello di sicurezza e impedisce agli utenti non autorizzati di aggirare la protezione del firewall. </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
