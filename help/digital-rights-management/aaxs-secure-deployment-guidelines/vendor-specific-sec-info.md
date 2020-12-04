---
seo-title: Informazioni di sicurezza specifiche per il fornitore
title: Informazioni di sicurezza specifiche per il fornitore
uuid: 23186770-c73a-4802-bc30-fa9e4b47d9ba
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---


# Informazioni di sicurezza specifiche per il fornitore{#vendor-specific-security-information}

Questa sezione contiene informazioni relative alla sicurezza sui sistemi operativi e i server applicazione incorporati nella soluzione di accesso al Adobe .

Utilizzare i collegamenti forniti in questa sezione per trovare informazioni di sicurezza specifiche per il fornitore per il sistema operativo e il server applicazioni in uso.

## Informazioni sulla sicurezza del sistema operativo {#section-B6D9D6CEA7CC42A8A20346600EFB5E4E}

Durante la protezione del sistema operativo, implementate con attenzione le misure descritte dal fornitore del sistema operativo, tra cui:

* Definizione e controllo di utenti, ruoli e privilegi
* Monitoraggio dei registri e dei percorsi di controllo
* Rimozione di servizi e applicazioni non necessari
* Backup dei file

Per informazioni di sicurezza sui sistemi operativi supportati da  Adobe Access, vedere le risorse in questa tabella.

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Esiste un rischio maggiore che un utente non autorizzato possa accedere al server applicazione se le patch e gli aggiornamenti di sicurezza del fornitore non vengono applicati in modo tempestivo. Verificate le patch di protezione prima di applicarle ai server di produzione. </p> <p class="- topic/p ">Inoltre, potete creare criteri e procedure per verificare e installare le patch su base regolare. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Software antivirus </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Gli scanner antivirus possono identificare i file infetti digitalizzando una firma o guardando per un comportamento insolito. Gli scanner conservano le firme antivirus in un file, solitamente memorizzato sul disco rigido locale. Poiché i nuovi virus vengono spesso scoperti, è necessario aggiornare frequentemente questo file per consentire allo scanner virus di identificare tutti i virus correnti. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Network Time Protocol (NTP) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Sia per il corretto funzionamento che per l'analisi forense, mantenete un tempo preciso sui server di accesso  Adobe e sui pacchetti di accesso  Adobe. Utilizzare una versione protetta di NTP per sincronizzare l'ora su tutti i sistemi connessi a Internet. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Informazioni sulla protezione del server applicazioni {#section-EBB4EF371CFF4A848694CC240B23D404}

Durante la protezione del server applicazioni, è necessario implementare le misure descritte dal fornitore del server, tra cui:

* Utilizzo di un nome utente amministratore non ovvio
* Disattivazione di servizi non necessari
* Protezione del console manager
* Abilitazione dei cookie protetti
* Chiusura delle porte non necessarie
* Limitazione delle interfacce amministrative per indirizzi IP o domini
* Utilizzo di Java™ Security Manager

