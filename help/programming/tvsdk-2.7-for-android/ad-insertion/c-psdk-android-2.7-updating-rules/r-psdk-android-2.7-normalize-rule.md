---
description: La regola di normalizzazione definisce una trasformazione URL da applicare a un URL creativo di origine ottenuto da una risposta VAST/VMAP.
keywords: normalizza regola;regole di selezione creativa
title: Normalizza regole
exl-id: 28f315fe-b665-4abb-9b28-0182e999a8b2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# Normalizza regole {#normalize-rules}

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
   <td><span class="codeph"> tipo</span></td> 
   <td><span class="codeph"> Stringa</span></td> 
   <td><span class="codeph"> normalizzare</span></td> 
   <td>Il valore deve essere sempre <span class="codeph"> normalizzare</span>.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> elemento</span></td> 
   <td><span class="codeph"> Stringa</span></td> 
   <td><span class="codeph"> host</span></td> 
   <td>Attualmente solo <span class="codeph"> host</span> è supportato. Questo attributo deve essere presente quando <span class="codeph"> corrisponde a</span> e <span class="codeph"> valori</span> attributi definiti.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> corrisponde a</span></td> 
   <td></td> 
   <td></td> 
   <td>Valori possibili:
    <ul id="ul_tnf_2hx_hz"> 
     <li><span class="codeph"> eq</span> - è uguale a</li> 
     <li><span class="codeph"> ne</span> - non è uguale a</li> 
     <li><span class="codeph"> co</span> - contiene</li> 
     <li><span class="codeph"> nc</span> - non contiene</li> 
     <li><span class="codeph"> sw</span> - inizia con</li> 
     <li><span class="codeph"> ew</span> - termina con</li> 
    </ul></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> valori</span></td> 
   <td><span class="codeph"> Array</span></td> 
   <td></td> 
   <td>TVSDK utilizzerà <span class="codeph"> corrisponde a</span> attributo su <span class="codeph"> elemento</span> della creatività sorgente e confrontarla con i valori definiti in questo array.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> trova</span></td> 
   <td><span class="codeph"> regex</span></td> 
   <td></td> 
   <td> Espressione regolare da applicare all’URL creativo di origine da rilevare.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> replace</span></td> 
   <td><span class="codeph"> regex</span></td> 
   <td></td> 
   <td> Espressione regolare da applicare all’URL creativo di origine da sostituire in base alla corrispondenza.</td> 
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
