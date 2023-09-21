---
description: La regola di priorità definisce l’ordine di priorità delle creatività dell’annuncio che verranno selezionate per la riproduzione da una risposta VAST/VMAP.
keywords: regola di priorità;regole di selezione creativa
title: Regole di priorità
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# Regole di priorità {#priority-rules}

La regola di priorità definisce l’ordine di priorità delle creatività dell’annuncio che verranno selezionate per la riproduzione da una risposta VAST/VMAP.

## Una regola Priority dispone dei seguenti attributi e valori possibili:

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
   <td> Array di tipi mime minuscoli che definiscono la priorità con cui selezionare le creatività sorgente da riprodurre.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> elemento</span></td> 
   <td><span class="codeph"> Stringa</span></td> 
   <td><span class="codeph"> host</span></td> 
   <td>Attualmente solo <span class="codeph"> host</span> è supportato. Questo attributo deve essere presente quando <span class="codeph"> corrisponde a</span> e <span class="codeph"> valori</span> attributi definiti.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> corrisponde a</span></td> 
   <td><span class="codeph"> Stringa</span></td> 
   <td><span class="codeph"> multiplo</span></td> 
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
   <td><span class="codeph"> tipo</span></td> 
   <td><span class="codeph"> Stringa</span></td> 
   <td><span class="codeph"> priorità</span></td> 
   <td>Il valore deve essere sempre <span class="codeph"> priorità</span></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> valori</span></td> 
   <td><span class="codeph"> Array</span></td> 
   <td></td> 
   <td> <p>TVSDK utilizzerà <span class="codeph"> corrisponde a</span> attributo su <span class="codeph"> elemento</span> della creatività sorgente e confrontarla con i valori definiti in questo array</p> </td> 
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
