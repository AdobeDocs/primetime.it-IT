---
title: Anteprima licenza
description: Anteprima licenza
copied-description: true
exl-id: 283ee661-b1ee-46b9-9337-0497c97bd785
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---

# Anteprima licenza{#license-preview}

Il client può inviare una richiesta di anteprima della licenza, il che significa che l’applicazione può eseguire un’operazione di anteprima prima di chiedere all’utente di acquistare il contenuto per determinare se il computer dell’utente soddisfa effettivamente tutti i criteri richiesti per la riproduzione. *Anteprima licenza* si riferisce alla capacità del cliente di visualizzare in anteprima la licenza (per vedere quali diritti la licenza consente) rispetto all’anteprima del contenuto (visualizzare una piccola parte del contenuto prima di decidere di acquistare). Alcuni dei parametri univoci di ogni computer sono: gli output disponibili e il relativo stato di protezione, la versione di runtime/DRM disponibile e il livello di protezione del client DRM. La modalità di anteprima della licenza consente al client runtime/DRM di testare la logica di business del server licenze e di fornire informazioni all&#39;utente in modo che possa prendere una decisione informata. In questo modo il client può vedere come si presenta una licenza valida ma non riceverebbe la chiave per decrittografare il contenuto. Il supporto per l’anteprima della licenza è facoltativo e necessario solo se si implementa un client personalizzato che utilizza questa funzionalità.

Per determinare se il client ha inviato una richiesta di anteprima o una richiesta di acquisizione licenza, chiama `LicenseRequestMessage.getRequestPhase()`e confrontarlo con `LicenseRequestMessage.RequestPhase.Acquire`
