---
seo-title: Revoca delle credenziali client e runtime DRM
title: Revoca delle credenziali client e runtime DRM
uuid: 774b8ac7-51bb-42fc-a05d-cfa718e24a81
translation-type: tm+mt
source-git-commit: fbc175f383c850a7286b1e6e89daa027e00b29ef
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---


# Revoca delle credenziali client e runtime DRM{#revoking-drm-client-and-runtime-credentials}

Le versioni DRM/Runtime sono identificate dal livello di protezione, dal numero di versione e da altri attributi, inclusi il sistema operativo e il runtime. Per limitare le versioni DRM/Runtime consentite, impostate le limitazioni del modulo in un criterio o in un `HandlerConfiguration`. Le restrizioni ai moduli possono includere un livello di protezione minimo e un elenco delle versioni dei moduli che non possono essere rilasciate. Consultate [Blocco elenco di client DRM con restrizioni all&#39;accesso al contenuto](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-blocklist-drm-clients.md) protetto per informazioni dettagliate sugli attributi utilizzati per identificare un modulo DRM/Runtime.

Se è impostato il livello di protezione minimo, la versione sul client (specificata nel token del computer) deve essere maggiore o uguale al valore specificato.

Se viene specificato un elenco di versioni escluse e la versione del client corrisponde a uno qualsiasi degli identificatori di versione nell&#39;elenco, al client non sarà consentito utilizzare un diritto contenente questa istanza ModuleRequirements. Affinché un modulo corrisponda alle informazioni sulla versione, tutti i parametri specificati nelle informazioni sulla versione, ad eccezione della versione release, devono corrispondere esattamente ai valori dei moduli. La versione di rilascio corrisponde se il valore del modulo client è minore o uguale al valore nelle informazioni sulla versione.

Nel caso in cui venga segnalata una violazione con una particolare versione di DRM client o runtime, il proprietario del contenuto e il distributore di contenuti (che esegue il server licenze) possono configurare il server in modo che rifiutino di rilasciare licenze durante un periodo in cui Adobe non dispone di una correzione. Questo può essere configurato tramite `HandlerConfiguration` come descritto in precedenza, o modificando tutti i criteri. In quest&#39;ultimo caso, potete mantenere un elenco di aggiornamento dei criteri e utilizzarlo per verificare se un criterio è stato aggiornato o revocato.

Se è necessaria una versione più recente di Adobe® Flash® Player/Adobe® AIR® Runtime o della libreria Adobe Content Protection (modulo DRM), aggiornate i criteri come mostrato in [Aggiornamento di un criterio tramite l&#39;API](../../aaxs-protecting-content/content-working-with-policies/content-updating-policy-using-java-api.md) Java e create un elenco di aggiornamento dei criteri, oppure impostate le limitazioni in `HandlerConfiguration` richiamando `HandlerConfiguration.setRuntimeModuleRequirements()` o `HandlerConfiguration.setDRMModuleRequirements()`. Quando un utente richiede una nuova licenza con questi elenchi di blocchi abilitati, prima di rilasciare una licenza è necessario installare i tempi di esecuzione e le librerie più recenti. Per un esempio di elenco dei blocchi in cui sono elencate le versioni DRM e runtime, consultate il codice di esempio in [Aggiornamento di un criterio tramite l&#39;API](../../aaxs-protecting-content/content-working-with-policies/content-updating-policy-using-java-api.md)Java.
