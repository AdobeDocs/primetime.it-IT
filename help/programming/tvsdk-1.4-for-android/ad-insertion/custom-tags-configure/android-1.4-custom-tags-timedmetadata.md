---
description: Quando TVSDK rileva un tag sottoscritto nella playlist/manifesto, il lettore tenta automaticamente di elaborare il tag e di esporlo sotto forma di un oggetto TimedMetadata.
title: Classe metadati temporizzati
exl-id: d45e304a-703e-45f4-b3f5-756fc6a614cb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---

# Classe metadati temporizzati{#timed-metadata-class}

Quando TVSDK rileva un tag sottoscritto nella playlist/manifesto, il lettore tenta automaticamente di elaborare il tag e di esporlo sotto forma di un oggetto TimedMetadata.

La classe fornisce i seguenti elementi:

<table id="table_FFC56AC5B1E04DA99C9309C0223ABA90"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Proprietà </th> 
   <th colname="col02" class="entry"> Tipo </th> 
   <th colname="col2" class="entry"> Descrizione </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> id </span> </td> 
   <td colname="col02"> long </td> 
   <td colname="col2"> Identificatore univoco dei metadati temporizzati. Questo valore viene in genere estratto dall’attributo ID del cue/tag. In caso contrario, viene fornito un valore casuale univoco. Utilizzare <span class="codeph"> getId </span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> metadati </span> </td> 
   <td colname="col02"> Metadati </td> 
   <td colname="col2"> Le informazioni elaborate/estratte dal tag personalizzato playlist/manifest. Utilizzare <span class="codeph"> getMetadata </span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> nome </span> </td> 
   <td colname="col02"> Stringa </td> 
   <td colname="col2"> Nome dei metadati temporizzati. Se il tipo è <span class="codeph"> TAG </span>, il valore rappresenta il nome del cue/tag. Se il tipo è <span class="codeph"> ID3 </span>, è nullo. Utilizzare <span class="codeph"> getName </span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> tempo </span> </td> 
   <td colname="col02"> long </td> 
   <td colname="col2"> La posizione temporale, in millisecondi, relativa all’inizio del contenuto principale in cui sono presenti i metadati temporizzati nel flusso. Utilizzare <span class="codeph"> getTime </span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> tipo </span> </td> 
   <td colname="col02"> Tipo </td> 
   <td colname="col2"> Tipo dei metadati temporizzati. Utilizzare <span class="codeph"> getType </span>. 
    <ul id="ul_70FBFB33E9F846D8B38592560CCE9560"> 
     <li id="li_739D30561BFB4D9B97DF212E4880BA2C">TAG: indica che i metadati temporizzati sono stati creati da un tag nella playlist/manifesto. </li> 
     <li id="li_E785E1DEF1CC4D9DBE7764E5D05EFAFC">ID3: indica che i metadati temporizzati sono stati creati da un tag ID3 nel flusso multimediale. </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

<!--<a id="section_737CC47997F74F80A3C5C6171ADE120E"></a>-->

Tenere presente quanto segue:

* TVSDK estrae automaticamente l&#39;elenco degli attributi in coppie chiave-valore e memorizza gli attributi nella proprietà dei metadati.

   >[!TIP]
   >
   >I dati complessi nei tag personalizzati del manifesto, ad esempio le stringhe con caratteri speciali, devono essere racchiusi tra virgolette. Ad esempio:
   >
   >
   ```
   >#EXT-CUSTOM-TAG:type=SpliceOut,ID=1,time=71819.7222,duration=30.0, 
   >url="www.example.com:8090?parameter1=xyz&parameter2=abc"
   >```

* Se l’estrazione non riesce a causa di un formato di tag personalizzato, la proprietà dei metadati sarà vuota e l’applicazione deve estrarre le informazioni effettive. In questo caso non viene generato alcun errore.

| Elemento | Descrizione |
|---|---|
| `public enum Type { TAG, ID3}` | Tipi possibili per i metadati temporizzati. |
| `public TimedMetadata(Type type, long time, long id, String name, Metadata metadata);` | Costruttore predefinito (ora è l’ora del flusso locale). |
| `public long getTime();` | La posizione temporale, relativa all’inizio del contenuto principale, in cui tali metadati sono stati inseriti nel flusso. |
| `public Metadata getMetadata();` | Metadati inseriti nel flusso. |
| `public Type getType();` | Restituisce il tipo dei metadati temporizzati. |
| `public long getId();` | Restituisce l’ID estratto dagli attributi del cue/tag. In caso contrario, viene fornito un valore casuale univoco. |
| `public String getName();` | Restituisce il nome del cue, che in genere corrisponde al nome del tag HLS. |
