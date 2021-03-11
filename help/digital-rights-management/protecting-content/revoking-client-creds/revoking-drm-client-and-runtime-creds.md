---
title: Revoca delle credenziali del client DRM e del runtime
description: Revoca delle credenziali del client DRM e del runtime
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---


# Revoca delle credenziali del client DRM e del runtime {#revoking-drm-client-and-runtime-credentials}

Le versioni DRM/Runtime sono identificate dal livello di sicurezza, dal numero di versione e da altri attributi, tra cui Sistema operativo e runtime. Per limitare le versioni DRM/Runtime consentite, imposta le restrizioni del modulo in un criterio DRM o in un `HandlerConfiguration`. Le restrizioni al modulo possono includere un livello minimo di sicurezza e un elenco di versioni del modulo che non possono essere rilasciate.

Per informazioni sugli attributi utilizzati per identificare un modulo DRM/Runtime, consulta [Elenco Bloccati di client DRM con restrizioni all’accesso a contenuto protetto](../../protecting-content/introduction/usage-rules/runtime-application-restrictions/blocklist-drm-clients.md) .

Se è impostato il livello di protezione minimo, la versione sul client (specificata nel token del computer) deve essere maggiore o uguale al valore specificato.

Se viene specificato un elenco di versioni escluse e la versione del client corrisponde a uno qualsiasi degli identificatori di versione nell’elenco, al client non sarà consentito utilizzare un diritto contenente questa istanza ModuleRequirements. Affinché un modulo corrisponda alle informazioni sulla versione, tutti i parametri specificati nelle informazioni sulla versione, ad eccezione della versione di rilascio, devono corrispondere esattamente ai valori dei moduli. La versione di rilascio corrisponde se il valore del modulo client è minore o uguale al valore nelle informazioni sulla versione.

Nel caso in cui venga segnalata una violazione con un particolare client DRM o una versione runtime, il proprietario del contenuto e il distributore di contenuti (che esegue il server licenze) possono configurare il server in modo che rifiutino di rilasciare licenze durante un periodo in cui Adobe non dispone di una correzione. Questo può essere configurato tramite `HandlerConfiguration` come descritto sopra, o apportando modifiche a tutti i criteri DRM. In quest&#39;ultimo caso, puoi mantenere un elenco di aggiornamento dei criteri DRM e utilizzarlo per verificare se un criterio DRM è stato aggiornato o revocato.

Se hai bisogno di una versione più recente di Adobe Flash Player/Adobe AIR Runtime o della libreria Adobe Content Protection (modulo DRM), devi aggiornare i criteri DRM.

Consulta [Aggiornamento di un criterio utilizzando l&#39;API Java](../../protecting-content/working-policies-overview/updating-policy-using-java-api.md).

Quindi devi creare un elenco di aggiornamento dei criteri DRM o impostare le restrizioni in `HandlerConfiguration` richiamando `HandlerConfiguration.setRuntimeModuleRequirements()` o `HandlerConfiguration.setDRMModuleRequirements()`. Quando un utente richiede una nuova licenza con gli elenchi Bloccati specificati abilitati, è necessario installare i runtime e le librerie più recenti prima di poter rilasciare una licenza.

Vedi il codice di esempio in [Aggiornamento di un criterio utilizzando l&#39;API Java Per un esempio su un elenco a blocchi di DRM e versioni di runtime](../../protecting-content/working-policies-overview/updating-policy-using-java-api.md) per un esempio su un elenco a blocchi di versioni DRM e runtime.
