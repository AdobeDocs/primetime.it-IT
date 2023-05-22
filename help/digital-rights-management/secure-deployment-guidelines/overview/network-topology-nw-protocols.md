---
description: Quando si configura un'architettura di rete sicura, i protocolli di rete sono necessari per l'interazione tra Adobe Primetime DRM e altri sistemi della rete aziendale.
title: Protocolli di rete Adobe Primetime DRM
exl-id: d5720ef4-6845-4a62-940a-9d8ba9b43b13
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# Protocolli di rete Adobe Primetime DRM {#adobe-primetime-drm-network-protocols}

Quando si configura un&#39;architettura di rete sicura, i protocolli di rete sono necessari per l&#39;interazione tra Adobe Primetime DRM e altri sistemi della rete aziendale.

Quando si configura un&#39;architettura di rete sicura, per questa interazione sono necessari i protocolli di rete seguenti:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_itc_33z_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Protocollo </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Utilizzare </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTP </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">I client Flash Player, Adobe AIR® e Adobe Primetime comunicano con Primetime DRM tramite HTTP. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTPS (facoltativo) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">I client Flash Player, Adobe AIR e Adobe Primetime possono utilizzare HTTPS per comunicare con Primetime DRM; non è necessario utilizzare HTTPS (SSL), a meno che non si supportino i client FMRMS 1.x. Per ulteriori informazioni, consulta <a href="../../secure-deployment-guidelines/overview/network-topology-firewall-rules.md" format="dita" scope="local"> URL in ingresso </a> e la configurazione di SSL. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Porte per server applicazioni {#ports-for-application-servers}

È possibile configurare il server licenze Adobe Primetime DRM in modo che utilizzi qualsiasi porta di rete.

Queste porte devono essere attivate o disattivate nel firewall interno, a seconda della funzionalità di rete che si desidera consentire ai client che si connettono al server applicazioni che esegue DRM di Primetime.

## Configurazione di SSL {#configuring-ssl}

Secure Sockets Layer (SSL) è necessario solo se è necessario il supporto per i client Flash Media Rights Management Server 1.x.

Per il server chiavi Adobe Primetime DRM è necessario SSL con autenticazione client. Per ulteriori informazioni, consulta [Utilizzo di Adobe Primetime DRM Key Server](../../using-the-drm-key-server/requirements.md).
