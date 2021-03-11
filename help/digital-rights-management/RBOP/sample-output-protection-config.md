---
description: Questa sezione presenta una configurazione di esempio che illustra i concetti e la forma della configurazione.
title: Esempio di configurazione RBOP
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---


# Esempio di configurazione RBOP {#sample-rbop-configuration}

Questa sezione presenta una configurazione di esempio che illustra i concetti e la forma della configurazione.

La seguente configurazione JSON di esempio definisce un criterio di output dei pixel che specifica quanto segue:

* Limita la decrittografia del video alle risoluzioni di 1080 o inferiori
* Imporre vincoli specifici per le risoluzioni 720 e 480:

   * Per la risoluzione 720: richiedono HDCP per l&#39;uscita digitale; richiedere la protezione *Copy Generation Management System - Analogico* (CGMS-A) per l&#39;uscita analogica.
   * Per la risoluzione 480: richiedono HDCP per l&#39;uscita digitale; non richiedono protezione per l&#39;analogico

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

Tieni presente quanto segue sulla configurazione di esempio precedente:

* Le specifiche `pixelCount` sono di un livello verso il basso nella struttura JSON, all&#39;interno della sezione `pixelConstraints`.

* All&#39;interno di ogni specifica di conteggio dei pixel, la protezione dell&#39;output è specificata sia per l&#39;uscita digitale che per quella analogica.
* Nelle specifiche di uscita digitale, vengono specificate le versioni HDCP, anche se il client al momento non supporta il controllo delle versioni HDCP. Per ulteriori informazioni, consulta le Domande frequenti .

