---
seo-title: Abilita demo modello di utilizzo
title: Abilita demo modello di utilizzo
uuid: 43930ebb-e936-4f48-990d-7ad19992e326
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '62'
ht-degree: 0%

---


# Abilita demo modello di utilizzo{#enable-the-usage-model-demo}

1. Specificare la proprietà personalizzata `RI_UsageModelDemo=true` al momento della creazione del pacchetto.

   Se state creando un pacchetto di contenuto tramite lo strumento della riga di comando Media Packager, immettete:

   ```
   java -jar AdobeMediaPackager.jar [<i>source_file</i>] [<i>dest_file</i>] -k RI_UsageModelDemo=true
   ```

>[!NOTE]
>
>Se non si attiva la modalità demo opzionale al momento della creazione del pacchetto, il server licenze rilascia una licenza in base al primo criterio DRM valido elaborato.

