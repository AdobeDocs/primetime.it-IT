---
seo-title: L'applicazione SWF consente l'elencazione
title: L'applicazione SWF consente l'elencazione
uuid: e3021ae9-54f4-4bcf-a274-515ae765f74b
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# L&#39;applicazione SWF consente l&#39;elencazione {#swf-application-allowlisting}

Per  elenco consentiti di un&#39;applicazione SWF, potete seguire una delle due strategie seguenti:

* Potete specificare un URL per un file SWF. Si tratta di un approccio molto flessibile, soprattutto in un ambiente di sviluppo in cui si sta rigenerando regolarmente il file SWF.
* Potete specificare un HASH SWF. Si tratta di un valore digest crittografato del file SWF. Questo approccio è meno flessibile (ma molto più rigoroso), in quanto l&#39;HASH SWF cambierà quando l&#39;applicazione cambia e viene ricreata. In questa situazione, tutti i contenuti associati al precedente HASH non potranno essere riprodotti sul nuovo lettore e dovranno essere reimpostati. Lo [!DNL PolicyManager.jar] strumento calcola automaticamente l&#39;hash se si specifica un [!DNL .swf] file.

   D&#39;altro canto, se utilizzate DRM di Primetime tramite Flash/Adobe Media Server (FMS/AMS), potete fornire il percorso dei file SWF specifici, e FMS/AMS hash automaticamente i file SWF da inserire nel criterio DRM utilizzato per creare il pacchetto dei contenuti in streaming da FMS/AMS.

Per informazioni dettagliate, consultate `policy.allowedSWFApplication.n` in Proprietà *di* configurazione.
