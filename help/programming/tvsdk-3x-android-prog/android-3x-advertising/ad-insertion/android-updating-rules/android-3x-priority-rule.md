---
description: La regola di priorità definisce l'ordine di priorità delle creatività degli annunci che verranno selezionate per la riproduzione da una risposta VAST/VMAP.
keywords: priority rule;creative selection rules
seo-description: La regola di priorità definisce l'ordine di priorità delle creatività degli annunci che verranno selezionate per la riproduzione da una risposta VAST/VMAP.
seo-title: Regole di priorità
title: Regole di priorità
uuid: 20dd0ded-06dd-427d-8dd3-79f9f8a3390c
translation-type: tm+mt
source-git-commit: 3fdae2b6babb578d2cacff970fd9c7b53ad2c5dc
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 1%

---


# Regole di priorità {#priority-rules}

La regola di priorità definisce l&#39;ordine di priorità delle creatività degli annunci che verranno selezionate per la riproduzione da una risposta VAST/VMAP.

<table id="table_ljp_tgx_hz">  
 <thead> 
  <tr> 
   <th class="entry"><b>Key</b></th> 
   <th class="entry"><b>Tipo</b></th> 
   <th class="entry"><b>Valori</b></th> 
   <th class="entry"><b>Descrizione</b></th>
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> priority</span></td> 
   <td><span class="codeph"> Matrice</span></td> 
   <td></td> 
   <td> Un array di tipi mime minuscoli che definiscono la priorità in cui devono essere selezionate le creatività sorgente per la riproduzione.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> item</span></td> 
   <td><span class="codeph"> Stringa</span></td> 
   <td><span class="codeph"> host</span></td> 
   <td>Attualmente è supportato solo <span class="codeph"> host</span>. Questo attributo deve essere presente quando gli attributi <span class="codeph"> corrispondono agli attributi </span> e <span class="codeph"> ai valori</span> sono definiti.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> matches</span></td> 
   <td><span class="codeph"> Stringa</span></td> 
   <td><span class="codeph"> multiple</span></td> 
   <td>Valori possibili:
    <ul id="ul_tnf_2hx_hz"> 
     <li><span class="codeph"> eq</span> - equals</li> 
     <li><span class="codeph"> ne</span> - not equals (non uguale a)</li> 
     <li><span class="codeph"> co</span> -contiene</li> 
     <li><span class="codeph"> nc</span> - not contains</li> 
     <li><span class="codeph"> sw</span>  - inizia con</li> 
     <li><span class="codeph"> ew</span> -end con</li> 
    </ul></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> type</span></td> 
   <td><span class="codeph"> Stringa</span></td> 
   <td><span class="codeph"> priority</span></td> 
   <td>Il valore deve sempre essere <span class="codeph"> priority</span></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> values</span></td> 
   <td><span class="codeph"> Matrice</span></td> 
   <td></td> 
   <td> <p>TVSDK utilizzerà l'attributo <span class="codeph"> corrisponde</span> sull'elemento <span class="codeph"></span> del creativo di origine e si confronta con i valori definiti in questa matrice</p> </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> stream</span></td> 
   <td><span class="codeph"> Stringa</span></td> 
   <td></td> 
   <td> <p>Il valore può essere <span class="codeph"> vod</span> o <span class="codeph"> live</span></p> </td> 
  </tr> 
 </tbody> 
</table>

```
{
    "ads": {
        "rules": {
            "default": [
                {
                    "
<b>type</b>": "
<b>priority</b>",
                    "
<b>stream</b>": "vod",
                    "
<b>priority</b>": [
                        "application/x-mpegurl",
                        "application/vnd.apple.mpegurl",
                        "application/x-shockwave-flash",
                        "video/mp4",
                        "video/m4v",
                        "video/x-flv",
                        "video/webm"
                    ]
                },
                {
                    ...
                },
            ]
        }
    }
}
```
