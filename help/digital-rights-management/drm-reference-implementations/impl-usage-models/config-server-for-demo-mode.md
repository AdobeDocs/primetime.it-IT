---
title: Configurare la modalità demo del modello di utilizzo
description: Configurare la modalità demo del modello di utilizzo
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---


# Configura la modalità demo del modello di utilizzo{#configure-usage-model-demo-mode}

Prima che il server di implementazione di riferimento possa rilasciare licenze per la demo del modello di utilizzo, devi configurare il server per specificare come vengono generate le licenze per ciascuno dei quattro modelli di utilizzo. Ciò significa che devi specificare un criterio DRM per ciascun modello di utilizzo. L’implementazione di riferimento include i seguenti criteri DRM di esempio nella directory [!DNL Reference Implementation/Server/Reference Implementation Server/resources/] :

* `dto-policy.pol` - (Download-To-own)
* `vod-policy.pol` - (Affitto/Video-On-Demand)
* `sub-policy.pol` - (abbonamento)
* `ad-policy.pol` - (con finanziamento pubblicitario)

>[!NOTE]
>
>È possibile sostituire questi criteri di esempio con i propri criteri DRM.

1. Imposta queste proprietà in [!DNL flashaccess-refimpl.properties] per specificare il criterio DRM che intendi applicare a ogni modello di utilizzo:

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

1. Copia i file dei criteri di esempio nella directory specificata nella proprietà `config.resourcesDirectory` in [!DNL flashaccess-refimpl.properties].
