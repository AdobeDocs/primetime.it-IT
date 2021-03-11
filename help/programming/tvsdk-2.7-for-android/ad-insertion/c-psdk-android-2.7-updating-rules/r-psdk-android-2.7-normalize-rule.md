---
description: La regola di normalizzazione definisce una trasformazione URL da applicare a un URL creativo di origine ottenuto da una risposta VAST/VMAP.
keywords: normalizza regola;regole di selezione creativa
title: Normalizzare le regole
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 1%

---


# Normalizzare le regole {#normalize-rules}

La regola di normalizzazione definisce una trasformazione URL da applicare a un URL creativo di origine ottenuto da una risposta VAST/VMAP.

## La regola di normalizzazione ha i seguenti attributi e valori possibili:

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
   <td><span class="codeph"> type</span></td> 
   <td><span class="codeph"> Stringa</span></td> 
   <td><span class="codeph"> normalizzare</span></td> 
   <td>Il valore deve sempre essere <span class="codeph"> normalize</span>.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> item</span></td> 
   <td><span class="codeph"> Stringa</span></td> 
   <td><span class="codeph"> host</span></td> 
   <td>Attualmente è supportato solo <span class="codeph"> host</span>. Questo attributo deve essere presente quando sono definiti gli attributi <span class="codeph"> corrisponde a</span> e <span class="codeph"> valori</span> .</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> matches</span></td> 
   <td></td> 
   <td></td> 
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
   <td><span class="codeph"> values</span></td> 
   <td><span class="codeph"> Array</span></td> 
   <td></td> 
   <td>TVSDK utilizzerà l'attributo <span class="codeph"> corrisponde a</span> sull' <span class="codeph"> elemento</span> del creativo sorgente e corrisponderà ai valori definiti in questo array.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> trova</span></td> 
   <td><span class="codeph"> regex</span></td> 
   <td></td> 
   <td> Un’espressione regolare da applicare all’URL creativo sorgente da abbinare.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> replace</span></td> 
   <td><span class="codeph"> regex</span></td> 
   <td></td> 
   <td> Un’espressione regolare da applicare all’URL creativo sorgente da sostituire in base alla corrispondenza.</td> 
  </tr> 
 </tbody> 
</table>

```
{
    "ads": {
        "rules": {
            "default": [
                {
                ...
                }
                {
                    "
<b>type</b>": "
<b>normalize</b>",
                    "
<b>item</b>": "host",
                    "
<b>matches</b>": "ew",
                    "
<b>values</b>": [
                        "redirector.gvt1.com"
                    ],
                    "
<b>find</b>": "videoplayback/(.*?)/expire/.*?/(.*?)/signature/.*?/",
                    "
<b>replace</b>": "videoplayback/$1/expire//$2/signature//"
                }                
            ]
        }
    }
}
```

