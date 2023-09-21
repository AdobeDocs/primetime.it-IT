---
title: Abilita la demo del modello di utilizzo
description: Abilita la demo del modello di utilizzo
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '62'
ht-degree: 0%

---

# Abilita la demo del modello di utilizzo{#enable-the-usage-model-demo}

1. Specificare la proprietà personalizzata `RI_UsageModelDemo=true` al momento del confezionamento.

   Se stai creando il pacchetto di contenuto utilizzando lo strumento della riga di comando di Media Packager, immetti:

   ```
   java -jar AdobeMediaPackager.jar [<i>source_file</i>] [<i>dest_file</i>] -k RI_UsageModelDemo=true
   ```

>[!NOTE]
>
>Se non si attiva la modalità demo opzionale al momento del packaging, il server licenze rilascia una licenza in base al primo criterio DRM valido elaborato.
