---
seo-title: Protocolli di rete utilizzati da  Adobe Access
title: Protocolli di rete utilizzati da  Adobe Access
uuid: 4f2ee3f5-6758-4fbe-b5cd-cead1e5ccde8
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---


# Protocolli di rete utilizzati da  accesso al Adobe {#network-protocols-used-by-adobe-access}

Quando si configura un&#39;architettura di rete protetta, i protocolli di rete riportati nella tabella seguente sono necessari per l&#39;interazione tra  accesso al Adobe e altri sistemi della rete aziendale.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-itc-33z-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Protocollo </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Use </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTP </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">I client Flash Player ,  Adobe AIR® e  Adobe Primetime comunicano con  Adobe Access via HTTP. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTPS (facoltativo) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">I client Flash Player,  Adobe AIR e  Adobe Primetime possono utilizzare HTTPS per comunicare con  accesso al Adobe, tuttavia, HTTPS (SSL) non è richiesto a meno che non sia necessario il supporto per i client FMRMS 1.x. Consultate le note nella tabella <a href="network-topology-firewall-rules.md" format="dita" scope="local"> URL in arrivo</a> e <a href="network-topology-nw-protocols.md"> Configurazione di SSL</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>