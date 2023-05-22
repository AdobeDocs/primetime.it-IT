---
description: Questa sezione presenta una configurazione di esempio che illustra i concetti e la forma della configurazione.
title: Configurazione RBOP di esempio
exl-id: 0f40be83-9c7f-482b-ac42-9aa4e3f46f58
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---

# Configurazione RBOP di esempio {#sample-rbop-configuration}

Questa sezione presenta una configurazione di esempio che illustra i concetti e la forma della configurazione.

La seguente configurazione JSON di esempio definisce un criterio di output in pixel che specifica quanto segue:

* Limita la decrittografia del video a risoluzioni pari o inferiori a 1080
* Imporre vincoli specifici per le risoluzioni 720 e 480:

   * Per la risoluzione 720: richiede HDCP per l&#39;uscita digitale; richiede *Sistema di gestione generazione copie - Analogico* (CGMS-A) per uscita analogica.
   * Per la risoluzione 480: richiede HDCP per l&#39;uscita digitale; non richiede protezione per l&#39;uscita analogica

```
{ 
  "pixelConstraints":  
    [ 
      { 
        "pixelCount": 720, 
        "digital": 
          [ 
            {"output": "REQUIRED", "hdcp": {"major": 1, "minor": 0}} 
          ], 
        "analog": {"output": "REQUIRED_CGMSA"} 
      }, 
      { 
        "pixelCount": 480, 
        "digital":  
          [ 
            {"output": "REQUIRED", "hdcp": {"major": 1, "minor": 0}} 
          ], 
        "analog": {"output": "NO_PROTECTION"} 
      } 
    ], 
  "maxPixel": 1080 
}
```

Per quanto riguarda la configurazione di esempio precedente, tieni presente quanto segue:

* Il `pixelCount` le specifiche sono di un livello inferiore nella struttura JSON, all’interno del `pixelConstraints` sezione.

* All&#39;interno di ogni specifica di pixel, la protezione dell&#39;uscita è specificata sia per l&#39;uscita digitale che per quella analogica.
* Nelle specifiche dell&#39;uscita digitale, sono specificate le versioni HDCP, anche se il client non supporta attualmente il controllo delle versioni HDCP. Per ulteriori informazioni, consulta le Domande frequenti.
