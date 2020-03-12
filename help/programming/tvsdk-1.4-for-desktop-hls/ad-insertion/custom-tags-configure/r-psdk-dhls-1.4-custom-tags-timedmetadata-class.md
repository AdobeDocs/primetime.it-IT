---
description: Quando TVSDK rileva un tag con iscrizione nella playlist o nel manifesto, il lettore tenta automaticamente di elaborare il tag ed esporlo sotto forma di oggetto TimedMetadata.
seo-description: Quando TVSDK rileva un tag con iscrizione nella playlist o nel manifesto, il lettore tenta automaticamente di elaborare il tag ed esporlo sotto forma di oggetto TimedMetadata.
seo-title: Classe di metadati temporizzati
title: Classe di metadati temporizzati
uuid: 827a3bcf-a584-4032-aa19-4fc7730778cc
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Classe di metadati temporizzati{#timed-metadata-class}

Quando TVSDK rileva un tag con iscrizione nella playlist o nel manifesto, il lettore tenta automaticamente di elaborare il tag ed esporlo sotto forma di oggetto TimedMetadata.

La classe fornisce gli elementi seguenti:

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
   <td colname="col1"><span class="codeph"> content</span> </td> 
   <td colname="col02"> Stringa </td> 
   <td colname="col2"> Contenuto non elaborato dei metadati temporizzati. Se il tipo è TAG, il valore rappresenta l'intero elenco di attributi del cue/tag. Se il tipo id ID3, è null. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> id</span> </td> 
   <td colname="col02"> Stringa </td> 
   <td colname="col2"> Identificatore univoco dei metadati temporizzati. Questo valore viene in genere estratto dall’attributo cue/tag ID. In caso contrario, viene fornito un valore casuale univoco. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> metadata</span> </td> 
   <td colname="col02"> Metadati </td> 
   <td colname="col2"> Informazioni elaborate/estratte dal tag personalizzato playlist/manifest. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> name</span> </td> 
   <td colname="col02"> Stringa </td> 
   <td colname="col2">Nome dei metadati temporizzati. Se il tipo è <span class="codeph"> TAG</span>, il valore rappresenta il nome del cue/tag. Se il tipo è <span class="codeph"> ID3</span>, è null. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> time</span> </td> 
   <td colname="col02"> Numero </td> 
   <td colname="col2"> La posizione temporale, in millisecondi, rispetto all'inizio del contenuto principale in cui sono presenti i metadati temporizzati nel flusso. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> type</span> </td> 
   <td colname="col02"> Stringa </td> 
   <td colname="col2">Il tipo di metadati temporizzati. 
    <ul id="ul_70FBFB33E9F846D8B38592560CCE9560"> 
     <li id="li_739D30561BFB4D9B97DF212E4880BA2C">TAG - indica che i metadati temporizzati sono stati creati da un tag nella playlist o nel manifesto. </li> 
     <li id="li_E785E1DEF1CC4D9DBE7764E5D05EFAFC">ID3 - indica che i metadati temporizzati sono stati creati da un tag ID3 nel flusso multimediale. </li> 
    </ul> </td> 
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



* Se l&#39;estrazione non riesce a causa di un formato di tag personalizzato, la proprietà dei metadati sarà vuota e l&#39;applicazione deve estrarre le informazioni effettive. In questo caso non viene generato alcun errore.

| Elemento | Descrizione |
|---|---|
| `TAG, ID3 ID3, TAG` | Tipi possibili per i metadati temporizzati. |
| `public function TimedMetadata(type:String, time:Number, id:String, name:String, content:String, metadata:Metadata)` | Costruttore predefinito (ora è l&#39;ora del flusso locale). |
| `content:String` | Contenuto non elaborato del tag sorgente di questi metadati temporizzati. |
| `time:Number` | La posizione temporale, relativa all&#39;inizio del contenuto principale, in cui tali metadati sono stati inseriti nel flusso. |
| `metadata:Metadata` | I metadati inseriti nel flusso. |
| `type:String` | Restituisce il tipo dei metadati temporizzati. |
| `id:String` | Restituisce l’ID estratto dagli attributi cue/tag. In caso contrario, viene fornito un valore casuale univoco. |
| `name:String` | Restituisce il nome del cue point, che in genere corrisponde al nome del tag HLS. |

