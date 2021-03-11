---
description: Le vulnerabilità relative alla sicurezza della rete costituiscono una delle prime minacce per qualsiasi server applicativo rivolto a Internet o Intranet e devi inoltre proteggere gli host della rete da tali vulnerabilità.
title: Sicurezza a livello di rete
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---


# Sicurezza a livello di rete{#network-layer-security}

Le vulnerabilità relative alla sicurezza della rete costituiscono una delle prime minacce per qualsiasi server applicativo rivolto a Internet o Intranet e devi inoltre proteggere gli host della rete da tali vulnerabilità.

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La segmentazione deve esistere in almeno due livelli con il server applicazioni utilizzato per eseguire Adobe Primetime DRM quando Primetime DRM è dietro il firewall interno. È necessario separare la rete esterna dalla rete DMZ che include i server web e i server web devono essere separati dalla rete interna. Potete usare i firewall per implementare questi livelli di separazione. </p> <p>Puoi classificare e controllare il traffico che passa attraverso ogni livello di rete per garantire che sia consentito solo il minimo assoluto di dati richiesti. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Indirizzi IP privati </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Utilizza NAT (Network Address Translation) con indirizzi IP privati RFC 1918 sui server di applicazioni DRM di Primetime. È possibile assegnare indirizzi IP privati (10.0.0.0/8, 172.16.0.0/12 e 192.168.0.0/16) per rendere più difficile per un aggressore indirizzare il traffico da e verso un host interno NAT attraverso Internet. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Firewall </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Di seguito sono riportati alcuni criteri da tenere in considerazione quando si seleziona una soluzione firewall: </p> <p class="- topic/p "> 
     <ul class="- topic/ul " id="ul_wjf_lhz_n4"> 
      <li class="- topic/li " id="li_A620D0B635384590BA7804F9720D04D0">Implementa firewall che supportano i server proxy e/o l’ispezione dello stato, invece di semplici soluzioni di filtraggio dei pacchetti. </li> 
      <li class="- topic/li " id="li_3E4F814A30C047539185C23F4F57C282">Utilizzare un firewall che supporta un paradigma di sicurezza in cui è possibile negare tutti i servizi, ad eccezione dei servizi esplicitamente consentiti. </li> 
      <li class="- topic/li " id="li_96160B3F14C4425397F017AF93FABE32">Implementa una soluzione firewall con doppio percorso o con più percorsi. Questa architettura fornisce il massimo livello di sicurezza e impedisce agli utenti non autorizzati di bypassare la protezione del firewall. </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

