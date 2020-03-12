---
description: I sistemi operativi e i server applicazioni sono inclusi nella soluzione Adobe Primetime DRM.
seo-description: I sistemi operativi e i server applicazioni sono inclusi nella soluzione Adobe Primetime DRM.
seo-title: Informazioni di sicurezza specifiche per il fornitore
title: Informazioni di sicurezza specifiche per il fornitore
uuid: 331baa42-5e19-40a5-bc74-0b1a2cb9370e
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Informazioni di sicurezza specifiche per il fornitore{#vendor-specific-security-information}

I sistemi operativi e i server applicazioni sono inclusi nella soluzione Adobe Primetime DRM.

Per informazioni sulla sicurezza specifiche per il fornitore per il sistema operativo e il server applicazione in uso, vedere Utilizzo del server chiavi DRM di Adobe Primetime.

## Informazioni sulla sicurezza del sistema operativo {#section_53CAD802FCA54C4D8CE0C4E1B3045E52}

Quando si protegge il sistema operativo, è necessario implementare le misure descritte dal fornitore del sistema operativo in uso.

Di seguito sono riportate alcune delle misure:

* Definizione e controllo di utenti, ruoli e privilegi
* Monitoraggio dei registri e dei percorsi di controllo
* Rimozione di servizi e applicazioni non necessari
* Backup dei file

Seguono alcune informazioni sui sistemi operativi supportati da Adobe Primetime DRM:

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Esiste un rischio maggiore che un utente non autorizzato possa accedere al server dell'applicazione se le patch e gli aggiornamenti di sicurezza del fornitore non vengono applicati in modo tempestivo. </p> <p>Nota:  Prima di applicarle ai server di produzione, verificare le patch di protezione. </p> <p class="- topic/p ">È necessario creare criteri e procedure per controllare e installare regolarmente le patch. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Software antivirus </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Gli scanner antivirus possono identificare i file infetti digitalizzando una firma o un comportamento anomalo. </p> <p>Gli scanner conservano le firme antivirus in un file, solitamente memorizzato sul disco rigido locale. I nuovi virus vengono spesso scoperti, quindi è necessario assicurarsi che questo file sia aggiornato regolarmente. In questo modo, gli scanner antivirus possono sempre identificare tutti i virus correnti. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Network Time Protocol (NTP) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Per un corretto funzionamento e un'analisi forense, continuate a disporre di tempo accurato sui server e sui pacchetti DRM di Primetime. Utilizzare una versione protetta di NTP per sincronizzare l'ora DRM di Primetime su tutti i sistemi connessi a Internet. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Informazioni sulla protezione del server applicazioni {#section_22986936F1A547CEAB2D97E9E9D4825C}

Quando si protegge il server applicazioni, è necessario implementare le misure descritte dal fornitore del server.

Di seguito sono riportati alcuni provvedimenti:

* Utilizzo di un nome utente amministratore non ovvio
* Disattivazione di servizi non necessari
* Protezione del console manager
* Abilitazione dei cookie protetti
* Chiusura delle porte non necessarie
* Limitazione delle interfacce amministrative per indirizzi IP o domini
* Utilizzo di Java™ Security Manager

