---
title: Archiviazione sicura dei criteri
description: Archiviazione sicura dei criteri
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---


# Memorizzazione sicura dei criteri{#securely-storing-policies}

Adobe Access SDK offre una grande flessibilità nello sviluppo di applicazioni da utilizzare nei pacchetti di contenuti e nella creazione di regole. Quando crei tali applicazioni, puoi consentire ad alcuni utenti di creare e modificare i criteri e limitare altri utenti in modo che possano applicare i criteri esistenti solo al contenuto. In questo caso, è necessario implementare i controlli di accesso necessari per creare account utente con privilegi diversi per la creazione dei criteri e l&#39;applicazione dei criteri al contenuto.

Le politiche non sono firmate o altrimenti protette dalla modifica finché non vengono utilizzate in imballaggi. Se sei preoccupato per gli utenti dei tuoi strumenti di imballaggio che modificano i criteri, dovresti considerare la possibilità di firmare i criteri in modo che non possano essere modificati.

Per ulteriori informazioni sulla creazione di applicazioni utilizzando l&#39;SDK, consulta la sezione *Guida di riferimento dell&#39;API di accesso agli Adobi*.
