---
title: Elenco consentiti per le applicazioni DRM di Primetime che possono riprodurre contenuti protetti
description: Elenco consentiti per le applicazioni DRM di Primetime che possono riprodurre contenuti protetti
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# Elenco consentiti per le applicazioni DRM di Primetime che possono riprodurre contenuti protetti {#allowlist-for-primetime-drm-applications-allowed-to-play-protected-content}

Un elenco consentiti specifica le applicazioni AIR, iOS e Android che possono riprodurre contenuti. Specifica inoltre ID applicazione AIR e iOS, versione minima, versione massima e ID editore.

Esempio di utilizzo: Utilizzare questa regola per limitare la riproduzione a una particolare applicazione o per controllare la versione dell&#39;applicazione che può accedere al contenuto.

>[!NOTE]
>
>Se si utilizza Adobe Flash Builder per creare applicazioni protette, è necessario assicurarsi di non distribuire l&#39;applicazione in modalità Debug. Quando distribuisci un&#39;applicazione in modalità Debug, il Flash Builder aggiunge `.debug` all&#39;ID dell&#39;applicazione AIR, il che causa il funzionamento imprevisto della funzionalità elenco consentiti in DRM di Primetime.
