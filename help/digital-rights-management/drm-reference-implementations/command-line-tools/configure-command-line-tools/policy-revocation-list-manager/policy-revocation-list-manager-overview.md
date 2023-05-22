---
title: Gestione elenco revoche DRM
description: Gestione elenco revoche DRM
copied-description: true
exl-id: 5b17d195-30ca-4005-b710-83a6f77779a2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 0%

---

# Gestione elenco revoche DRM {#policy-revocation-list-manager}

Utilizzare lo strumento da riga di comando Gestione elenchi revoche DRM di Primetime ( [!DNL AdobeRevocationListManager.jar]) per creare e gestire elenchi di revoca e per verificare se i criteri sono stati revocati.

Prima dell’esecuzione [!DNL AdobeRevocationListManager.jar], è necessario impostare le proprietà in *Proprietà di Gestione elenchi aggiornamento criteri e Gestione elenchi di revoche* del file di configurazione.

>[!NOTE]
>
>È inoltre possibile specificare tutte le proprietà di Revocation List Manager dalla riga di comando.

## Utilizzo della riga di comando di Revocation List Manager {#revocation-list-manager-command-line-usage}

```
java -jar AdobeRevocationListManager.jar 
<i class="+ topic ph hi-d="" i "="">
 destfile 
 <i class="+ topic ph hi-d="" i "="">
  crlNumber [
  <i class="+ topic ph hi-d="" i "="">
   options] 
       java -jar AdobeRevocationListManager.jar -d 
   <i class="+ topic ph hi-d="" i "="">
     filename
   </i class="+ topic>
  </i class="+ topic>
 </i class="+ topic>
</i class="+ topic>
```

* `destfile` specifica il nome del file in cui vengono salvate le proprietà dell&#39;elenco di revoche.
* `crlNumber` rappresenta un numero di versione non negativo dell’elenco di revoche di certificati (CRL, Certificate Revocation List). È necessario incrementare questo numero ogni volta che il CRL viene aggiornato.

**Tabella 5: Opzioni della riga di comando**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_a3y_wqy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> Opzione della riga di comando </th> 
   <th colname="2" class="- topic/entry entry"> Descrizione </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-c file di configurazione</span> </td> 
   <td colname="2" class="- topic/entry "><p class="- topic/p ">Specifica il nome e la posizione del file di configurazione. </p><p class="- topic/p ">Se non si specifica un nome o una posizione, DRM Revocation List Manager cerca <span class="filepath"> flashaccesstools.properties</span> nella directory di lavoro corrente. </p><p>Nota: le opzioni specificate nella riga di comando hanno la precedenza su quelle specificate nel file di configurazione. </p>Specifica la posizione del file di configurazione. Se non si applica questa opzione, il Gestore elenchi di revoche cerca <span class="filepath"> flashaccesstools.properties</span> nella directory di lavoro. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-d nomefile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Visualizza informazioni sull'elenco di revoche. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-e data</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">(Facoltativo) La data di scadenza dell'elenco di revoche. Utilizza uno dei seguenti formati: 
     <ul id="ul_2C89F8183C3647C593CB67576D9DED07"> 
      <li id="li_A866F6CBCB464193A119A6609C8F3B2A"><span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-gg</span> </li> 
      <li id="li_B5F9F6C995E64464838DDE447848F707"><span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-gg-h24:min:sec</span> </li> 
     </ul>Ad esempio, 2009-01-31-14:30:00 rappresenta il 31 gennaio alle 14:30. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-f nomefile[certfile]</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Aggiunge tutte le voci dall'elenco di revoche esistente. È possibile specificare un solo file esistente. </p> <p class="- topic/p ">Se l'elenco esistente è stato firmato con una credenziale diversa da quella utilizzata per firmare il nuovo elenco, è necessario specificare il relativo file di certificato accanto a per verificarne la firma. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Non chiedere se il file di destinazione deve essere sovrascritto. Se il file di destinazione esiste già e <span class="codeph"> -o</span> non è impostato, si verifica un errore. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> Se il file di destinazione esiste già, è possibile sovrascriverlo senza che venga richiesto. </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-r issuerName serialNumber revoationDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Revoca il certificato identificato da <span class="codeph"> issuerName</span> e <span class="codeph"> serialNumber</span> alla data specificata. Il <span class="codeph"> issuerName</span> deve utilizzare il formato nome 509. Ad esempio: <span class="codeph"> CN=12345,O=Adobe Systems Incorporated,C=US</span>. </p> <p>È necessario specificare i numeri seriali in un formato esadecimale. È inoltre necessario specificare la data di revoca in uno dei seguenti formati: 
     <ul id="ul_1524FBC6818248F3A2B271243E649400"> 
      <li id="li_BC618EA2332D42A59B1B5434CAFFD2AF"><span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-gg</span> </li> 
      <li id="li_97F77810D20C4CF2944EFCFF5DFAE467"><span class="+ topic/ph pr-d/codeph codeph">aaaa-mm-gg-h24:min:sec</span> </li> 
     </ul>Ad esempio, 2008-12-1 o 2008-12-1-00:00:00 per mezzanotte del 1 dicembre 2008. Se non si specifica la data di revoca, viene applicata automaticamente la data corrente. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Proprietà di configurazione {#configuration-properties}

Per firmare gli elenchi di revoche è necessario applicare le credenziali. Le seguenti proprietà di Revocation List Manager specificano un file PKCS12 che include le credenziali per la firma degli elenchi di revoche (Certificato server licenze), insieme alla password per il certificato:

* `revocation.sign.certfile=license-server-credentials.pfx`
* `revocation.sign.certpass=password`
