---
description: I sistemi operativi e i server applicazioni sono inclusi nella soluzione Adobe Primetime DRM.
title: Informazioni di sicurezza specifiche per il fornitore
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---


# Informazioni di sicurezza specifiche per il fornitore{#vendor-specific-security-information}

I sistemi operativi e i server applicazioni sono inclusi nella soluzione Adobe Primetime DRM.

Per informazioni sulla sicurezza specifiche per il fornitore per il sistema operativo e il server applicazioni, vedere Utilizzo del server chiavi DRM di Adobe Primetime.

## Informazioni sulla sicurezza del sistema operativo {#section_53CAD802FCA54C4D8CE0C4E1B3045E52}

Quando si protegge il sistema operativo, è necessario implementare le misure descritte dal fornitore del sistema operativo in uso.

Ecco alcune delle misure:

* Definizione e controllo di utenti, ruoli e privilegi
* Monitoraggio dei registri e dei percorsi di controllo
* Rimozione di servizi e applicazioni superflui
* Backup dei file

Ecco alcune informazioni sui sistemi operativi supportati da Adobe Primetime DRM:

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">Guida alla sicurezza di Windows Server 2008</i> </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Red Hat® Enterprise Linux® 5.4, 5.5 e 5.6. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">Guida alla sicurezza di Red Hat Enterprise Linux 5</i> </p> </td> 
  </tr> 
 </tbody> 
</table>

Ecco alcune informazioni sugli approcci per ridurre al minimo le vulnerabilità di sicurezza nel sistema operativo:

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">C'è un rischio maggiore che un utente non autorizzato possa accedere al server dell'applicazione se le patch e gli aggiornamenti di sicurezza del fornitore non vengono applicati in modo tempestivo. </p> <p>Nota:  Assicurati di testare le patch di sicurezza prima di applicarle ai server di produzione. </p> <p class="- topic/p ">È necessario creare criteri e procedure per verificare e installare regolarmente le patch. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Software di protezione contro i virus </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Gli scanner di virus possono identificare i file infetti digitalizzando una firma o un comportamento insolito. </p> <p>Gli scanner conservano le firme dei virus in un file, che di solito è memorizzato sul disco rigido locale. Vengono spesso rilevati nuovi virus, pertanto è necessario assicurarsi che il file venga aggiornato regolarmente. In questo modo, gli scanner antivirus possono sempre identificare tutti i virus correnti. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Network Time Protocol (NTP) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Per un corretto funzionamento e un'analisi forense, assicurati di avere un tempo preciso sui server e sui pacchetti DRM di Primetime. Utilizzare una versione sicura di NTP per sincronizzare l'ora DRM di Primetime su tutti i sistemi collegati a Internet. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Informazioni sulla sicurezza del server applicazioni {#section_22986936F1A547CEAB2D97E9E9D4825C}

Quando si protegge il server applicazioni, è necessario implementare le misure descritte dal fornitore del server.

Ecco alcune delle misure seguenti:

* Utilizzo di un nome utente amministratore non ovvio
* Disattivazione dei servizi non necessari
* Protezione della console manager
* Abilitazione dei cookie sicuri
* Chiusura delle porte non necessarie
* Limitazione delle interfacce amministrative per indirizzi IP o domini
* Utilizzo di Java™ Security Manager

