---
title: Protocolli di rete utilizzati da Adobe Access
description: Protocolli di rete utilizzati da Adobe Access
copied-description: true
exl-id: f065690d-6fa1-43a7-8aa8-a1ccd68e998d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# Protocolli di rete utilizzati da Adobe Access {#network-protocols-used-by-adobe-access}

Quando si configura un&#39;architettura di rete sicura, i protocolli di rete riportati nella tabella seguente sono necessari per l&#39;interazione tra Adobe Access e altri sistemi della rete aziendale.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-itc-33z-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Protocollo </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Utilizzare </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTP </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">I client Flash Player, Adobe AIR® e Adobe Primetime comunicano con Adobe Access tramite HTTP. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTPS (facoltativo) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">I client Flash Player, Adobe AIR e Adobe Primetime possono utilizzare HTTPS per la comunicazione con Adobe Access. Tuttavia, HTTPS (SSL) non è necessario, a meno che non sia necessario il supporto per i client FMRMS 1.x. Vedere le note nella tabella <a href="network-topology-firewall-rules.md" format="dita" scope="local"> URL in ingresso</a> e <a href="network-topology-nw-protocols.md"> Configurazione di SSL</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>
