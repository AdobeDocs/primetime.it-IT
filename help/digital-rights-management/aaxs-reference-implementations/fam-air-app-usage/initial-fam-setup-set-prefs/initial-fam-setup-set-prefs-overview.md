---
title: Panoramica sull’impostazione delle preferenze
description: Panoramica sull’impostazione delle preferenze
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---

# Panoramica sull’impostazione delle preferenze {#setting-preferences-overview}

Ad eccezione dell’URL del server Packager, tutte le preferenze specificate di seguito sono memorizzate in [!DNL flashaccess-refimpl-packager.properties] sul server. Tutte le impostazioni possono essere modificate direttamente nel file delle proprietà o tramite l’applicazione AIR. Le password vengono crittografate quando vengono memorizzate nel file delle proprietà sul server. Digita la password non crittografata nell’interfaccia utente e verrà crittografata prima che venga memorizzata nel file.

>[!NOTE]
>
>Tutte le directory e i percorsi si riferiscono alle directory sul server Packager, non sul client che esegue l&#39;applicazione AIR.

Tutte le modifiche apportate qui hanno effetto immediato dopo il salvataggio delle preferenze. Non è necessario riavviare il server a meno che il thread Packager non venga terminato a causa di problemi di configurazione.

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
   <td colname="1" class="- topic/entry "> URL server Packager </td> 
   <td colname="2" class="- topic/entry "> Percorso del server in esecuzione <span class="filepath"> flashaccess-packager.war </span>ad esempio, <span class="filepath"> https://localhost:8080 </span> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> Directory risorse </td> 
   <td colname="2" class="- topic/entry "> Directory contenente criteri, certificati, credenziali e qualsiasi altra risorsa necessaria per il server Packager </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> URL server licenze </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">URL del server da cui il client deve richiedere una licenza; ad esempio, <span class="filepath"> https://mylicenseserver.com:8080 </span> </p> </td> 
  </tr> 
 </tbody> 
</table>
