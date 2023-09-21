---
title: Revoca delle credenziali di runtime e del client DRM
description: Revoca delle credenziali di runtime e del client DRM
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# Revoca delle credenziali di runtime e del client DRM{#revoking-drm-client-and-runtime-credentials}

Le versioni DRM/Runtime sono identificate dal livello di protezione, dal numero di versione e da altri attributi, inclusi il sistema operativo e il runtime. Per limitare le versioni DRM/runtime consentite, impostare le restrizioni del modulo in un criterio o in un `HandlerConfiguration`. Le limitazioni del modulo possono includere un livello di sicurezza minimo e un elenco di versioni del modulo a cui non è consentito rilasciare una licenza. Consulta [Elenco Bloccati di client DRM a cui è limitato l&#39;accesso ai contenuti protetti](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-blocklist-drm-clients.md) per informazioni dettagliate sugli attributi utilizzati per identificare un modulo DRM/Runtime.

Se è impostato il livello di protezione minimo, la versione sul client (specificata nel token del computer) deve essere maggiore o uguale al valore specificato.

Se viene specificato un elenco di versioni escluse e la versione del client corrisponde a uno qualsiasi degli identificatori di versione nell’elenco, al client non sarà consentito utilizzare un diritto contenente questa istanza ModuleRequirements. Affinché un modulo corrisponda alle informazioni sulla versione, tutti i parametri specificati nelle informazioni sulla versione, ad eccezione della versione di rilascio, devono corrispondere esattamente ai valori dei moduli. La versione di rilascio corrisponde se il valore del modulo client è minore o uguale al valore indicato nelle informazioni sulla versione.

Nel caso in cui venga segnalata una violazione con una particolare versione del client DRM o runtime, il proprietario del contenuto e il distributore di contenuto (che esegue il server licenze) possono configurare il server per rifiutare il rilascio delle licenze durante un periodo in cui Adobe non dispone di una correzione. Questa può essere configurata tramite `HandlerConfiguration` come descritto in precedenza, o apportando modifiche a tutte le politiche. In quest&#39;ultimo caso, è possibile gestire un elenco di aggiornamenti dei criteri e utilizzarlo per verificare se un criterio è stato aggiornato o revocato.

Se hai bisogno di una versione più recente di Adobe® Flash® Player/Adobe® AIR® Runtime o della libreria di protezione dei contenuti Adobi (modulo DRM), aggiorna i criteri come mostrato nella [Aggiornamento di un criterio tramite API Java](../../aaxs-protecting-content/content-working-with-policies/content-updating-policy-using-java-api.md) e creare un Elenco di aggiornamento dei criteri o impostare restrizioni in `HandlerConfiguration` richiamando `HandlerConfiguration.setRuntimeModuleRequirements()` o `HandlerConfiguration.setDRMModuleRequirements()`. Quando un utente richiede una nuova licenza con questi elenchi Bloccati abilitati, è necessario installare le librerie e i runtime più recenti prima di poter rilasciare una licenza. Per un esempio sull’elenco a blocchi delle versioni DRM e runtime, vedi il codice di esempio in [Aggiornamento di un criterio tramite API Java](../../aaxs-protecting-content/content-working-with-policies/content-updating-policy-using-java-api.md).
