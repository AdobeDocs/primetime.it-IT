---
title: Elenco consentiti per le applicazioni DRM Primetime autorizzate a riprodurre contenuti protetti
description: Elenco consentiti per le applicazioni DRM Primetime autorizzate a riprodurre contenuti protetti
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# Elenco consentiti per le applicazioni DRM Primetime autorizzate a riprodurre contenuti protetti {#allowlist-for-primetime-drm-applications-allowed-to-play-protected-content}

Un elenco consentiti specifica le applicazioni AIR, iOS e Android autorizzate a riprodurre il contenuto. Specifica inoltre gli ID applicazione AIR e iOS, la versione minima, la versione massima e l’ID dell’editore.

Caso d’uso di esempio: utilizza questa regola per limitare la riproduzione a una particolare applicazione o per controllare la versione dell’applicazione che può accedere al contenuto.

>[!NOTE]
>
>Se si utilizza Adobe Flash Builder per creare applicazioni protette, è necessario assicurarsi di non distribuire l&#39;applicazione in modalità di debug. Quando si distribuisce un&#39;applicazione in modalità di debug, il Flash Builder aggiunge `.debug` all’ID dell’applicazione AIR, che determina un comportamento imprevisto della funzionalità di elenco consentiti in Primetime DRM.
