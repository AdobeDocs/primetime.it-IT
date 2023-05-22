---
description: Adobe Primetime DRM è una soluzione di protezione dei contenuti e del Digital Rights Management avanzato (DRM) per contenuti audiovisivi di alto valore. Nelle applicazioni che supportano la creazione di API Java, puoi utilizzare l’SDK DRM di Primetime per specificare i criteri DRM, applicarli al contenuto e crittografare tale contenuto.
title: Novità di Adobe Primetime DRM
exl-id: 998dae80-b3d3-419e-8fd3-d925a83d8b53
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# Novità di Adobe Primetime DRM{#what-is-new-in-adobe-primetime-drm}

Adobe Primetime DRM è una soluzione di protezione dei contenuti e del Digital Rights Management avanzato (DRM) per contenuti audiovisivi di alto valore. Nelle applicazioni che supportano la creazione di API Java, puoi utilizzare l’SDK DRM di Primetime per specificare i criteri DRM, applicarli al contenuto e crittografare tale contenuto.

>[!NOTE]
>
>In precedenza, Primetime DRM era chiamato Adobe Access e prima di questo, Flash Access.

Di seguito è riportata una descrizione dettagliata del processo di protezione dei contenuti:

1. Utilizzare le API Java DRM per impostare le proprietà dei criteri DRM e i parametri di crittografia.
1. Creare un criterio DRM che descriva i ruoli di utilizzo per qualsiasi contenuto.

   È possibile creare un numero qualsiasi di criteri DRM. La maggior parte degli utenti crea un numero limitato di criteri e quindi li applica a molti file.
1. Creare un pacchetto di un file multimediale.

   *`Packaging a file`* significa che si crittografa il file e quindi si applica una policy DRM al file.
1. Implementare il server licenze per rilasciare una licenza all&#39;utente.

Una volta completati questi passaggi, il contenuto crittografato sarà pronto per l’implementazione. Dopo la distribuzione, un client può richiedere una licenza al server licenze e, una volta ricevuto, può riprodurre il contenuto.

L’SDK DRM di Primetime fornisce un’API Java per completare queste attività. L’SDK include implementazioni di riferimento del server licenze e strumenti per riga di comando, entrambi basati sulle API Java dell’SDK DRM.

In questa versione sono state introdotte nuove funzioni descritte di seguito.

## Nuove funzioni {#section_F6BA874CEAE24610920BC3A4C6D20EBA}

* **Hard stop -** È possibile specificare se la riproduzione si arresta o continua alla fine di una finestra di riproduzione.
* **Controlli dell&#39;uscita dipendenti dalla risoluzione -** Potete specificare i vincoli di output in base alle risoluzioni dei pixel.
* **Anonimizzazione delle risposte del server licenze -** Per migliorare la privacy con i protocolli del server licenze DRM Primetime, il numero di serie del certificato di trasporto verrà azzerato per le risposte del server licenze ai client di supporto.
