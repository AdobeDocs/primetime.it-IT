---
description: Domande frequenti sull'utilizzo della protezione dell'output basata su risoluzione.
seo-description: Domande frequenti sull'utilizzo della protezione dell'output basata su risoluzione.
seo-title: Domande frequenti su RBOP
title: Domande frequenti su RBOP
uuid: 7dcd337c-369a-474c-8768-409c48b5cee5
translation-type: tm+mt
source-git-commit: fa9e89dd63c8b4c9d6eee78258957cfd30c29088
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%

---


# Domande frequenti su RBOP {#rbop-faq}

Domande frequenti sull&#39;utilizzo della protezione dell&#39;output basata su risoluzione.

* **D.** *Quando si definisce un requisito di output digitale per un vincolo di pixel, si verificano errori di analisi/formattazione quando si esce dalla versione HDCP, ma non si hanno requisiti HDCP. Come posso configurare il mio requisito di output digitale in questo caso?* **A.** Poiché al momento il controllo della versione HDCP non è supportato nel client,  Adobe consiglia di impostare la versione HDCP su  `1.0`. Questo garantisce che la configurazione sia formattata correttamente ed è semanticamente coerente in futuro quando sarà supportato il controllo della versione HDCP. Lo snippet di codice seguente illustra una configurazione con questo valore HDCP.

   ```
   { "pixelConstraints":  
     [  
       { "pixelCount": 720, "digital":  
         [  
           {  
             "output": "REQUIRED", "hdcp": {"major": 1, "minor": 0}  
           }  
         ]  
       }  
     ]  
   }
   ```

* **D.** *I vincoli di pixel RBOP sono discreti o basati su intervalli?* **I vincoli di pixel A.** RBOP sono basati su intervalli. Ogni conteggio di pixel definisce i requisiti per tutti i conteggi di pixel inferiori o uguali al conteggio specificato o fino al conteggio più grande inferiore a tale valore, se esistono più vincoli di pixel. In altre parole, i valori vengono applicati come soglie massime per ciascun conteggio pixel verticale.

   Supponiamo che un flusso MBR con risoluzioni verticali di 240, 480, 600, 720 e 1080 venga trasmesso al lettore con le seguenti impostazioni RBOP.

   **Impostazioni criteri RBOP:**

   * 720P - HDCP richiesto
   * 480P - No OP

   A ciascuna variante saranno applicate le seguenti regole.

   **Flussi:**

   * 240, 480: Sono &lt;= 480; non è richiesto nessun OP e i flussi si caricano con o senza HDCP.
   * 600, 720: Entrambe sono &lt;= 720; HDCP è richiesto per la riproduzione
   * 1080: > 720; il flusso è elencato come blocco (restituito dall&#39;errore) in quanto non è presente nelle regole sopra riportate.


* **D.** Su alcuni dispositivi Android, le limitazioni del numero di pixel definite non vengono applicate esattamente come definite. Cosa sta succedendo?

   **A.** Alcuni dispositivi Android riportano dimensioni dei fotogrammi leggermente superiori a quelle normali. Per ovviare a questa situazione, regolare le dimensioni dei fotogrammi ( `maxPixel` e `pixelCount` impostazioni) verso l&#39;alto di 20 pixel. Ad esempio, regolate le impostazioni delle dimensioni del fotogramma verso l’alto, da:

   ```
   { 
       "maxPixel": 800, 
       "pixelConstraints": [ 
           { "pixelCount": 532, 
             "digital": [{"output": "REQUIRED", "hdcp":{"major": 1,"minor": 0}}], 
             "analog": {"output": "REQUIRED"} 
           }, 
   ... 
   ```

   a:

   ```
   { 
       "maxPixel": 820, 
       "pixelConstraints": [ 
           { "pixelCount": 552, 
             "digital": [{"output": "REQUIRED", "hdcp":{"major": 1,"minor": 0}}], 
             "analog": {"output": "REQUIRED"} 
           }, 
   ... 
   ```

   in tutte le istanze di `maxPixel` e `pixelCount`.

