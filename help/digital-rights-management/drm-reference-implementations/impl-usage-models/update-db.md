---
title: Aggiornare il database di implementazione di riferimento
description: Aggiornare il database di implementazione di riferimento
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# Aggiornare il database di implementazione di riferimento{#update-the-reference-implementation-db}

Per controllare i modelli di utilizzo in base ai quali viene rilasciata una licenza a un utente designato, aggiungere voci al database di implementazione di riferimento.

1. Aggiungi voci al `Customer` tabella.

   Il `Customer` La tabella include nomi utente e password per l&#39;autenticazione degli utenti. Indica inoltre se un utente dispone di un abbonamento (una licenza rilasciata in base al *Abbonamento* modello di utilizzo).

1. Concedi a un utente l’accesso secondo i modelli di utilizzo Download-to-own o Video-on-demand.

       Aggiungi voci alla tabella &quot;CustomerAuthorization&quot; per specificare:
   
   * Modello di utilizzo
   * Ogni segmento di contenuto a cui un utente può accedere

Per ulteriori informazioni su come compilare ogni tabella, vedere [!DNL PopulateSampleDB.sql] (incluso nel DVD DRM Primetime nel [!DNL Reference Implementation/Server/Reference Implementation Server/dbscript/] directory).
