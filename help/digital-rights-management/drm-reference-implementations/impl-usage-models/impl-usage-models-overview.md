---
title: Panoramica
description: Panoramica
copied-description: true
exl-id: 974b9a5e-43f6-4ec8-8048-dfcc1cff0f6f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Panoramica{#overview}

L’implementazione di riferimento include un’opzione in modalità demo che illustra come implementare diversi modelli di utilizzo per un segmento di contenuto collocato. La modalità demo presenta la logica di business per questi modelli di utilizzo:

* **Download-To-Own (DTO)** - Gli utenti possono scaricare il contenuto online o offline e ricevono una licenza permanente per il contenuto.
* **Noleggio/Video on demand (VOD)** - I contenuti disponibili sono soggetti a restrizioni temporali. Ad esempio, gli utenti possono riprodurre i contenuti durante un periodo di 30 giorni. Una volta avviata la riproduzione, l’utente dispone di un massimo di 48 ore per terminare la visualizzazione del contenuto. Il contenuto deve essere visualizzato in 30 giorni.
* **Abbonamento (tutto ciò che puoi mangiare)** - Alcuni servizi offrono abbonamenti a pagamento che consentono agli utenti di accedere illimitatamente a un&#39;ampia raccolta di contenuti, a condizione che continuino a pagare una tariffa mensile. Il server licenze rilascia una licenza univoca per ciascun segmento di contenuto e una licenza radice che scade alla fine del periodo di abbonamento. Ogni mese, quando gli utenti rinnovano l’abbonamento, è necessario rinnovare anche la licenza root.

   >[!NOTE]
   >
   >Per i modelli di utilizzo precedenti, dopo l&#39;acquisizione di una licenza, gli utenti devono immettere le credenziali in modo che il server possa verificare che gli utenti dispongano di un account di noleggio.

* **Finanziato da annunci** - Il contenuto viene monetizzato includendo la pubblicità come parte dell’esperienza. Con questo modello, il contenuto può essere distribuito e non richiede l’autenticazione dell’utente.

In modalità demo del modello di utilizzo, la logica di business sul server controlla gli attributi per le licenze generate. Al momento della creazione del pacchetto, i criteri DRM devono solo indicare se è richiesta o meno l&#39;autenticazione.

Per abilitare tutti e quattro i modelli di utilizzo, è necessario includere solo due criteri DRM:

* Un criterio DRM che consente l’accesso anonimo per il modello finanziato dall’annuncio
* Un criterio DRM che richiede l&#39;autenticazione nome utente/password per gli altri tre modelli di utilizzo.

Quando un utente richiede una licenza, un&#39;applicazione client può determinare se richiedere all&#39;utente l&#39;autenticazione in base alle informazioni di autenticazione contenute nei criteri DRM.
