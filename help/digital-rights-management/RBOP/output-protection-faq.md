---
description: Domande frequenti sull'utilizzo della protezione dell'output basata sulla risoluzione.
title: DOMANDE FREQUENTI SU RBOP
exl-id: 16b95db4-43a9-4458-b7f4-94033a36542e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# DOMANDE FREQUENTI SU RBOP {#rbop-faq}

Domande frequenti sull&#39;utilizzo della protezione dell&#39;output basata sulla risoluzione.

* **D.** *Quando si definisce un requisito di uscita digitale per un vincolo di pixel, si verificano errori di analisi/formattazione quando si esce dalla versione HDCP, ma non è necessario alcun requisito HDCP. Come si configura il fabbisogno di output digitale in questo caso?* **R.** Poiché il controllo della versione HDCP non è attualmente supportato dal client, l’Adobe consiglia di impostare la versione HDCP su `1.0`. In questo modo la configurazione sarà formattata correttamente e sarà semanticamente coerente in futuro quando sarà supportato il controllo della versione HDCP. Lo snippet seguente illustra una configurazione con questo valore HDCP.

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

* **D.** *I vincoli pixel RBOP sono discreti o basati su intervalli?* **R.** I vincoli dei pixel RBOP sono basati sull&#39;intervallo. Ogni conteggio di pixel definisce i requisiti per tutti i conteggi di pixel minori o uguali al conteggio specificato o fino al conteggio più grande minore di tale valore, se esiste più di un vincolo pixel. In breve, i valori si applicano come soglie massime per ogni conteggio di pixel verticali.

   Supponiamo che un flusso MBR con risoluzioni verticali di 240, 480, 600, 720 e 1080 venga passato al lettore con le seguenti impostazioni RBOP.

   **Impostazioni criteri RBOP:**

   * 720P - HDCP richiesto
   * 480P - Nessun OP

   Le seguenti regole vengono applicate a ogni variante.

   **Flussi:**

   * 240, 480: entrambi sono &lt;= 480; non è richiesto alcun OP e i flussi verranno caricati con o senza HDCP presente.
   * 600, 720: entrambi sono &lt;= 720; per la riproduzione è richiesto l&#39;HDCP
   * 1080: > 720; il flusso viene inserito nell’elenco dei blocchi (errore restituito) perché non si trova nelle regole precedenti.


* **D.** Su alcuni dei miei dispositivi Android, le restrizioni di conteggio dei pixel che ho definito non vengono applicate esattamente come definito. Cosa sta succedendo?

   **R.** Alcuni dispositivi Android segnalano dimensioni dei fotogrammi leggermente superiori alle dimensioni normali. Per risolvere questo problema, regolare le dimensioni dei frame ( `maxPixel` e `pixelCount` di 20 pixel. Ad esempio, è possibile regolare le dimensioni dei fotogrammi verso l&#39;alto, da:

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

   in, per tutte le istanze di `maxPixel` e `pixelCount`.
