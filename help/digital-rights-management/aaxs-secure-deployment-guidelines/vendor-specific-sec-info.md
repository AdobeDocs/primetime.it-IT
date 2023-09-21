---
title: Informazioni di sicurezza specifiche del fornitore
description: Informazioni di sicurezza specifiche del fornitore
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# Informazioni di sicurezza specifiche del fornitore{#vendor-specific-security-information}

Questa sezione contiene informazioni relative alla protezione dei sistemi operativi e dei server applicazioni incorporati nella soluzione Adobe Access.

Utilizzare i collegamenti forniti in questa sezione per trovare informazioni sulla protezione specifiche per il sistema operativo e il server applicazioni.

## Informazioni sulla sicurezza del sistema operativo {#section-B6D9D6CEA7CC42A8A20346600EFB5E4E}

Quando si protegge il sistema operativo, è necessario implementare con attenzione le misure descritte dal fornitore del sistema operativo, tra cui:

* Definizione e controllo di utenti, ruoli e privilegi
* Registri di monitoraggio e audit trail
* Rimozione di servizi e applicazioni non necessari
* Backup dei file

Per informazioni sulla protezione dei sistemi operativi supportati da Adobe Access, vedere le risorse in questa tabella.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-ugl-kjz-n4"> 
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

Nella tabella seguente vengono descritti alcuni approcci potenziali per ridurre al minimo le vulnerabilità di sicurezza presenti nel sistema operativo.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-whl-kjz-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Elemento </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descrizione </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Patch di sicurezza </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Esiste un rischio maggiore che un utente non autorizzato possa accedere all'Application Server se le patch e gli aggiornamenti di sicurezza del fornitore non vengono applicati in modo tempestivo. Verificare le patch di sicurezza prima di applicarle ai server di produzione. </p> <p class="- topic/p ">È inoltre possibile creare criteri e procedure per verificare e installare regolarmente le patch. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Software antivirus </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Gli scanner antivirus possono identificare i file infetti eseguendo la scansione alla ricerca di una firma o osservando un comportamento insolito. Gli scanner conservano le firme dei virus in un file, in genere memorizzato sul disco rigido locale. Poiché i nuovi virus vengono individuati spesso, è necessario aggiornare frequentemente questo file affinché il programma antivirus possa identificare tutti i virus correnti. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">NTP (Network Time Protocol) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Per il corretto funzionamento e per l'analisi forense, è necessario mantenere l'ora esatta sui server di accesso Adobe e sui pacchetti di accesso Adobe. Utilizzare una versione protetta di NTP per sincronizzare l'ora su tutti i sistemi connessi a Internet. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Informazioni sulla sicurezza del server applicazioni {#section-EBB4EF371CFF4A848694CC240B23D404}

Quando si protegge il server applicazioni, è necessario implementare le misure descritte dal fornitore del server, tra cui:

* Utilizzo di un nome utente amministratore non ovvio
* Disabilitazione dei servizi non necessari
* Protezione di Console Manager
* Abilitazione dei cookie protetti
* Chiusura delle porte non necessarie
* Limitazione delle interfacce amministrative per indirizzi IP o domini
* Utilizzo di Java™ Security Manager
