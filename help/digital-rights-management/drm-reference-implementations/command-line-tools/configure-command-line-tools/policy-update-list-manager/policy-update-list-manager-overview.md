---
seo-title: Panoramica
title: Panoramica
uuid: 19d05867-c210-4cd0-bc2f-5dd75f5774e5
translation-type: tm+mt
source-git-commit: a33e1f290fcf78e6f131910f6037f4803f7be98d
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 0%

---


# Gestione elenco aggiornamenti criteri DRM {#policy-update-list-manager}

Utilizzate lo strumento della riga di comando Gestione elenchi aggiornamenti criteri DRM di Primetime ( [!DNL AdobePolicyUpdateListManager.jar]) per creare e gestire gli elenchi degli aggiornamenti dei criteri DRM e per verificare se i criteri sono stati aggiornati o revocati.

Prima di eseguire lo strumento della riga di comando Gestione elenchi aggiornamenti criteri, è necessario impostare le proprietà nella sezione *Gestione elenchi aggiornamenti criteri e Proprietà Gestione elenchi revoca* del file di configurazione.

>[!NOTE]
>
>È inoltre possibile specificare tutte le proprietà di Policy Update List Manager dalla riga di comando.

## Utilizzo della riga di comando di Gestione elenchi aggiornamenti criteri {#policy-update-list-manager-command-line-usage}

**Creare un elenco di aggiornamento dei criteri:**

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

**Visualizzare un elenco di aggiornamento criteri esistente:**

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
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c file di configurazione  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Specifica il nome e la posizione del file di configurazione. </p> <p class="- topic/p ">Se non si specifica un nome o una posizione, DRM Policy Update List Manager cerca <span class="filepath"> flashaccesstools.properties </span> nella directory di lavoro corrente. </p> <p>Nota:  Le opzioni specificate nella riga di comando hanno la precedenza rispetto alle opzioni specificate nel file di configurazione. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -d nomefile  </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Visualizza informazioni sull'elenco di aggiornamento dei criteri DRM. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e data  </span> </td> 
   <td colname="2" class="- topic/entry "> <p>(Facoltativo) Data di scadenza dell'elenco di aggiornamento dei criteri DRM. </p> <p>Utilizzare il formato <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> o <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:sec </span> (ad esempio, 2009-01-31-14:30:00 rappresenta il 31 gennaio alle 2:30 PM). </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -f nomefile [certfile]  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Aggiunge tutte le voci dall'elenco di aggiornamento dei criteri DRM esistente. È possibile specificare un solo file esistente. </p> <p class="- topic/p ">Se l'elenco esistente è stato firmato con una credenziale diversa da quella utilizzata per firmare il nuovo elenco, è necessario specificare il relativo file di certificato per verificarne la firma. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -noprompt  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Non chiedere se il file di destinazione deve essere sovrascritto. Se il file di destinazione esiste già e <span class="codeph"> -o </span> non è impostato, si verifica un errore. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Se il file di destinazione esiste già, sovrascrivetelo senza richiedere l'invio di richieste. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r  </span> <span class="+ topic/ph pr-d/codeph codeph"> data policyID  </span> "  <span class="+ topic/ph pr-d/codeph codeph"> reasonCode  </span>" "  <span class="+ topic/ph pr-d/codeph codeph"> reasonText  </span>" "  <span class="+ topic/ph pr-d/codeph codeph"> reasonURL  </span>" </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">(Facoltativo) Revoca l'ID del criterio DRM alla data specificata. Potete fornire un codice del motivo, un testo del motivo e un URL del motivo facoltativi. È necessario specificare una stringa vuota "" per indicare che non viene fornito alcun valore per i parametri facoltativi. È possibile specificare la data in <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> o <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:sec </span> in questi formati. Ad esempio, 2008-12-1 o 2008-12-1-00:00:00 rappresenta la mezzanotte del 1 dicembre 2008). Se non si specifica una data, la data corrente viene applicata automaticamente. Pertanto, il codice motivo deve essere maggiore o uguale a 0. Potete inoltre specificare più opzioni -r. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-rf <span class="+ topic/ph pr-d/codeph codeph"> policyFilename </span> <span class="+ topic/ph pr-d/codeph codeph"> data </span> " <span class="+ topic/ph pr-d/codeph codeph"> reasonCode </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonText </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonURL </span>" </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Esegue la stessa azione dell'opzione <span class="codeph"> -r </span>. Tuttavia, estrae l'identificatore del criterio DRM da un file specificato. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -u policyFilename " reasonCode" " reasonText" " reasonURL"  </span> </td> 
   <td colname="2" class="- topic/entry "> <p>Sostituisce qualsiasi criterio DRM corrispondente in una richiesta di licenza con questo criterio DRM utilizzando il codice del motivo specificato (facoltativo), il testo del motivo (facoltativo) e l'URL del motivo (facoltativo). </p> <p>Una stringa vuota "" indica che non è stato fornito alcun valore per i parametri facoltativi. </p> <p>Il codice del motivo deve essere maggiore o uguale a <span class="codeph"> 0 </span>. Potete specificare più opzioni <span class="codeph"> -u </span>. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Proprietà di configurazione {#configuration-properties}

Le seguenti proprietà di Gestione elenchi aggiornamenti criteri DRM di Primetime specificano un file PKCS12 che include le credenziali per la firma di elenchi di revoche (Certificato server licenze), insieme a una password.

* `revocation.sign.certfile=license-server-credentials.pfx`
* `revocation.sign.certpass=password`