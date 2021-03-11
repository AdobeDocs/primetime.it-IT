---
title: Inserimento di applicazioni SWF nell’elenco Consentiti
description: Inserimento di applicazioni SWF nell’elenco Consentiti
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# Inserimento di applicazioni SWF nell&#39;elenco Consentiti {#swf-application-allowlisting}

Per elenco consentiti di un&#39;applicazione SWF, è possibile seguire una delle due strategie seguenti:

* È possibile specificare un URL per un file SWF. Questo è un approccio molto flessibile, soprattutto in un ambiente di sviluppo in cui si sta ricostruendo regolarmente il SWF.
* È possibile specificare un HASH SWF. Si tratta di un valore digest crittografato del tuo SWF. Questo approccio è meno flessibile (ma molto più rigoroso), in quanto SWF HASH cambierà quando l&#39;applicazione cambia e viene ricostruita. In questa situazione, tutti i contenuti legati al precedente HASH non potranno giocare sul nuovo giocatore e dovranno essere riconfezionati. Lo strumento [!DNL PolicyManager.jar] calcola automaticamente l’hash se si specifica un file [!DNL .swf].

   D&#39;altro canto, se utilizzi Primetime DRM tramite Flash/Adobe Medium Server (FMS/AMS), puoi fornire il percorso dei tuoi particolari SWF, e FMS/AMS cancellerà automaticamente i SWF da inserire nel criterio DRM che viene utilizzato per creare il pacchetto dei contenuti in streaming da FMS/AMS.

Per ulteriori informazioni, consulta `policy.allowedSWFApplication.n` in *Proprietà di configurazione* .
