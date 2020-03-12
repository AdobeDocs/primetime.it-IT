---
description: Quando si configura un'architettura di rete protetta, per l'interazione tra Adobe Primetime DRM e altri sistemi della rete aziendale sono necessari protocolli di rete.
seo-description: Quando si configura un'architettura di rete protetta, per l'interazione tra Adobe Primetime DRM e altri sistemi della rete aziendale sono necessari protocolli di rete.
seo-title: Protocolli di rete DRM di Adobe Primetime
title: Protocolli di rete DRM di Adobe Primetime
uuid: 8954e33c-83ac-4b40-9e45-005d4954b44e
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Protocolli di rete DRM di Adobe Primetime {#adobe-primetime-drm-network-protocols}

Quando si configura un&#39;architettura di rete protetta, per l&#39;interazione tra Adobe Primetime DRM e altri sistemi della rete aziendale sono necessari protocolli di rete.

Quando si configura un&#39;architettura di rete protetta, per questa interazione sono necessari i seguenti protocolli di rete:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_itc_33z_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Protocollo </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Use </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTP </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">I client Flash Player, Adobe AIR® e Adobe Primetime comunicano con Primetime DRM tramite HTTP. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTPS (facoltativo) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">I client Flash Player, Adobe AIR e Adobe Primetime possono utilizzare HTTPS per comunicare con Primetime DRM; HTTPS (SSL) è richiesto solo se si supportano i client FMRMS 1.x. Per ulteriori informazioni, consultate URL <a href="../../secure-deployment-guidelines/overview/network-topology-firewall-rules.md" format="dita" scope="local"> in arrivo </a> e Configurazione di SSL. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Porte per i server applicazioni {#ports-for-application-servers}

È possibile configurare il server delle licenze Adobe Primetime DRM in modo che utilizzi qualsiasi porta di rete.

Queste porte devono essere abilitate o disattivate sul firewall interno, a seconda della funzionalità di rete che si desidera consentire ai client che si connettono al server applicazione che esegue Primetime DRM.

## Configurazione di SSL {#configuring-ssl}

Il Secure Sockets Layer (SSL) è necessario solo se è richiesto il supporto per i client Flash Media Rights Management Server 1.x.

SSL con autenticazione client è richiesto per Adobe Primetime DRM Key Server. Per ulteriori informazioni, vedere [Utilizzo del server](../../using-the-drm-key-server/requirements.md)di chiavi DRM di Adobe Primetime.