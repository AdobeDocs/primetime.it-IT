---
seo-title: Anteprima licenza
title: Anteprima licenza
uuid: 3069aa16-5bf3-4af6-801c-ad823530d7eb
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Anteprima licenza{#license-preview}

Il client può inviare una richiesta di anteprima della licenza, il che significa che l&#39;applicazione può eseguire un&#39;operazione di anteprima prima di chiedere all&#39;utente di acquistare il contenuto per determinare se il computer dell&#39;utente soddisfa effettivamente tutti i criteri richiesti per la riproduzione.

*`License preview`* si riferisce alla capacità del cliente di visualizzare l&#39;anteprima della licenza (per vedere quali diritti la licenza consente), invece di visualizzare l&#39;anteprima del contenuto (visualizzare una piccola parte del contenuto prima di decidere di acquistare). Alcuni dei parametri univoci per ogni computer sono: output disponibili e relativo stato di protezione, versione runtime/DRM disponibile e livello di protezione client DRM. La modalità di anteprima della licenza consente al client runtime/DRM di verificare la logica aziendale del server licenze e fornire informazioni all&#39;utente in modo che possa prendere una decisione informata. In questo modo il cliente può vedere l&#39;aspetto di una licenza valida, ma non riceve la chiave per decifrare il contenuto. Il supporto per l&#39;anteprima della licenza è facoltativo e necessario solo se implementate un client personalizzato che utilizza questa funzionalità.

Per determinare se il client ha inviato una richiesta di anteprima o una richiesta di acquisizione della licenza, chiamatela `LicenseRequestMessage.getRequestPhase()`e confrontalo con `LicenseRequestMessage.RequestPhase.Acquire`
