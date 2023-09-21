---
title: Regole aziendali dimostrative del modello di utilizzo
description: Regole aziendali dimostrative del modello di utilizzo
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---

# Regole aziendali dimostrative del modello di utilizzo{#usage-model-demo-business-rules}

Quando un utente richiede una licenza, il server di implementazione di riferimento controlla i metadati inviati dal client per determinare se il contenuto è stato creato utilizzando `RI_UsageModelDemo` proprietà. In questo caso, il server applica le regole business seguenti.

* Se uno dei criteri DRM richiede l&#39;autenticazione:

   * Se la richiesta contiene un token di autenticazione valido, cerca il nome dell’utente nella tabella del database del cliente.

     Se non riesci a individuare il nome dell’utente, completa le seguenti attività:

      * Se il `Customer.IsSubscriber` proprietà impostata su `true`, è necessario generare una licenza per *`Subscription`* modello di utilizzo e inviarlo all&#39;utente.

      * Cercare un record in `CustomerAuthorization` tabella di database per il nome dell&#39;utente e l&#39;ID contenuto.

     Se è possibile individuare il record dell&#39;utente, completare le attività seguenti:

      * Se il `CustomerAuthorization.UsageType` proprietà impostata su `DTO`, genera una licenza per il modello di utilizzo DTO e la invia all&#39;utente.

      * Se il `CustomerAuthorization.UsageType` proprietà impostata su `VOD`, genera una licenza per il modello di utilizzo VOD e inviala all’utente.

     Se nessuno dei criteri DRM consente l&#39;accesso anonimo, completare le operazioni seguenti:

      * Se nella richiesta non è presente un token di autenticazione valido, è necessario restituire un errore di tipo &quot;autenticazione richiesta&quot;.
      * In caso contrario, viene restituito un errore &quot;non autorizzato&quot;.

* Se uno dei criteri DRM consente l’accesso anonimo, genera una licenza per il modello di utilizzo finanziato da Ad e inviala all’utente.
