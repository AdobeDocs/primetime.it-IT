---
description: I sistemi operativi e i server delle applicazioni sono inclusi nella soluzione Adobe Primetime DRM.
title: Informazioni di sicurezza specifiche del fornitore
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---

# Informazioni di sicurezza specifiche del fornitore{#vendor-specific-security-information}

I sistemi operativi e i server delle applicazioni sono inclusi nella soluzione Adobe Primetime DRM.

Per informazioni sulla sicurezza specifiche del fornitore per il sistema operativo e il server applicazioni, vedere Utilizzo del server chiavi Adobe Primetime DRM.

## Informazioni sulla sicurezza del sistema operativo {#section_53CAD802FCA54C4D8CE0C4E1B3045E52}

Quando si protegge il sistema operativo, è necessario implementare le misure descritte dal fornitore del sistema operativo.

Ecco alcune delle misure:

* Definizione e controllo di utenti, ruoli e privilegi
* Registri di monitoraggio e audit trail
* Rimozione di servizi e applicazioni non necessari
* Backup dei file

Di seguito sono riportate alcune informazioni sui sistemi operativi supportati da Adobe Primetime DRM:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_ugl_kjz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Sistema operativo </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Risorsa di sicurezza </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Microsoft® Windows Server® 2008 Enterprise o Standard Edition </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">Guida alla protezione di Windows Server 2008</i> </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Red Hat® Enterprise Linux® 5.4, 5.5 e 5.6. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">Guida alla sicurezza di Red Hat Enterprise Linux 5</i> </p> </td> 
  </tr> 
 </tbody> 
</table>

Seguono alcune informazioni sugli approcci per ridurre al minimo le vulnerabilità di sicurezza nel sistema operativo:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_whl_kjz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Elemento </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descrizione </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Patch di sicurezza </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Esiste un rischio maggiore che un utente non autorizzato possa accedere all'Application Server se le patch e gli aggiornamenti di sicurezza del fornitore non vengono applicati in modo tempestivo. </p> <p>Nota: verificare le patch di sicurezza prima di applicarle ai server di produzione. </p> <p class="- topic/p ">È necessario creare criteri e procedure per verificare e installare regolarmente le patch. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Software antivirus </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">I programmi antivirus possono identificare i file infetti tramite la ricerca di una firma o di un comportamento insolito. </p> <p>Gli scanner conservano le firme dei virus in un file, in genere memorizzato sul disco rigido locale. I nuovi virus vengono rilevati spesso, pertanto devi assicurarti che il file venga aggiornato regolarmente. In questo modo, i programmi antivirus possono sempre identificare tutti i virus correnti. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">NTP (Network Time Protocol) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Per il corretto funzionamento e l'analisi forense, mantenere l'ora esatta sui server e sui pacchetti DRM Primetime. Utilizzare una versione protetta di NTP per sincronizzare l'ora DRM di Primetime su tutti i sistemi connessi a Internet. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Informazioni sulla sicurezza del server applicazioni {#section_22986936F1A547CEAB2D97E9E9D4825C}

Quando si protegge il server applicazioni, è necessario implementare le misure descritte dal fornitore del server.

Ecco alcune di queste misure:

* Utilizzo di un nome utente amministratore non ovvio
* Disabilitazione dei servizi non necessari
* Protezione di Console Manager
* Abilitazione dei cookie protetti
* Chiusura delle porte non necessarie
* Limitazione delle interfacce amministrative per indirizzi IP o domini
* Utilizzo di Java™ Security Manager
