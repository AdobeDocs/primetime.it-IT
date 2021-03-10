---
title: Revoca delle credenziali del client DRM e del runtime
description: Revoca delle credenziali del client DRM e del runtime
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---


# Revoca delle credenziali del client DRM e del runtime{#revoking-drm-client-and-runtime-credentials}

Le versioni DRM/Runtime sono identificate dal livello di sicurezza, dal numero di versione e da altri attributi, inclusi il sistema operativo e il runtime. Per limitare le versioni DRM/Runtime consentite, imposta le restrizioni del modulo in un criterio o in un `HandlerConfiguration`. Le restrizioni al modulo possono includere un livello minimo di sicurezza e un elenco di versioni del modulo che non possono essere rilasciate. Per informazioni sugli attributi utilizzati per identificare un modulo DRM/Runtime, consulta [Elenco Bloccati di client DRM con restrizioni all’accesso a contenuto protetto](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-blocklist-drm-clients.md) .

Se è impostato il livello di protezione minimo, la versione sul client (specificata nel token del computer) deve essere maggiore o uguale al valore specificato.

Se viene specificato un elenco di versioni escluse e la versione del client corrisponde a uno qualsiasi degli identificatori di versione nell’elenco, al client non sarà consentito utilizzare un diritto contenente questa istanza ModuleRequirements. Affinché un modulo corrisponda alle informazioni sulla versione, tutti i parametri specificati nelle informazioni sulla versione, ad eccezione della versione di rilascio, devono corrispondere esattamente ai valori dei moduli. La versione di rilascio corrisponde se il valore del modulo client è minore o uguale al valore nelle informazioni sulla versione.

Nel caso in cui venga segnalata una violazione con un particolare client DRM o una versione runtime, il proprietario del contenuto e il distributore di contenuti (che esegue il server licenze) possono configurare il server in modo che rifiutino di rilasciare licenze durante un periodo in cui Adobe non dispone di una correzione. È possibile configurarlo tramite `HandlerConfiguration` come descritto in precedenza o apportando modifiche a tutti i criteri. In quest&#39;ultimo caso, è possibile mantenere un elenco di aggiornamento dei criteri e utilizzarlo per verificare se un criterio è stato aggiornato o revocato.

Se hai bisogno di una versione più recente di Adobe® Flash® Player/Adobe® AIR® Runtime o della libreria Adobe Content Protection (modulo DRM), aggiorna i criteri come mostrato in [Aggiornamento di un criterio utilizzando l&#39;API Java](../../aaxs-protecting-content/content-working-with-policies/content-updating-policy-using-java-api.md) e crea un elenco di aggiornamento dei criteri o imposta le restrizioni in `HandlerConfiguration` richiamando `HandlerConfiguration.setRuntimeModuleRequirements()` o `HandlerConfiguration.setDRMModuleRequirements()`. Quando un utente richiede una nuova licenza con questi elenchi Bloccati abilitati, è necessario installare i tempi di esecuzione e le librerie più recenti prima di rilasciare una licenza. Per un esempio sul blocco di DRM e versioni di runtime, vedi il codice di esempio in [Aggiornamento di un criterio tramite l&#39;API Java](../../aaxs-protecting-content/content-working-with-policies/content-updating-policy-using-java-api.md).
