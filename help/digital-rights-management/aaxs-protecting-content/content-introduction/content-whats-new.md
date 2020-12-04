---
description: ' Adobe® Access™ è una soluzione avanzata per la gestione dei diritti digitali e la protezione dei contenuti per contenuti audiovisivi di alto valore. Utilizzando gli strumenti creati mediante le API Java, potete creare criteri, applicare criteri ai file contenenti contenuto audio e video e cifrare tali file. I passaggi ad alto livello per l''esecuzione di tali attività sono i seguenti: '
seo-description: ' Adobe® Access™ è una soluzione avanzata per la gestione dei diritti digitali e la protezione dei contenuti per contenuti audiovisivi di alto valore. Utilizzando gli strumenti creati mediante le API Java, potete creare criteri, applicare criteri ai file contenenti contenuto audio e video e cifrare tali file. I passaggi ad alto livello per l''esecuzione di tali attività sono i seguenti: '
seo-title: Panoramica
title: Panoramica
uuid: 874c175b-8207-49fa-aad4-204ccbee9c2c
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---


# Panoramica {#overview}

 Adobe® Access™ è una soluzione avanzata per la gestione dei diritti digitali e la protezione dei contenuti per contenuti audiovisivi di alto valore. Utilizzando gli strumenti creati mediante le API Java, potete creare criteri, applicare criteri ai file contenenti contenuto audio e video e cifrare tali file. I passaggi di alto livello per l&#39;esecuzione di tali attività sono i seguenti:

1. Utilizzate le API Java per impostare le proprietà del criterio e i parametri di cifratura.
1. Create un criterio che descriva i ruoli di utilizzo per il contenuto. (Vedere [Utilizzo dei criteri](../../aaxs-protecting-content/content-working-with-policies/content-working-with-policies-overview.md)).

   Potete creare un numero qualsiasi di criteri. La maggior parte degli utenti crea un numero limitato di criteri e li applica a molti file.

1. Creare pacchetti di un file multimediale.

   In questo contesto, la *creazione di pacchetti per un file* significa cifrarlo e applicarvi un criterio. (Vedere [Creazione di pacchetti di file multimediali](../../aaxs-protecting-content/content-packaging-media-files/content-packaging-media-files-overview.md).)

1. Implementate il server licenze per rilasciare una licenza all&#39;utente.

Il contenuto crittografato è ora pronto per la distribuzione e il client può richiedere la licenza dal server.

L’SDK fornisce un’API Java per eseguire queste attività e include implementazioni di riferimento del server licenze e strumenti della riga di comando basati sulle API Java. Per informazioni, vedere *Utilizzo delle implementazioni di riferimento per l&#39;accesso al Adobe*.

## Novità in  Adobe Access 5.2 {#section_06220EDE36B54DCB9CA7963B76DA8167}

* **CEK** esterno: La capacità di integrare un Content Key Management System (CKMS) nei flussi di lavoro di gestione delle licenze DRM e di creazione di pacchetti di contenuti, invece di cifrare il CEK e impacchettarlo nei metadati del contenuto. Vedere [ Accesso al Adobe DRM Panoramica CEK esterna](../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md).

* **Licenza (voucher) Ritorno**: Possibilità per un cliente di restituire (o eliminare) una licenza rilasciata al client.
* **Server** chiavi Xbox: Possibilità di proteggere i contenuti inviati a Xbox e Xbox 360. (È necessario un client Adobe Primetime .)

## Regole di utilizzo personalizzate {#custom-usage-rules}

Specifica le regole di utilizzo personalizzate. I dati personalizzati possono essere inclusi nelle licenze rilasciate dal server licenze. L&#39;interpretazione/gestione di questi dati è completamente all&#39;implementazione dell&#39;applicazione client e del server licenze.

Esempio di utilizzo: Consente l&#39;estensibilità delle regole di utilizzo consentendo ad altre regole aziendali di essere trasmesse in modo sicuro come parte del criterio e/o della licenza di contenuto. Per motivi di sicurezza, poiché queste regole di utilizzo sono applicate nel codice dell&#39;applicazione client personalizzato, questa opzione deve essere utilizzata insieme alle opzioni dell&#39;applicazione AIR o del elenco consentiti di Flash Player SWF  AIR. Per ulteriori informazioni, vedere [Limitazioni di runtime e applicazione](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-allowlist-air.md).
