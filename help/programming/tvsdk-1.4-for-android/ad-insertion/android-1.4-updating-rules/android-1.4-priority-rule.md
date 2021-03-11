---
description: La regola di priorità definisce l'ordine di priorità delle creatività degli annunci che verranno selezionate per la riproduzione da una risposta VAST/VMAP.
keywords: regola di priorità;regole di selezione creativa
title: Regole di priorità
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 1%

---


# Regole di priorità{#priority-rules}

La regola di priorità definisce l&#39;ordine di priorità delle creatività degli annunci che verranno selezionate per la riproduzione da una risposta VAST/VMAP.

**Tabella 1: Una regola di priorità ha i seguenti attributi e valori possibili:**

<table id="table_ljp_tgx_hz">  
 <thead> 
  <tr> 
   <th class="entry"> Chiave</th> 
   <th class="entry"> Tipo</th> 
   <th class="entry"> Valori</th> 
   <th class="entry"> Descrizione</th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> priorità</span></td> 
   <td><span class="codeph"> Array</span></td> 
   <td></td> 
   <td> Matrice di tipi di mime in minuscolo che definiscono la priorità in cui devono essere selezionate le creazioni di origine per la riproduzione.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> item</span></td> 
   <td><span class="codeph"> Stringa</span></td> 
   <td><span class="codeph"> host</span></td> 
   <td>Attualmente è supportato solo <span class="codeph"> host</span>. Questo attributo deve essere presente quando sono definiti gli attributi <span class="codeph"> corrisponde a</span> e <span class="codeph"> valori</span> .</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> matches</span></td> 
   <td><span class="codeph"> Stringa</span></td> 
   <td><span class="codeph"> multiplo</span></td> 
   <td>Valori possibili:
    <ul id="ul_tnf_2hx_hz"> 
     <li><span class="codeph"> eq</span>  - è uguale a</li> 
     <li><span class="codeph"> ne</span>  - not equals</li> 
     <li><span class="codeph"> co</span>  - contiene</li> 
     <li><span class="codeph"> nc</span>  - non contiene</li> 
     <li><span class="codeph"> sw</span>  - inizia con</li> 
     <li><span class="codeph"> </span>  - termina con</li> 
    </ul></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> type</span></td> 
   <td><span class="codeph"> Stringa</span></td> 
   <td><span class="codeph"> priorità</span></td> 
   <td>Il valore deve sempre essere <span class="codeph"> priority</span></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> values</span></td> 
   <td><span class="codeph"> Array</span></td> 
   <td></td> 
   <td> <p>TVSDK utilizzerà l'attributo <span class="codeph"> corrisponde</span> sull' <span class="codeph"> elemento</span> del creativo sorgente e corrisponde ai valori definiti in questo array</p> </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> flusso</span></td> 
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

