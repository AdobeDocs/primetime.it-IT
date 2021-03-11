---
description: Quando si configura un'architettura di rete sicura, sono necessari protocolli di rete per l'interazione tra Adobe Primetime DRM e altri sistemi della rete aziendale.
title: Protocolli di rete Adobe Primetime DRM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---


# Protocolli di rete Adobe Primetime DRM {#adobe-primetime-drm-network-protocols}

Quando si configura un&#39;architettura di rete sicura, sono necessari protocolli di rete per l&#39;interazione tra Adobe Primetime DRM e altri sistemi della rete aziendale.

Quando si configura un&#39;architettura di rete protetta, per questa interazione sono necessari i seguenti protocolli di rete:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_itc_33z_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Protocollo </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Utilizzo </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTP </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">I client Flash Player, Adobe AIR® e Adobe Primetime comunicano con DRM di Primetime via HTTP. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTPS (facoltativo) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">I client Flash Player, Adobe AIR e Adobe Primetime possono utilizzare HTTPS per comunicare con Primetime DRM; HTTPS (SSL) è richiesto solo se sono supportati i client FMRMS 1.x. Per ulteriori informazioni, consulta <a href="../../secure-deployment-guidelines/overview/network-topology-firewall-rules.md" format="dita" scope="local"> URL in arrivo </a> e Configurazione di SSL. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Porte per server applicazioni {#ports-for-application-servers}

Puoi configurare il server di licenza Adobe Primetime DRM per l&#39;utilizzo di qualsiasi porta di rete.

Queste porte devono essere abilitate o disabilitate nel firewall interno, a seconda della funzionalità di rete che si desidera consentire ai client che si connettono al server applicazioni che esegue Primetime DRM.

## Configurazione di SSL {#configuring-ssl}

Il Secure Sockets Layer (SSL) è necessario solo se è necessario il supporto per i client Flash Media Rights Management Server 1.x.

SSL con autenticazione client è necessario per il server chiavi DRM di Adobe Primetime. Per ulteriori informazioni, consulta [Utilizzo del server chiavi DRM di Adobe Primetime](../../using-the-drm-key-server/requirements.md).