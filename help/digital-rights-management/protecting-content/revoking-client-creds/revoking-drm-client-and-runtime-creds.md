---
title: Revoca delle credenziali di runtime e del client DRM
description: Revoca delle credenziali di runtime e del client DRM
copied-description: true
exl-id: 3a91a256-ab01-48d8-99f3-854195faae6f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# Revoca delle credenziali di runtime e del client DRM {#revoking-drm-client-and-runtime-credentials}

Le versioni DRM/Runtime sono identificate dal livello di protezione, dal numero di versione e da altri attributi, inclusi il sistema operativo e il runtime. Per limitare le versioni DRM/Runtime consentite, impostare le restrizioni del modulo in un criterio DRM o in un `HandlerConfiguration`. Le limitazioni del modulo possono includere un livello di sicurezza minimo e un elenco di versioni del modulo a cui non è consentito rilasciare una licenza.

Consulta [Elenco Bloccati di client DRM a cui è limitato l&#39;accesso ai contenuti protetti](../../protecting-content/introduction/usage-rules/runtime-application-restrictions/blocklist-drm-clients.md) per informazioni dettagliate sugli attributi utilizzati per identificare un modulo DRM/Runtime.

Se è impostato il livello di protezione minimo, la versione sul client (specificata nel token del computer) deve essere maggiore o uguale al valore specificato.

Se viene specificato un elenco di versioni escluse e la versione del client corrisponde a uno qualsiasi degli identificatori di versione nell’elenco, al client non sarà consentito utilizzare un diritto contenente questa istanza ModuleRequirements. Affinché un modulo corrisponda alle informazioni sulla versione, tutti i parametri specificati nelle informazioni sulla versione, ad eccezione della versione di rilascio, devono corrispondere esattamente ai valori dei moduli. La versione di rilascio corrisponde se il valore del modulo client è minore o uguale al valore indicato nelle informazioni sulla versione.

Nel caso in cui venga segnalata una violazione con una particolare versione del client DRM o runtime, il proprietario del contenuto e il distributore di contenuto (che esegue il server licenze) possono configurare il server per rifiutare il rilascio delle licenze durante un periodo in cui Adobe non dispone di una correzione. Questa può essere configurata tramite `HandlerConfiguration` come descritto in precedenza o apportando modifiche a tutte le regole DRM. In quest&#39;ultimo caso, è possibile gestire un elenco di aggiornamento dei criteri DRM e utilizzarlo per verificare se un criterio DRM è stato aggiornato o revocato.

Se hai bisogno di una versione più recente del Flash Player Adobe/Adobe AIR Runtime o della libreria di protezione dei contenuti Adobi (modulo DRM), devi aggiornare i criteri DRM.

Consulta [Aggiornamento di un criterio tramite API Java](../../protecting-content/working-policies-overview/updating-policy-using-java-api.md).

Quindi è necessario creare un elenco di aggiornamento dei criteri DRM o impostare restrizioni in `HandlerConfiguration` richiamando `HandlerConfiguration.setRuntimeModuleRequirements()` o `HandlerConfiguration.setDRMModuleRequirements()`. Quando un utente richiede una nuova licenza con gli elenchi Bloccati specificati abilitati, è necessario installare le librerie e i runtime più recenti prima di poter rilasciare una licenza.

Vedi il codice di esempio in [Aggiornamento di un criterio utilizzando l’API Java Per un esempio sull’elenco di blocchi DRM e versioni di runtime](../../protecting-content/working-policies-overview/updating-policy-using-java-api.md) per un esempio sull’elenco Bloccati delle versioni DRM e runtime.
