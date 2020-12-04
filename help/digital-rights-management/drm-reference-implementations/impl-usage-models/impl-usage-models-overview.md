---
description: 'null'
seo-description: 'null'
seo-title: Panoramica
title: Panoramica
uuid: 5f82f603-6e2d-4c9d-a49f-7b07f30a29e4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---


# Overview{#overview}

L&#39;implementazione di riferimento include un&#39;opzione della modalità demo che illustra come implementare diversi modelli di utilizzo per un segmento di contenuto incluso nel pacchetto. La modalità demo presenta la logica aziendale per i seguenti modelli di utilizzo:

* **Download-Da-sé (DTO)**  - Gli utenti possono scaricare il contenuto online o offline e ricevono una licenza permanente per il contenuto.
* **Noleggio/Video-On-Demand (VOD)**  - I contenuti disponibili sono soggetti a limitazioni temporali. Ad esempio, gli utenti possono riprodurre il contenuto per un periodo di 30 giorni. Dopo l&#39;inizio della riproduzione, l&#39;utente può visualizzare il contenuto fino a 48 ore. Il contenuto deve essere visualizzato entro 30 giorni.
* **Abbonamento (all-you-can-eat)**  - Alcuni servizi offrono abbonamenti a pagamento che danno agli utenti accesso illimitato a una vasta libreria di contenuti, purché continuino a pagare una tariffa mensile. Il server licenze rilascia una licenza univoca per ciascun segmento di contenuto e rilascia anche una licenza radice che scade alla fine del periodo di iscrizione. Ogni mese, quando gli utenti rinnovano l&#39;iscrizione, è necessario rinnovare anche la licenza radice.

   >[!NOTE]
   >
   >Per i modelli di utilizzo precedenti, dopo aver acquisito una licenza, gli utenti devono immettere le proprie credenziali in modo che il server possa verificare che gli utenti abbiano un account di noleggio.

* **Ad-funding**  - Il contenuto viene monetizzato includendo la pubblicità come parte dell&#39;esperienza. Con questo modello, il contenuto può essere distribuito e non richiede l&#39;autenticazione dell&#39;utente.

In modalità demo modello di utilizzo, la logica aziendale sul server controlla gli attributi per le licenze generate. Al momento della creazione del pacchetto, il criterio DRM deve indicare solo se è necessaria o meno l&#39;autenticazione.

Per abilitare tutti e quattro i modelli di utilizzo, è necessario includere solo due criteri DRM:

* Una politica DRM che consente l&#39;accesso anonimo per il modello Ad-funding
* Un criterio DRM che richiede l&#39;autenticazione nome utente/password per gli altri tre modelli di utilizzo.

Quando un utente richiede una licenza, un&#39;applicazione client può determinare se richiedere all&#39;utente l&#39;autenticazione in base alle informazioni di autenticazione contenute nei criteri DRM.
