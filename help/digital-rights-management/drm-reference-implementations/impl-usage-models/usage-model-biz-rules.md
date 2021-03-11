---
title: Regole aziendali dimostrative del modello di utilizzo
description: Regole aziendali dimostrative del modello di utilizzo
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---


# Regole aziendali dimostrative del modello di utilizzo{#usage-model-demo-business-rules}

Quando un utente richiede una licenza, il server di implementazione di riferimento controlla i metadati inviati dal client, per determinare se il contenuto è stato compilato utilizzando la proprietà `RI_UsageModelDemo` . In questo caso, il server applica le seguenti regole business.

* Se uno dei criteri DRM richiede l’autenticazione:

   * Se la richiesta contiene un token di autenticazione valido, cercare il nome dell&#39;utente nella tabella del database del cliente.

      Se non è possibile individuare il nome dell&#39;utente, eseguire le operazioni seguenti:

      * Se la proprietà `Customer.IsSubscriber` è impostata su `true`, è necessario generare una licenza per il modello di utilizzo *`Subscription`* e inviarla all&#39;utente.

      * Cerca un record nella tabella di database `CustomerAuthorization` per il nome dell&#39;utente e l&#39;ID del contenuto.

      Se è possibile individuare il record dell&#39;utente, completare le seguenti attività:

      * Se la proprietà `CustomerAuthorization.UsageType` è impostata su `DTO`, genera una licenza per il modello di utilizzo DTO e inviala all’utente.

      * Se la proprietà `CustomerAuthorization.UsageType` è impostata su `VOD`, genera una licenza per il modello di utilizzo VOD e inviala all’utente.

      Se nessuno dei criteri DRM consente l&#39;accesso anonimo, completa le seguenti attività:

      * Se nella richiesta non è presente un token di autenticazione valido, devi restituire un errore di autenticazione richiesta.
      * In caso contrario, restituisce un errore &quot;non autorizzato&quot;.



* Se uno dei criteri DRM consente l&#39;accesso anonimo, genera una licenza per il modello di utilizzo finanziato dall&#39;Ad e la invia all&#39;utente.

