---
description: Adobe Primetime DRM è una soluzione avanzata di protezione dei contenuti e dei Digital Rights Management per contenuti audiovisivi di alto valore. Nelle applicazioni che supportano la creazione di API Java, puoi utilizzare l’SDK DRM di Primetime per specificare i criteri DRM, applicarli al contenuto e cifrarli.
title: Novità in Adobe Primetime DRM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---


# Novità in Adobe Primetime DRM{#what-is-new-in-adobe-primetime-drm}

Adobe Primetime DRM è una soluzione avanzata di protezione dei contenuti e dei Digital Rights Management per contenuti audiovisivi di alto valore. Nelle applicazioni che supportano la creazione di API Java, puoi utilizzare l’SDK DRM di Primetime per specificare i criteri DRM, applicarli al contenuto e cifrarli.

>[!NOTE]
>
>Primetime DRM era precedentemente denominato Adobe Access e prima di tale Flash Access.

Di seguito è riportata una panoramica dettagliata del processo di protezione dei contenuti:

1. Utilizza le API Java DRM per impostare le proprietà dei criteri DRM e i parametri di crittografia.
1. Crea un criterio DRM che descrive i ruoli di utilizzo per qualsiasi contenuto.

   Puoi creare un numero qualsiasi di criteri DRM. La maggior parte degli utenti crea un numero limitato di criteri e quindi li applica a molti file.
1. Creare un pacchetto di un file multimediale.

   *`Packaging a file`* significa che devi crittografare il file e quindi applicare al file un criterio DRM.
1. Implementa il server licenze per rilasciare una licenza all&#39;utente.

Al completamento di questi passaggi, il contenuto crittografato è pronto per la distribuzione. Dopo la distribuzione, un client può richiedere una licenza dal server licenze e, una volta ricevuta, può riprodurre il contenuto.

L’SDK DRM di Primetime fornisce un’API Java per completare queste attività. L’SDK include implementazioni di riferimento del server di licenza e degli strumenti della riga di comando, entrambi basati sulle API Java SDK DRM.

Le funzioni descritte di seguito sono nuove in questa versione.

## Nuove funzioni {#section_F6BA874CEAE24610920BC3A4C6D20EBA}

* **Arresto rigido:** è possibile specificare se la riproduzione si arresta o continua alla fine di una finestra di riproduzione.
* **Controlli di output dipendenti dalla risoluzione:** è possibile specificare i vincoli di output in base alle risoluzioni dei pixel.
* **Anonimizzazione delle risposte del server licenze -** Per migliorare la privacy con i protocolli del server licenze DRM di Primetime, il numero di serie del certificato di trasporto verrà azzerato per le risposte del server licenze ai client di supporto.

