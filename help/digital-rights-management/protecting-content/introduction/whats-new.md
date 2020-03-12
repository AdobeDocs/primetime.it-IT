---
description: Adobe Primetime DRM è una soluzione avanzata per la gestione dei diritti digitali (DRM) e la protezione dei contenuti per contenuti audiovisivi di alto valore. Nelle applicazioni che supportano la creazione di API Java, potete utilizzare l'SDK DRM di Primetime per specificare i criteri DRM, applicare tali criteri al contenuto e cifrare tale contenuto.
seo-description: Adobe Primetime DRM è una soluzione avanzata per la gestione dei diritti digitali (DRM) e la protezione dei contenuti per contenuti audiovisivi di alto valore. Nelle applicazioni che supportano la creazione di API Java, potete utilizzare l'SDK DRM di Primetime per specificare i criteri DRM, applicare tali criteri al contenuto e cifrare tale contenuto.
seo-title: Novità in Adobe Primetime DRM
title: Novità in Adobe Primetime DRM
uuid: 3c8da594-a231-4496-bffc-130775ecae50
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Novità in Adobe Primetime DRM{#what-is-new-in-adobe-primetime-drm}

Adobe Primetime DRM è una soluzione avanzata per la gestione dei diritti digitali (DRM) e la protezione dei contenuti per contenuti audiovisivi di alto valore. Nelle applicazioni che supportano la creazione di API Java, potete utilizzare l&#39;SDK DRM di Primetime per specificare i criteri DRM, applicare tali criteri al contenuto e cifrare tale contenuto.

>[!NOTE]
>
>Primetime DRM era precedentemente denominato Adobe Access e prima di tale data, Flash Access.

Di seguito è riportata una panoramica dettagliata del processo di protezione dei contenuti:

1. Utilizzate le API Java DRM per impostare le proprietà dei criteri DRM e i parametri di crittografia.
1. Create un criterio DRM che descriva i ruoli di utilizzo per qualsiasi contenuto.

   Potete creare un numero qualsiasi di criteri DRM. La maggior parte degli utenti crea un numero limitato di criteri, quindi li applica a molti file.
1. Creare pacchetti di un file multimediale.

   *`Packaging a file`* significa che devi crittografare il file e quindi applicare un criterio DRM al file.
1. Implementate il server licenze per rilasciare una licenza all&#39;utente.

Con il completamento di questi passaggi, il contenuto crittografato è pronto per la distribuzione. Dopo la distribuzione, un client può richiedere una licenza dal server licenze e, dopo la ricezione, può riprodurre il contenuto.

L&#39;SDK DRM di Primetime fornisce un&#39;API Java per completare queste attività. L’SDK include implementazioni di riferimento del server licenze e degli strumenti della riga di comando, entrambi basati sulle API Java SDK DRM.

Le funzioni descritte di seguito sono nuove in questa versione.

## Nuove funzioni {#section_F6BA874CEAE24610920BC3A4C6D20EBA}

* **Arresto rigido -** È possibile specificare se la riproduzione si arresta o continua alla fine di una finestra di riproduzione.
* **Controlli di output dipendenti dalla risoluzione -** È possibile specificare vincoli di output in base alle risoluzioni dei pixel.
* **Anonimizzazione delle risposte del server licenze - Per migliorare la privacy con i protocolli del server licenze DRM di Primetime, il numero di serie del certificato di trasporto verrà azzerato per le risposte del server licenze ai client di supporto.**

