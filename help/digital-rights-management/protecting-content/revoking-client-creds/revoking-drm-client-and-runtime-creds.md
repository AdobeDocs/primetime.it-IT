---
seo-title: Revoca delle credenziali client e runtime DRM
title: Revoca delle credenziali client e runtime DRM
uuid: 8e36536a-8eed-4d27-8a5f-8d3219817e57
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---


# Revoca delle credenziali client e runtime DRM {#revoking-drm-client-and-runtime-credentials}

Le versioni DRM/Runtime sono identificate dal livello di protezione, dal numero di versione e da altri attributi, compresi il sistema operativo e il runtime. Per limitare le versioni DRM/Runtime consentite, impostate le limitazioni del modulo in un criterio DRM o in un `HandlerConfiguration`. Le restrizioni ai moduli possono includere un livello di protezione minimo e un elenco delle versioni dei moduli che non possono essere rilasciate.

Consultate [Blocco elenco di client DRM con restrizioni all&#39;accesso al contenuto](../../protecting-content/introduction/usage-rules/runtime-application-restrictions/blocklist-drm-clients.md) protetto per informazioni dettagliate sugli attributi utilizzati per identificare un modulo DRM/Runtime.

Se è impostato il livello di protezione minimo, la versione sul client (specificata nel token del computer) deve essere maggiore o uguale al valore specificato.

Se viene specificato un elenco di versioni escluse e la versione del client corrisponde a uno qualsiasi degli identificatori di versione nell&#39;elenco, al client non sarà consentito utilizzare un diritto contenente questa istanza ModuleRequirements. Affinché un modulo corrisponda alle informazioni sulla versione, tutti i parametri specificati nelle informazioni sulla versione, ad eccezione della versione release, devono corrispondere esattamente ai valori dei moduli. La versione di rilascio corrisponde se il valore del modulo client è minore o uguale al valore nelle informazioni sulla versione.

Nel caso in cui venga segnalata una violazione con una particolare versione di DRM client o runtime, il proprietario del contenuto e il distributore di contenuti (che esegue il server licenze) possono configurare il server in modo che rifiutino di rilasciare licenze durante un periodo in cui Adobe non dispone di una correzione. Questo può essere configurato tramite `HandlerConfiguration` come descritto in precedenza, o modificando tutti i criteri DRM. In quest&#39;ultimo caso, potete mantenere un elenco di aggiornamento dei criteri DRM e usarlo per verificare se un criterio DRM è stato aggiornato o revocato.

Se è necessaria una versione più recente di Adobe Flash Player/Adobe AIR Runtime o della libreria Adobe Content Protection (modulo DRM), è necessario aggiornare i criteri DRM.

Consultate [Aggiornamento di un criterio tramite l&#39;API](../../protecting-content/working-policies-overview/updating-policy-using-java-api.md)Java.

Quindi devi creare un elenco di aggiornamento criteri DRM o impostare le restrizioni in `HandlerConfiguration` richiamando `HandlerConfiguration.setRuntimeModuleRequirements()` o `HandlerConfiguration.setDRMModuleRequirements()`. Quando un utente richiede una nuova licenza con gli elenchi di blocchi specificati abilitati, è necessario installare i runtime e le librerie più recenti prima di poter rilasciare una licenza.

Vedere il codice di esempio in [Aggiornamento di un criterio tramite l&#39;API JavaPer un esempio in cui sono elencate versioni](../../protecting-content/working-policies-overview/updating-policy-using-java-api.md) DRM e runtime per un esempio in cui sono elencati i blocchi DRM e le versioni runtime.
