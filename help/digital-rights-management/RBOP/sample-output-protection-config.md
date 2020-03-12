---
description: Questa sezione presenta una configurazione di esempio che illustra i concetti e la forma della configurazione.
seo-description: Questa sezione presenta una configurazione di esempio che illustra i concetti e la forma della configurazione.
seo-title: Esempio di configurazione RBOP
title: Esempio di configurazione RBOP
uuid: fa5ead93-36c5-4ad1-947b-c4f1f2632d9b
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# Esempio di configurazione RBOP {#sample-rbop-configuration}

Questa sezione presenta una configurazione di esempio che illustra i concetti e la forma della configurazione.

La seguente configurazione JSON di esempio definisce un criterio di output dei pixel che specifica quanto segue:

* Limita la decrittazione del video alle risoluzioni 1080 o inferiori
* Imporre vincoli specifici per le risoluzioni 720 e 480:

   * Per una risoluzione 720: richiedono HDCP per l&#39;uscita digitale; richiede un sistema di gestione della generazione *di copie - protezione analogica* (CGMS-A) per l&#39;uscita analogica.
   * Per 480 risoluzioni: richiedono HDCP per l&#39;uscita digitale; non richiedono protezione per l&#39;analogico

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

Tenete presente quanto segue sulla configurazione di esempio precedente:

* Le `pixelCount` specifiche sono un livello giù nella struttura JSON, all&#39;interno della `pixelConstraints` sezione.

* All&#39;interno di ogni specifica di conteggio dei pixel, la protezione dell&#39;output è specificata sia per l&#39;uscita digitale che per quella analogica.
* Nelle specifiche di uscita digitale, sono specificate le versioni HDCP, anche se il client non supporta attualmente la versione HDCP. Per ulteriori informazioni, consulta le Domande frequenti.

