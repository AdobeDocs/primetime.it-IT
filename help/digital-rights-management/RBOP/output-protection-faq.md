---
description: Domande frequenti sull'utilizzo della protezione dell'output basata sulla risoluzione.
title: Domande frequenti su RBOP
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---


# Domande frequenti su RBOP {#rbop-faq}

Domande frequenti sull&#39;utilizzo della protezione dell&#39;output basata sulla risoluzione.

* **D.** *Quando definisco un requisito di output digitale per un vincolo di pixel, ricevo errori di analisi/formattazione quando lascio fuori la versione HDCP, ma non ho requisiti HDCP. Come posso configurare il mio requisito di output digitale in questo caso?* **A.** Poiché attualmente il controllo della versione HDCP non è supportato nel client, Adobe consiglia di impostare la versione HDCP su  `1.0`. Questo assicurerà che la configurazione sia formattata correttamente ed è semanticamente coerente in futuro quando sarà supportato il controllo della versione HDCP. Il frammento seguente illustra una configurazione con questo valore HDCP.

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

* **D.** *I vincoli di pixel RBOP sono discreti o basati su intervalli?* **I vincoli di pixel A.** RBOP sono suddivisi in base a. Ogni conteggio di pixel definisce i requisiti per tutti i conteggi di pixel inferiori o uguali al conteggio specificato o fino al conteggio più grande minore di quel valore se esistono più vincoli di pixel. In parole povere, i valori si applicano come soglie massime per ogni conteggio pixel verticale.

   Supponiamo che un flusso MBR con risoluzioni verticali di 240, 480, 600, 720 e 1080 venga trasmesso al lettore con le seguenti impostazioni RBOP.

   **Impostazioni dei criteri RBOP:**

   * 720P - HDCP richiesto
   * 480P - No OP

   A ogni variante verranno applicate le seguenti regole.

   **Flussi:**

   * 240, 480: sono &lt;= 480; non è richiesto nessun OP e i flussi si caricano con o senza HDCP presente.
   * 600, 720: sono &lt;= 720; HDCP è richiesto per la riproduzione
   * 1080: > 720; il flusso è inserito nell’elenco dei blocchi (restituito l’errore) in quanto non è trovato nelle regole di cui sopra.


* **D.** Su alcuni dei miei dispositivi Android, le restrizioni di conteggio dei pixel che ho definito non vengono applicate esattamente come definite. Cosa sta succedendo?

   **A.** Alcuni dispositivi Android registrano dimensioni dei fotogrammi leggermente superiori a quelle normali. Per ovviare a questa situazione, regola le dimensioni dei fotogrammi ( `maxPixel` e `pixelCount` impostazioni) verso l&#39;alto di 20 pixel. Ad esempio, regola le impostazioni delle dimensioni del fotogramma verso l&#39;alto, da:

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

   in tutto, per tutte le istanze di `maxPixel` e `pixelCount`.

