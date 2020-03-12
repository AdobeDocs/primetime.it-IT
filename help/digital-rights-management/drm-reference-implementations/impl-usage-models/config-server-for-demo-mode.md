---
description: 'null'
seo-description: 'null'
seo-title: Configurare la modalità demo del modello di utilizzo
title: Configurare la modalità demo del modello di utilizzo
uuid: f818c7fc-e88f-4fa4-926e-08a1337b28d3
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Configurare la modalità demo del modello di utilizzo{#configure-usage-model-demo-mode}

Prima che il server di implementazione di riferimento possa rilasciare licenze per la demo del modello di utilizzo, devi configurare il server per specificare in che modo vengono generate le licenze per ciascuno dei quattro modelli di utilizzo. Ciò significa che è necessario specificare un criterio DRM per ciascun modello di utilizzo. L&#39;implementazione di riferimento include i seguenti criteri DRM di esempio nella [!DNL Reference Implementation/Server/Reference Implementation Server/resources/] directory:

* `dto-policy.pol` - (Download-In-Proprio)
* `vod-policy.pol` - (Affitto/Video-On-Demand)
* `sub-policy.pol` - (Iscrizione)
* `ad-policy.pol` - (Ad-funding)

>[!NOTE]
>
>Potete sostituire questi criteri di esempio con criteri DRM personalizzati.

1. Impostate queste proprietà in [!DNL flashaccess-refimpl.properties] per specificare il criterio DRM che prevedete di applicare a ciascun modello di utilizzo:

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

1. Copiate i file dei criteri di esempio nella directory specificata nella `config.resourcesDirectory` proprietà in [!DNL flashaccess-refimpl.properties].
