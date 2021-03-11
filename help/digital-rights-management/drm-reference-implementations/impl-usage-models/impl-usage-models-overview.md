---
title: Panoramica
description: Panoramica
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---


# Panoramica{#overview}

L’implementazione di riferimento include un’opzione di modalità demo che dimostra come implementare diversi modelli di utilizzo per un segmento di contenuto in pacchetto. La modalità demo presenta la logica di business per questi modelli di utilizzo:

* **Download-To-own (DTO)**  - Gli utenti possono scaricare il contenuto online o offline e ricevono una licenza permanente per il contenuto.
* **Noleggio/Video-On-Demand (VOD)**  - I contenuti disponibili sono soggetti a restrizioni basate sul tempo. Ad esempio, gli utenti possono riprodurre contenuti per un periodo di 30 giorni. Una volta avviata la riproduzione, l&#39;utente ha fino a 48 ore per terminare la visione del contenuto. Il contenuto deve essere visualizzato in 30 giorni.
* **Abbonamento (all-you-can-eat)**  - Alcuni servizi offrono abbonamenti a pagamento che danno agli utenti accesso illimitato a una grande libreria di contenuti fino a quando continuano a pagare una tariffa mensile. Il server licenze rilascia una licenza univoca per ogni segmento di contenuto e rilascia anche una licenza radice che scade alla fine del periodo di abbonamento. Ogni mese, quando gli utenti rinnovano il loro abbonamento, anche la licenza radice deve essere rinnovata.

   >[!NOTE]
   >
   >Per i modelli di utilizzo precedenti, dopo aver acquisito una licenza, gli utenti devono immettere le proprie credenziali in modo che il server possa verificare che gli utenti abbiano un account di noleggio.

* **Finanziato con**  annunci: i contenuti vengono monetizzati includendo la pubblicità come parte dell&#39;esperienza. Con questo modello, il contenuto può essere distribuito e non richiede l’autenticazione dell’utente.

In modalità demo modello di utilizzo, la logica di business sul server controlla gli attributi per le licenze generate. Al momento del packaging la politica DRM deve solo indicare se è necessaria o meno l&#39;autenticazione.

Per abilitare tutti e quattro i modelli di utilizzo, è sufficiente includere due criteri DRM:

* Una politica DRM che consente l&#39;accesso anonimo per il modello finanziato dall&#39;Ad
* Un criterio DRM che richiede l’autenticazione nome utente/password per gli altri tre modelli di utilizzo.

Quando un utente richiede una licenza, un&#39;applicazione client può determinare se richiedere all&#39;utente l&#39;autenticazione in base alle informazioni di autenticazione contenute nei criteri DRM.
