---
description: Adobe ® Access™ è una soluzione avanzata per la gestione dei diritti digitali e la protezione dei contenuti audiovisivi di alto valore. Utilizzando gli strumenti creati con le API Java, puoi creare policy, applicare policy a file contenenti contenuti audio e video e crittografare tali file. I passaggi di alto livello per eseguire queste attività sono i seguenti
title: Panoramica
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# Panoramica {#overview}

Adobe ® Access™ è una soluzione avanzata per la gestione dei diritti digitali e la protezione dei contenuti audiovisivi di alto valore. Utilizzando gli strumenti creati con le API Java, puoi creare policy, applicare policy a file contenenti contenuti audio e video e crittografare tali file. I passaggi di alto livello per eseguire queste attività sono i seguenti:

1. Utilizza le API Java per impostare le proprietà dei criteri e i parametri di crittografia.
1. Crea un criterio che descriva i ruoli di utilizzo per il contenuto. (vedere [Utilizzo dei criteri](../../aaxs-protecting-content/content-working-with-policies/content-working-with-policies-overview.md)).

   Puoi creare un numero qualsiasi di criteri. La maggior parte degli utenti crea un numero limitato di policy e le applica a molti file.

1. Creare un pacchetto di un file multimediale.

   In questo contesto: *creazione di pacchetti di un file* significa crittografarlo e applicarvi una policy. (vedere [Creazione di pacchetti di file multimediali](../../aaxs-protecting-content/content-packaging-media-files/content-packaging-media-files-overview.md).)

1. Implementare il server licenze per rilasciare una licenza all&#39;utente.

Il contenuto crittografato è ora pronto per la distribuzione e il client può richiedere la licenza al server.

L’SDK fornisce un’API Java per eseguire queste attività e include implementazioni di riferimento del server licenze e strumenti per riga di comando basati sulle API Java. Per informazioni, consulta *Utilizzo delle implementazioni di riferimento di accesso Adobe*.

## Novità di Adobe Access 5.2 {#section_06220EDE36B54DCB9CA7963B76DA8167}

* **CEK esterno**: possibilità di integrare un sistema di gestione delle chiavi di contenuto (CKMS) nei flussi di lavoro di gestione delle licenze DRM e di creazione dei pacchetti di contenuti, invece di crittografare il CEK e raggrupparlo nei metadati del contenuto. Consulta [Panoramica sul controllo esterno DRM di accesso Adobe](../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md).

* **Restituzione licenza (voucher)**: possibilità per un client di restituire (o eliminare) una licenza rilasciata al client.
* **Server chiave Xbox**: possibilità di proteggere il contenuto inviato a Xbox e Xbox 360. (È necessario un client Adobe Primetime).

## Regole di utilizzo personalizzate {#custom-usage-rules}

Specifica le regole di utilizzo personalizzate. I dati personalizzati possono essere inclusi nelle licenze rilasciate dal server licenze. L&#39;interpretazione/gestione di questi dati dipende interamente dall&#39;implementazione dell&#39;applicazione client e del server licenze.

Caso d’uso di esempio: abilita l’estensibilità delle regole di utilizzo consentendo ad altre regole aziendali di essere trasmesse in modo sicuro come parte della licenza della policy e/o del contenuto. Per motivi di sicurezza, poiché queste regole di utilizzo vengono applicate nel codice dell’applicazione client personalizzata, questa opzione deve essere utilizzata insieme alle opzioni di elenco consentiti dell’applicazione AIR o di Flash Player SWF. Per ulteriori informazioni, consulta [Restrizioni per runtime e applicazioni](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-allowlist-air.md).
