---
description: 'Adobe® Access™ è una soluzione avanzata per la gestione dei diritti digitali e la protezione dei contenuti per contenuti audiovisivi di alto valore. Utilizzando gli strumenti creati tramite le API Java, puoi creare criteri, applicare criteri ai file contenenti contenuto audio e video e cifrare tali file. I passaggi di alto livello per l''esecuzione di queste attività sono i seguenti: '
title: Panoramica
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---


# Panoramica {#overview}

Adobe® Access™ è una soluzione avanzata per la gestione dei diritti digitali e la protezione dei contenuti per contenuti audiovisivi di alto valore. Utilizzando gli strumenti creati tramite le API Java, puoi creare criteri, applicare criteri ai file contenenti contenuto audio e video e cifrare tali file. I passaggi di alto livello per l&#39;esecuzione di queste attività sono i seguenti:

1. Utilizza le API Java per impostare le proprietà dei criteri e i parametri di crittografia.
1. Crea un criterio che descrive i ruoli di utilizzo per il contenuto. (Vedere [Uso dei criteri](../../aaxs-protecting-content/content-working-with-policies/content-working-with-policies-overview.md)).

   È possibile creare un numero qualsiasi di criteri. La maggior parte degli utenti crea un numero limitato di criteri e li applica a molti file.

1. Creare un pacchetto di un file multimediale.

   In questo contesto, *creare un pacchetto per un file* significa cifrarlo e applicarvi un criterio. (Consultare [Creazione di pacchetti di file multimediali](../../aaxs-protecting-content/content-packaging-media-files/content-packaging-media-files-overview.md).)

1. Implementa il server licenze per rilasciare una licenza all&#39;utente.

Il contenuto crittografato è ora pronto per la distribuzione e il client può richiedere la licenza dal server.

L’SDK fornisce un’API Java per eseguire queste attività e include implementazioni di riferimento del server licenze e strumenti della riga di comando basati sulle API Java. Per informazioni, consulta *Utilizzo delle implementazioni di riferimento di accesso Adobe*.

## Novità di Adobe Access 5.2 {#section_06220EDE36B54DCB9CA7963B76DA8167}

* **CEK** esterno: La possibilità di integrare un sistema di gestione delle chiavi di contenuto (CKMS) nei flussi di lavoro di gestione delle licenze DRM e di creazione dei pacchetti di contenuti, invece di crittografare il CEK e incorporarlo nei metadati del contenuto. Consulta [Panoramica sull&#39;accesso Adobe a DRM External CEK](../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md).

* **Licenza (voucher) Ritorno**: La possibilità per un cliente di restituire (o cancellare) una licenza rilasciata al cliente.
* **Server** chiavi Xbox: Possibilità di proteggere i contenuti inviati a Xbox e Xbox 360. È necessario un client Adobe Primetime.

## Regole di utilizzo personalizzate {#custom-usage-rules}

Specifica le regole di utilizzo personalizzate. I dati personalizzati possono essere inclusi nelle licenze rilasciate dal server licenze. L&#39;interpretazione/gestione di questi dati è completamente all&#39;altezza dell&#39;implementazione dell&#39;applicazione client e del server licenze.

Esempio di utilizzo: Consente l’estensibilità delle regole di utilizzo consentendo ad altre regole business di essere trasmesse in modo sicuro come parte dei criteri e/o della licenza di contenuto. Per motivi di sicurezza, poiché queste regole di utilizzo sono applicate nel codice personalizzato dell’applicazione client, questa opzione deve essere utilizzata insieme alle opzioni dell’applicazione AIR o dell’elenco consentiti Flash Player SWF. Per ulteriori informazioni, vedere [Restrizioni per runtime e applicazioni](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-allowlist-air.md).
