---
seo-title: Panoramica delle preferenze
title: Panoramica delle preferenze
uuid: d1c067b1-6c2b-460e-8d00-5a5bfee0789c
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# Panoramica delle preferenze {#setting-preferences-overview}

Ad eccezione dell&#39;URL di Packager Server, tutte le preferenze specificate di seguito vengono memorizzate nel [!DNL flashaccess-refimpl-packager.properties] file sul server. Tutte le impostazioni possono essere modificate direttamente nel file delle proprietà o tramite l&#39;applicazione AIR. Le password vengono crittografate quando vengono memorizzate nel file delle proprietà sul server. Digita la password non crittografata nell&#39;interfaccia utente e verrà crittografata prima di essere memorizzata nel file.

>[!NOTE]
>
>Tutte le directory e i percorsi fanno riferimento alle directory sul server packager, non sul client che esegue l&#39;applicazione AIR.

Eventuali modifiche apportate in questo caso avranno effetto immediatamente dopo il salvataggio delle preferenze. Non è necessario riavviare il server a meno che il thread di Packager non sia terminato a causa di problemi di configurazione.

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
   <td colname="1" class="- topic/entry "> URL del server Packager </td> 
   <td colname="2" class="- topic/entry "> Posizione del server in cui è in esecuzione <span class="filepath"> flashaccess-packager.war </span>; ad esempio <span class="filepath"> https://localhost:8080 </span> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> Directory risorse </td> 
   <td colname="2" class="- topic/entry "> Directory contenente criteri, certificati, credenziali e qualsiasi altra risorsa necessaria per il server packager </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> URL server licenze </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">URL del server dal quale il cliente deve richiedere una licenza; ad esempio <span class="filepath"> https://mylicenseserver.com:8080 </span> </p> </td> 
  </tr> 
 </tbody> 
</table>

