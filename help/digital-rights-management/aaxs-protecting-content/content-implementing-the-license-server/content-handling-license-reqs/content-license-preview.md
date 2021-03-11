---
title: Anteprima della licenza
description: Anteprima della licenza
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---


# Anteprima licenza{#license-preview}

Il client può inviare una richiesta di anteprima della licenza, il che significa che l&#39;applicazione può eseguire un&#39;operazione di anteprima prima di chiedere all&#39;utente di acquistare il contenuto per determinare se il computer dell&#39;utente soddisfa effettivamente tutti i criteri necessari per la riproduzione. *L’* anteprima della licenza si riferisce alla capacità del cliente di visualizzare l’anteprima della licenza (per vedere quali diritti consente la licenza) invece di visualizzare l’anteprima del contenuto (visualizzare una piccola parte del contenuto prima di decidere di acquistare). Alcuni dei parametri univoci per ogni computer sono: le uscite disponibili e il loro stato di protezione, la versione runtime/DRM disponibile e il livello di sicurezza client DRM. La modalità di anteprima della licenza consente al client runtime/DRM di verificare la logica di business del server licenze e fornire informazioni all’utente in modo che possa prendere una decisione informata. Così il cliente può vedere come si presenta una licenza valida ma non riceverà effettivamente la chiave per decrittografare il contenuto. Il supporto per l’anteprima della licenza è facoltativo e necessario solo se si implementa un client personalizzato che utilizza questa funzionalità.

Per determinare se il client ha inviato una richiesta di anteprima o una richiesta di acquisizione di licenza, chiamare `LicenseRequestMessage.getRequestPhase()`e confrontarla con `LicenseRequestMessage.RequestPhase.Acquire`
