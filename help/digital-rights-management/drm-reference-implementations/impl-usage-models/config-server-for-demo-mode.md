---
title: Configurare la modalità demo del modello di utilizzo
description: Configurare la modalità demo del modello di utilizzo
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# Configurare la modalità demo del modello di utilizzo{#configure-usage-model-demo-mode}

Prima che il server di implementazione di riferimento possa rilasciare licenze per la demo del modello di utilizzo, è necessario configurare il server per specificare la modalità di generazione delle licenze per ciascuno dei quattro modelli di utilizzo. Ciò significa che è necessario specificare un criterio DRM per ogni modello di utilizzo. L’implementazione di riferimento include i seguenti criteri DRM di esempio nella [!DNL Reference Implementation/Server/Reference Implementation Server/resources/] directory:

* `dto-policy.pol` - (Download-To-Own)
* `vod-policy.pol` - (noleggio/video on demand)
* `sub-policy.pol` - (Abbonamento)
* `ad-policy.pol` - (Ad-supported)

>[!NOTE]
>
>È possibile sostituire questi criteri di esempio con criteri DRM personalizzati.

1. Imposta queste proprietà in [!DNL flashaccess-refimpl.properties] per specificare il criterio DRM che si intende applicare a ogni modello di utilizzo:

   ```
   # DRM Policy file name for Download To Own usage 
   RefImpl.UsageModelDemo.Policy.DTO=dto-policy.pol 
   # DRM Policy file name for Rental usage 
   RefImpl.UsageModelDemo.Policy.VOD=vod-policy.pol 
   # DRM Policy file name for Subscription usage 
   RefImpl.UsageModelDemo.Policy.Subscribe=sub-policy.pol 
   # DRM Policy file name for Ad Supported (free) usage 
   RefImpl.UsageModelDemo.Policy.Free=ad-policy.pol
   ```

1. Copiare i file dei criteri di esempio nella directory specificata nel `config.resourcesDirectory` proprietà in [!DNL flashaccess-refimpl.properties].
