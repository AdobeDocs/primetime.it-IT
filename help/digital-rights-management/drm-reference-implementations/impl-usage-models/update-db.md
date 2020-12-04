---
seo-title: Aggiornare il database di implementazione di riferimento
title: Aggiornare il database di implementazione di riferimento
uuid: 2883045e-ad62-466d-94a2-fc45ded2a4f5
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# Aggiornare l&#39;implementazione di riferimento DB{#update-the-reference-implementation-db}

Per controllare i modelli di utilizzo in base ai quali una licenza viene rilasciata a un utente designato, aggiungere voci al database di implementazione di riferimento.

1. Aggiungere voci alla tabella `Customer`.

   La tabella `Customer` include nomi utente e password per l&#39;autenticazione degli utenti. Indica inoltre se un utente dispone di un&#39;iscrizione (una licenza rilasciata in base al modello di utilizzo *Subscription*).

1. Concedi a un utente l’accesso tramite i modelli di utilizzo Download-to-own o Video-on-demand.

       Aggiungere voci alla tabella &quot;CustomerAuthorization&quot; per specificare:
   
   * Il modello di utilizzo
   * Ciascun segmento di contenuto a cui un utente può accedere

Per ulteriori informazioni su come compilare ciascuna tabella, vedere lo script [!DNL PopulateSampleDB.sql] (incluso nel DVD DRM Primetime nella directory [!DNL Reference Implementation/Server/Reference Implementation Server/dbscript/]).
