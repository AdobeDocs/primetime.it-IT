---
description: Domande frequenti sull'utilizzo della protezione dell'output basata su risoluzione.
seo-description: Domande frequenti sull'utilizzo della protezione dell'output basata su risoluzione.
seo-title: Domande frequenti su RBOP
title: Domande frequenti su RBOP
uuid: 7dcd337c-369a-474c-8768-409c48b5cee5
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---


# Domande frequenti su RBOP {#rbop-faq}

Domande frequenti sull&#39;utilizzo della protezione dell&#39;output basata su risoluzione.

* **D.** *Quando si definisce un requisito di output digitale per un vincolo di pixel, si verificano errori di analisi/formattazione quando si esce dalla versione HDCP, ma non sono presenti requisiti HDCP. Come posso configurare il mio requisito di output digitale in questo caso?* **A.** Poiché al momento il controllo della versione HDCP non è supportato nel client, Adobe consiglia di impostare la versione HDCP su `1.0`. Questo garantisce che la configurazione sia formattata correttamente ed è semanticamente coerente in futuro quando sarà supportato il controllo della versione HDCP. Lo snippet di codice seguente illustra una configurazione con questo valore HDCP.

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

* **D.** *I vincoli di pixel RBOP sono discreti o basati su intervalli?* **A.** I vincoli di pixel RBOP sono basati su intervalli. Ogni conteggio di pixel definisce i requisiti per tutti i conteggi di pixel inferiori o uguali al conteggio specificato o fino al conteggio più grande inferiore a tale valore, se esistono più vincoli di pixel. In altre parole, i valori vengono applicati come soglie massime per ciascun conteggio pixel verticale.

   Supponiamo che un flusso MBR con risoluzioni verticali di 240, 480, 600, 720 e 1080 venga trasmesso al lettore con le seguenti impostazioni RBOP.

   **Impostazioni criteri RBOP:**

   * 720P - HDCP richiesto
   * 480P - No OP
   A ciascuna variante saranno applicate le seguenti regole.

   **Flussi:**

   * 240, 480: Sono &lt;= 480; non è richiesto nessun OP e i flussi si caricano con o senza HDCP.
   * 600, 720: Entrambe sono &lt;= 720; HDCP è richiesto per la riproduzione
   * 1080: > 720; il flusso è elencato come blocco (restituito dall&#39;errore) in quanto non è presente nelle regole sopra riportate.


* **D.** Su alcuni dispositivi Android, le limitazioni del numero di pixel definite non vengono applicate esattamente come sono definite. Cosa sta succedendo?

   **A.** Alcuni dispositivi Android riportano dimensioni dei fotogrammi leggermente superiori a quelle normali. Per ovviare a questa situazione, regolate le dimensioni dei fotogrammi ( `maxPixel` e `pixelCount` le impostazioni) verso l’alto di 20 pixel. Ad esempio, regolate le impostazioni delle dimensioni del fotogramma verso l’alto, da:

   ```
   { 
       "maxPixel":  
   
<b>800</b>,&quot;pixelConstraints&quot;: [{ &quot;pixelCount&quot;:\
<b>532</b>,&quot;digitale&quot;: [{&quot;output&quot;: &quot;REQUIRED&quot;, &quot;hdcp&quot;:{&quot;major&quot;: 1, &quot;minore&quot;: 0}}],&quot;analogico&quot;: {&quot;output&quot;: &quot;OBBLIGATORIO&quot;},..

```
to: 
```
{&quot;maxPixel&quot;:\
<b>820</b>,&quot;pixelConstraints&quot;: [{ &quot;pixelCount&quot;:\
<b>552</b>,&quot;digitale&quot;: [{&quot;output&quot;: &quot;REQUIRED&quot;, &quot;hdcp&quot;:{&quot;major&quot;: 1, &quot;minore&quot;: 0}}],&quot;analogico&quot;: {&quot;output&quot;: &quot;OBBLIGATORIO&quot;},..

```
throughout, for all instances of `maxPixel` and `pixelCount`.

