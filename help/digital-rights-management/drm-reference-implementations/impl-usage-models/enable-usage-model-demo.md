---
seo-title: Abilita demo modello di utilizzo
title: Abilita demo modello di utilizzo
uuid: 43930ebb-e936-4f48-990d-7ad19992e326
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Abilita demo modello di utilizzo{#enable-the-usage-model-demo}

1. Specificate la proprietà personalizzata `RI_UsageModelDemo=true` al momento della creazione del pacchetto.

   Se state creando un pacchetto di contenuto tramite lo strumento della riga di comando Media Packager, immettete:

   ```
   java -jar AdobeMediaPackager.jar [
   
<i>source_file</i>] [<i>dest_file</i>] -k RI_UsageModelDemo=true

```
>[!NOTE] {class="- topic/note "}
>
>If you do not activate the optional demo mode at packaging time, the license server issues a license based on the first valid DRM policy it processes.

