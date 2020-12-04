---
description: Le vulnerabilità di sicurezza della rete sono tra le prime minacce a qualsiasi server applicazioni rivolto a Internet o Intranet e devi rendere più rigidi gli host presenti sulla rete rispetto a tali vulnerabilità.
seo-description: Le vulnerabilità di sicurezza della rete sono tra le prime minacce a qualsiasi server applicazioni rivolto a Internet o Intranet e devi rendere più rigidi gli host presenti sulla rete rispetto a tali vulnerabilità.
seo-title: Protezione dei livelli di rete
title: Protezione dei livelli di rete
uuid: c750c595-a784-47ce-be0b-17b8d60c5753
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---


# Protezione del livello di rete{#network-layer-security}

Le vulnerabilità di sicurezza della rete sono tra le prime minacce a qualsiasi server applicazioni rivolto a Internet o Intranet e devi rendere più rigidi gli host presenti sulla rete rispetto a tali vulnerabilità.

Di seguito sono riportate alcune tecniche comuni per ridurre le vulnerabilità di sicurezza della rete:

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">La segmentazione deve esistere in almeno due livelli con il server applicazione utilizzato per eseguire  Adobe Primetime DRM quando Primetime DRM è protetto da un firewall interno. È necessario separare la rete esterna dalla rete perimetrale che include i server Web e i server Web devono essere separati dalla rete interna. Potete usare i firewall per implementare questi livelli di separazione. </p> <p>Potete classificare e controllare il traffico che passa attraverso ciascun livello di rete per garantire che sia consentito solo il minimo assoluto di dati richiesti. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Indirizzi IP privati </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Utilizzate Network Address Translation (NAT) con indirizzi IP privati RFC 1918 sui server applicazione DRM di Primetime. Potete assegnare indirizzi IP privati (10.0.0.0/8, 172.16.0.0/12 e 192.168.0.0/16) per rendere più difficile per un utente malintenzionato indirizzare il traffico da e verso un host interno NAT attraverso Internet. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Firewall </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Di seguito sono riportati alcuni criteri da tenere in considerazione per la selezione di una soluzione firewall: </p> <p class="- topic/p "> 
     <ul class="- topic/ul " id="ul_wjf_lhz_n4"> 
      <li class="- topic/li " id="li_A620D0B635384590BA7804F9720D04D0">Implementate firewall che supportano server proxy e/o ispezione dello stato, invece di semplici soluzioni di filtraggio dei pacchetti. </li> 
      <li class="- topic/li " id="li_3E4F814A30C047539185C23F4F57C282">Utilizzare un firewall che supporta un paradigma di protezione in cui è possibile negare tutti i servizi, ad eccezione dei servizi consentiti in modo esplicito. </li> 
      <li class="- topic/li " id="li_96160B3F14C4425397F017AF93FABE32">Implementate una soluzione firewall che sia a due o più host. Questa architettura offre il massimo livello di protezione e impedisce agli utenti non autorizzati di aggirare la protezione del firewall. </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

