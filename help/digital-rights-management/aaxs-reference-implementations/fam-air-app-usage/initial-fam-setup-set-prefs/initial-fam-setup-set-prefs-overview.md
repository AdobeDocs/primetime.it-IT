---
title: Panoramica sull'impostazione delle preferenze
description: Panoramica sull'impostazione delle preferenze
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# Panoramica sulle preferenze di impostazione {#setting-preferences-overview}

Ad eccezione dell&#39;URL del server Packager, tutte le preferenze specificate di seguito sono memorizzate nel file [!DNL flashaccess-refimpl-packager.properties] sul server. Tutte le impostazioni possono essere modificate direttamente nel file delle proprietà o tramite l’applicazione AIR. Le password vengono crittografate quando vengono memorizzate nel file delle proprietà sul server. Digita la password non crittografata nell’interfaccia utente e verrà crittografata prima di essere memorizzata nel file .

>[!NOTE]
>
>Tutte le directory e i percorsi fanno riferimento alle directory sul server packager, non sul client che esegue l’applicazione AIR.

Tutte le modifiche apportate in questo caso hanno effetto immediatamente dopo il salvataggio delle preferenze. Non è necessario riavviare il server a meno che il thread Packager non sia terminato a causa di problemi di configurazione.

Le descrizioni delle preferenze utilizzano i termini seguenti:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_tj5_hcz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> Preferenza </th> 
   <th colname="2" class="- topic/entry entry"> Descrizione </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> URL del server del pacchetto </td> 
   <td colname="2" class="- topic/entry "> Posizione del server che esegue <span class="filepath"> flashaccess-packager.war </span>; ad esempio, <span class="filepath"> https://localhost:8080 </span> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> Directory risorse </td> 
   <td colname="2" class="- topic/entry "> Directory contenente criteri, certificati, credenziali e qualsiasi altra risorsa necessaria per il server del packager </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> URL server licenze </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">URL del server da cui il cliente deve richiedere una licenza; ad esempio, <span class="filepath"> https://mylicenseserver.com:8080 </span> </p> </td> 
  </tr> 
 </tbody> 
</table>

