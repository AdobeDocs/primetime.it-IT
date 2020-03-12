---
description: Quando TVSDK rileva un tag con iscrizione nella playlist o nel manifesto, il lettore tenta automaticamente di elaborare ed esporre il tag sotto forma di un oggetto TimedMetadata.
seo-description: Quando TVSDK rileva un tag con iscrizione nella playlist o nel manifesto, il lettore tenta automaticamente di elaborare ed esporre il tag sotto forma di un oggetto TimedMetadata.
seo-title: Classe di metadati temporizzati
title: Classe di metadati temporizzati
uuid: c7b1c1d7-48b3-43c7-aa21-f800d894976d
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Classe di metadati temporizzati {#timed-metadata-class}

Quando TVSDK rileva un tag con iscrizione nella playlist o nel manifesto, il lettore tenta automaticamente di elaborare ed esporre il tag sotto forma di un oggetto TimedMetadata.

La classe fornisce gli elementi seguenti:

<table id="table_FFC56AC5B1E04DA99C9309C0223ABA90"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b> Proprietà </b></th> 
   <th colname="col02" class="entry"> <b> Tipo </b></th> 
   <th colname="col2" class="entry"> <b> Descrizione </b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> id </span> </td> 
   <td colname="col02"> long </td> 
   <td colname="col2"> <p>Identificatore univoco dei metadati temporizzati. </p> <p>Questo valore viene in genere estratto dall’attributo cue/tag ID. In caso contrario, viene fornito un valore casuale univoco. Utilizzate <span class="codeph"> getId </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> metadata </span> </td> 
   <td colname="col02"> Metadati </td> 
   <td colname="col2"> <p>Informazioni elaborate/estratte dal tag personalizzato playlist/manifest. Utilizzate <span class="codeph"> getMetadata </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> name </span> </td> 
   <td colname="col02"> Stringa </td> 
   <td colname="col2"> <p>Nome dei metadati temporizzati. Se il tipo è <span class="codeph"> TAG </span>, il valore rappresenta il nome del cue/tag. Se il tipo è <span class="codeph"> ID3 </span>, è null. Utilizzate <span class="codeph"> getName </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> time </span> </td> 
   <td colname="col02"> long </td> 
   <td colname="col2"> <p>La posizione temporale, in millisecondi, rispetto all'inizio del contenuto principale in cui sono presenti i metadati temporizzati nel flusso. Usa <span class="codeph"> getTime </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> type </span> </td> 
   <td colname="col02"> Tipo </td> 
   <td colname="col2"> <p>Il tipo di metadati temporizzati. Usa <span class="codeph"> getType </span>. 
     <ul id="ul_70FBFB33E9F846D8B38592560CCE9560"> 
      <li id="li_739D30561BFB4D9B97DF212E4880BA2C">TAG - indica che i metadati temporizzati sono stati creati da un tag nella playlist o nel manifesto. </li> 
      <li id="li_E785E1DEF1CC4D9DBE7764E5D05EFAFC">ID3 - indica che i metadati temporizzati sono stati creati da un tag ID3 nel flusso multimediale. </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

<!--<a id="section_737CC47997F74F80A3C5C6171ADE120E"></a>-->

Ricorda quanto segue:

* TVSDK estrae automaticamente l&#39;elenco degli attributi in coppie chiave-valore e memorizza gli attributi nella proprietà metadata.

   >[!TIP]
   >
   >I dati complessi nei tag personalizzati nel manifesto, come le stringhe con caratteri speciali, devono essere racchiusi tra virgolette. Ad esempio:   >
   >
   >
   ```>
   >#EXT-CUSTOM-TAG:type=SpliceOut,ID=1,time=71819.7222,duration=30.0,url= 
   >"www.example.com:8090?parameter1=xyz&parameter2=abc"
   >```  >
   >



* Se l&#39;estrazione non riesce a causa di un formato di tag personalizzato, la proprietà dei metadati sarà vuota e l&#39;applicazione deve estrarre le informazioni effettive. In questo caso, non viene generato alcun errore.

<table id="table_1BAE98BF23F641A3A5709EBE37B327F6"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> <b>Elemento </b></th> 
   <th colname="col2" class="entry"> <b>Descrizione</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public enum Type {TAG, ID3} </span> </td> 
   <td colname="col2"> <p>Tipi possibili per i metadati temporizzati. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public TimedMetadata(tipo, long time, long id, String name, Metadata); </span> </td> 
   <td colname="col2"> <p>Costruttore predefinito (ora è l'ora del flusso locale). </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public long getTime(); </span> </td> 
   <td colname="col2"> <p>La posizione temporale, relativa all'inizio del contenuto principale, in cui tali metadati sono stati inseriti nel flusso. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public Metadata getMetadata(); </span> </td> 
   <td colname="col2"> <p>I metadati inseriti nel flusso. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public Type getType(); </span> </td> 
   <td colname="col2"> <p>Restituisce il tipo dei metadati temporizzati. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public long getId(); </span> </td> 
   <td colname="col2"> <p>Restituisce l’ID estratto dagli attributi cue/tag. In caso contrario, viene fornito un valore casuale univoco. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public String getName(); </span> </td> 
   <td colname="col2"> <p>Restituisce il nome del cue point, che in genere corrisponde al nome del tag HLS. </p> </td> 
  </tr> 
 </tbody> 
</table>