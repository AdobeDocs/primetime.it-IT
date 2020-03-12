---
description: La regola normalizza definisce una trasformazione URL da applicare a un URL creativo sorgente ottenuto da una risposta VAST/VMAP.
keywords: normalize rule;creative selection rules
seo-description: La regola normalizza definisce una trasformazione URL da applicare a un URL creativo sorgente ottenuto da una risposta VAST/VMAP.
seo-title: Normalizza regole
title: Normalizza regole
uuid: 8511000e-3a8a-42f3-b4be-d069d09112b0
translation-type: tm+mt
source-git-commit: 3fdae2b6babb578d2cacff970fd9c7b53ad2c5dc

---


# Normalizza regole {#normalize-rules}

La regola normalizza definisce una trasformazione URL da applicare a un URL creativo sorgente ottenuto da una risposta VAST/VMAP.

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
   <td><span class="codeph"> type</span></td> 
   <td><span class="codeph"> Stringa</span></td> 
   <td><span class="codeph"> normalizzare</span></td> 
   <td>Il valore deve sempre essere <span class="codeph"> normalizzato</span>.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> item</span></td> 
   <td><span class="codeph"> Stringa</span></td> 
   <td><span class="codeph"> host</span></td> 
   <td>Attualmente è supportato solo <span class="codeph"> l'host</span> . Questo attributo deve essere presente quando <span class="codeph"> corrisponde</span> agli attributi <span class="codeph"> e i valori</span> sono definiti.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> matches</span></td> 
   <td></td> 
   <td></td> 
   <td>Valori possibili:
    <ul id="ul_tnf_2hx_hz"> 
     <li><span class="codeph"> eq</span> - è uguale a</li> 
     <li><span class="codeph"> ne</span> - not equals (non uguale a)</li> 
     <li><span class="codeph"> co</span> - contiene</li> 
     <li><span class="codeph"> nc</span> - non contiene</li> 
     <li><span class="codeph"> sw</span> - inizia con</li> 
     <li><span class="codeph"> ew</span> - end con</li> 
    </ul></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> values</span></td> 
   <td><span class="codeph"> Matrice</span></td> 
   <td></td> 
   <td>TVSDK utilizzerà l'attributo <span class="codeph"> matches</span> sull' <span class="codeph"> elemento</span> del creativo di origine e si confronterà con i valori definiti in questa matrice.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> find</span></td> 
   <td><span class="codeph"> regex</span></td> 
   <td></td> 
   <td> Un'espressione regolare da applicare all'URL creativo di origine per la corrispondenza.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> replace</span></td> 
   <td><span class="codeph"> regex</span></td> 
   <td></td> 
   <td> Un'espressione regolare da applicare all'URL creativo di origine da sostituire in base alla corrispondenza.</td> 
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
