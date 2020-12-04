---
description: 'null'
seo-description: 'null'
seo-title: Regole aziendali dimostrative del modello di utilizzo
title: Regole aziendali dimostrative del modello di utilizzo
uuid: c55f85be-5ecb-4a78-b47d-7001ec207d3a
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# Regole aziendali demo modello di utilizzo{#usage-model-demo-business-rules}

Quando un utente richiede una licenza, il server di implementazione di riferimento verifica i metadati inviati dal client, per determinare se il contenuto è stato incluso nel pacchetto utilizzando la proprietà `RI_UsageModelDemo`. In questo caso, il server applica le seguenti regole aziendali.

* Se uno dei criteri DRM richiede l&#39;autenticazione:

   * Se la richiesta contiene un token di autenticazione valido, cercate il nome dell&#39;utente nella tabella del database del cliente.

      Se non riuscite a individuare il nome dell’utente, effettuate le seguenti operazioni:

      * Se la proprietà `Customer.IsSubscriber` è impostata su `true`, è necessario generare una licenza per il modello di utilizzo *`Subscription`* e inviarla all&#39;utente.

      * Cercare nella tabella di database `CustomerAuthorization` un record per il nome dell&#39;utente e l&#39;ID del contenuto.

      Se è possibile individuare il record dell&#39;utente, completare le seguenti attività:

      * Se la proprietà `CustomerAuthorization.UsageType` è impostata su `DTO`, genera una licenza per il modello di utilizzo DTO e la invia all&#39;utente.

      * Se la proprietà `CustomerAuthorization.UsageType` è impostata su `VOD`, generare una licenza per il modello di utilizzo VOD e inviarla all&#39;utente.

      Se nessuna delle policy DRM consente l&#39;accesso anonimo, completare le seguenti attività:

      * Se nella richiesta non è presente un token di autenticazione valido, è necessario restituire un errore di autenticazione richiesta.
      * In caso contrario, viene restituito un errore &quot;non autorizzato&quot;.



* Se uno dei criteri DRM consente l&#39;accesso anonimo, genera una licenza per il modello di utilizzo finanziato tramite Ad e la invia all&#39;utente.

