---
title: Inserimento di applicazioni SWF nell’elenco Consentiti
description: Inserimento di applicazioni SWF nell’elenco Consentiti
copied-description: true
exl-id: ae8b7f52-897f-43f9-ac7b-665d4b8c16b8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# Inserimento di applicazioni SWF nell’elenco Consentiti {#swf-application-allowlisting}

Per elenco consentiti un’applicazione SWF, puoi seguire una delle due strategie seguenti:

* Puoi specificare un URL per un SWF. Si tratta di un approccio molto flessibile, soprattutto in un ambiente di sviluppo in cui si sta ricostruendo regolarmente il SWF.
* Puoi specificare un HASH SWF. Si tratta di un valore di digest crittografico del SWF. Questo approccio è meno flessibile (ma molto più rigoroso), in quanto l’HASH del SWF cambia quando l’applicazione cambia e viene ricostruita. In questa situazione, tutti i contenuti associati all’HASH precedente non verranno riprodotti sul nuovo lettore e dovranno essere ricompilati. Il [!DNL PolicyManager.jar] calcolerà automaticamente l&#39;hash se si specifica un [!DNL .swf] file.

   Se invece si utilizza Primetime DRM tramite Flash/Adobe Medium Server (FMS/AMS), è possibile specificare il percorso dei SWF specifici e FMS/AMS eseguirà automaticamente l&#39;hash dei SWF da inserire nel criterio DRM utilizzato per creare il pacchetto del contenuto in streaming da FMS/AMS.

Consulta `policy.allowedSWFApplication.n` in *Proprietà di configurazione* per i dettagli.
