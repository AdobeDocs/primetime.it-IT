---
title: Informazioni di sicurezza specifiche per il fornitore
description: Informazioni di sicurezza specifiche per il fornitore
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---


# Informazioni di sicurezza specifiche per il fornitore{#vendor-specific-security-information}

Questa sezione contiene informazioni relative alla sicurezza sui sistemi operativi e i server applicativi incorporati nella soluzione Adobe Access.

Utilizzare i collegamenti forniti in questa sezione per trovare informazioni di sicurezza specifiche del fornitore per il sistema operativo e il server applicazioni.

## Informazioni sulla sicurezza del sistema operativo {#section-B6D9D6CEA7CC42A8A20346600EFB5E4E}

Quando proteggi il sistema operativo, implementa con attenzione le misure descritte dal fornitore del sistema operativo, tra cui:

* Definizione e controllo di utenti, ruoli e privilegi
* Monitoraggio dei registri e dei percorsi di controllo
* Rimozione di servizi e applicazioni superflui
* Backup dei file

Per informazioni sulla sicurezza dei sistemi operativi supportati da Adobe Access, vedere le risorse presenti in questa tabella.

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">Guida alla sicurezza di Windows Server 2008</i> </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Red Hat® Enterprise Linux® 5.4, 5.5 e 5.6. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">Guida alla sicurezza di Red Hat Enterprise Linux 5</i> </p> </td> 
  </tr> 
 </tbody> 
</table>

Nella tabella seguente sono descritti alcuni approcci potenziali per ridurre al minimo le vulnerabilità di sicurezza riscontrate nel sistema operativo.

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Esiste un rischio maggiore che un utente non autorizzato possa accedere al server dell'applicazione se le patch e gli aggiornamenti di sicurezza del fornitore non vengono applicati in modo tempestivo. Verifica le patch di sicurezza prima di applicarle ai server di produzione. </p> <p class="- topic/p ">Inoltre, crea criteri e procedure per verificare e installare le patch regolarmente. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Software di protezione contro i virus </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Gli scanner di virus possono identificare i file infetti digitalizzando una firma o guardando per un comportamento insolito. Gli scanner conservano le firme dei virus in un file, che di solito è memorizzato sul disco rigido locale. Poiché i nuovi virus vengono spesso scoperti, è necessario aggiornare frequentemente questo file affinché lo scanner antivirus identifichi tutti i virus correnti. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Network Time Protocol (NTP) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Per il corretto funzionamento e l'analisi forense, è necessario mantenere un tempo preciso sui server di accesso agli Adobi e sui pacchetti di accesso agli Adobi. Utilizzare una versione sicura di NTP per sincronizzare l'ora su tutti i sistemi connessi a Internet. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Informazioni sulla sicurezza del server applicazioni {#section-EBB4EF371CFF4A848694CC240B23D404}

Quando si protegge il server applicazioni, è necessario implementare le misure descritte dal fornitore del server, tra cui:

* Utilizzo di un nome utente amministratore non ovvio
* Disattivazione dei servizi non necessari
* Protezione della console manager
* Abilitazione dei cookie sicuri
* Chiusura delle porte non necessarie
* Limitazione delle interfacce amministrative per indirizzi IP o domini
* Utilizzo di Java™ Security Manager

