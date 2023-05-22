---
title: Panoramica
description: Panoramica
copied-description: true
exl-id: 1e06bead-4b45-4bf0-8bcf-1ea376af6bd8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---

# Gestione elenco aggiornamenti criteri DRM {#policy-update-list-manager}

Utilizzare lo strumento da riga di comando Gestione elenchi aggiornamento criteri DRM di Primetime ( [!DNL AdobePolicyUpdateListManager.jar]) per creare e gestire gli elenchi di aggiornamento dei criteri DRM e per verificare se i criteri sono stati aggiornati o revocati.

Prima di eseguire lo strumento da riga di comando Gestione elenco aggiornamenti criteri, è necessario impostare le proprietà in *Proprietà di Gestione elenchi aggiornamento criteri e Gestione elenchi di revoche* del file di configurazione.

>[!NOTE]
>
>È inoltre possibile specificare tutte le proprietà di Gestione elenco aggiornamento criteri dalla riga di comando.

## Utilizzo della riga di comando di Gestione elenchi aggiornamento criteri {#policy-update-list-manager-command-line-usage}

**Creare un elenco di aggiornamenti dei criteri:**

```
java -jar AdobePolicyUpdateListManager.jar  
<i class="+ topic ph hi-d="" i "="">
  destfile [ 
 <i class="+ topic ph hi-d="" i "="">
   options]  
 </i class="+ topic> 
</i class="+ topic>
```

* `destfile` indica il nome del file in cui è scritto l&#39;elenco di aggiornamento dei criteri DRM.

**Visualizzare un elenco di aggiornamenti dei criteri esistente:**

```
java -jar AdobePolicyUpdateListManager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  filename 
</i class="+ topic>
```

* `filename` Nome del file dell&#39;elenco di aggiornamento dei criteri.

**Tabella 4: Opzioni della riga di comando**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_ghb_jqy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Opzione della riga di comando </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descrizione </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c file di configurazione </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica il nome e la posizione del file di configurazione. </p> <p class="- topic/p ">Se non si specifica un nome o una posizione, DRM Policy Update List Manager cerca <span class="filepath"> flashaccesstools.properties </span> nella directory di lavoro corrente. </p> <p>Nota: le opzioni specificate nella riga di comando hanno la precedenza su quelle specificate nel file di configurazione. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -d nomefile </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Visualizza informazioni sull'elenco di aggiornamento dei criteri DRM. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e data </span> </td> 
   <td colname="2" class="- topic/entry "> <p>(Facoltativo) Data di scadenza dell'elenco di aggiornamento dei criteri DRM. </p> <p>Utilizza il formato <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-gg </span> o <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-gg-h24:min:sec </span> (ad esempio, 2009-01-31-14:30:00 rappresenta il 31 gennaio alle 14:30). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -f nomefile [certfile] </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Aggiunge tutte le voci dell'elenco di aggiornamento dei criteri DRM esistente. È possibile specificare un solo file esistente. </p> <p class="- topic/p ">Se l'elenco esistente è stato firmato con una credenziale diversa da quella utilizzata per firmare il nuovo elenco, è necessario specificare il relativo file di certificato per verificarne la firma. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Non chiedere se il file di destinazione deve essere sovrascritto. Se il file di destinazione esiste già e <span class="codeph"> -o </span> non è impostato, si verifica un errore. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se il file di destinazione esiste già, sovrascriverlo senza chiedere conferma. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r policyID </span> <span class="+ topic/ph pr-d/codeph codeph"> data </span> " <span class="+ topic/ph pr-d/codeph codeph"> reasonCode </span>"" <span class="+ topic/ph pr-d/codeph codeph"> reasonText </span>"" <span class="+ topic/ph pr-d/codeph codeph"> reasonURL </span>" </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">(Facoltativo) Revoca l'ID del criterio DRM alla data specificata. È possibile fornire un codice motivo facoltativo, un testo del motivo e un URL del motivo. È necessario specificare una stringa vuota "" per indicare che non viene fornito alcun valore per i parametri facoltativi. È possibile specificare la data in <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-gg </span> o <span class="+ topic/ph pr-d/codeph codeph"> aaaa-mm-gg-h24:min:sec </span> in questi formati. Ad esempio, 2008-12-1 o 2008-12-1-00:00:00 rappresenta la mezzanotte del 1º dicembre 2008). Se non si specifica una data, la data corrente viene applicata automaticamente. Pertanto, il codice motivo deve essere maggiore o uguale a 0. È inoltre possibile specificare più opzioni -r. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-rf <span class="+ topic/ph pr-d/codeph codeph"> policyFilename </span> <span class="+ topic/ph pr-d/codeph codeph"> data </span> " <span class="+ topic/ph pr-d/codeph codeph"> reasonCode </span>"" <span class="+ topic/ph pr-d/codeph codeph"> reasonText </span>"" <span class="+ topic/ph pr-d/codeph codeph"> reasonURL </span>" </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Esegue la stessa azione del <span class="codeph"> -r </span> opzione. Tuttavia, estrae l'identificatore della policy DRM da un file specificato. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -u policyFilename " reasonCode" " reasonText" " reasonURL" </span> </td> 
   <td colname="2" class="- topic/entry "> <p>Sostituisce qualsiasi criterio DRM corrispondente in una richiesta di licenza con questo criterio DRM utilizzando il codice motivo specificato (facoltativo), il testo del motivo (facoltativo) e l'URL del motivo (facoltativo). </p> <p>Una stringa vuota "" indica che non hai fornito alcun valore per i parametri facoltativi. </p> <p>Il codice motivo deve essere maggiore o uguale a <span class="codeph"> 0 </span>. È possibile specificare più <span class="codeph"> -u </span> opzioni. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Proprietà di configurazione {#configuration-properties}

Nelle seguenti proprietà di Gestione elenchi aggiornamento criteri DRM di Primetime è specificato un file PKCS12 che include le credenziali per la firma degli elenchi di revoche (certificato del server di licenze) e una password.

* `revocation.sign.certfile=license-server-credentials.pfx`
* `revocation.sign.certpass=password`
