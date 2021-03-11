---
title: Attiva la demo del modello di utilizzo
description: Attiva la demo del modello di utilizzo
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '62'
ht-degree: 0%

---


# Attiva la demo del modello di utilizzo{#enable-the-usage-model-demo}

1. Specifica la proprietà personalizzata `RI_UsageModelDemo=true` al momento della creazione del pacchetto.

   Se si crea un pacchetto di contenuto utilizzando lo strumento a riga di comando Media Packager, immettere:

   ```
   java -jar AdobeMediaPackager.jar [<i>source_file</i>] [<i>dest_file</i>] -k RI_UsageModelDemo=true
   ```

>[!NOTE]
>
>Se non si attiva la modalità demo opzionale al momento dell&#39;imballaggio, il server licenze rilascia una licenza in base al primo criterio DRM valido che elabora.

