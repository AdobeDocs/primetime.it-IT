---
title: Aggiorna il database di implementazione di riferimento
description: Aggiorna il database di implementazione di riferimento
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# Aggiorna l&#39;implementazione di riferimento DB{#update-the-reference-implementation-db}

Per controllare i modelli di utilizzo in base ai quali viene rilasciata una licenza a un utente designato, aggiungere voci al database di implementazione di riferimento.

1. Aggiungi le voci alla tabella `Customer`.

   La tabella `Customer` include nomi utente e password per l&#39;autenticazione degli utenti. Indica inoltre se un utente dispone di un abbonamento (una licenza rilasciata sotto il modello di utilizzo *Abbonamento*).

1. Concedi a un utente l&#39;accesso ai modelli di utilizzo Download-to-own o Video-on-demand.

       Aggiungi le voci alla tabella &quot;CustomerAuthorization&quot; per specificare:
   
   * Il modello di utilizzo
   * Ogni segmento di contenuto a cui un utente può accedere

Per ulteriori informazioni su come compilare ogni tabella, vedere lo script [!DNL PopulateSampleDB.sql] (incluso nel DVD DRM Primetime nel [!DNL Reference Implementation/Server/Reference Implementation Server/dbscript/] directory).
