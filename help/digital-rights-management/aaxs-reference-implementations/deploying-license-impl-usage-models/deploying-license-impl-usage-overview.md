---
seo-title: Panoramica sull’implementazione dei modelli di utilizzo
title: Panoramica sull’implementazione dei modelli di utilizzo
uuid: 1041bb84-9996-4284-b2a0-d6fc6d4b73d9
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---


# Panoramica sull’implementazione dei modelli di utilizzo {#implementing-the-usage-models-overview}

L’implementazione di riferimento include una logica aziendale che illustra come abilitare i seguenti quattro diversi modelli di utilizzo per un contenuto incluso nel pacchetto:

* Download-to-own (DTO)
* Affitto/Video-on-demand (VOD)
* Abbonamento (all-you-can-eat)
* Ad-funding

Per abilitare la demo del modello di utilizzo, specificate la proprietà personalizzata `RI_UsageModelDemo=true` al momento della creazione del pacchetto. Se state creando un pacchetto di contenuto mediante lo strumento della riga di comando Media Packager, specificate quanto segue:

```
    java -jar AdobeMediaPackager.jar source.flv dest.flv -k RI_UsageModelDemo=true
```

>[!NOTE]
>
>Se non si attiva la modalità demo opzionale al momento della creazione del pacchetto, il server licenze utilizza il criterio specificato al momento della creazione del pacchetto per rilasciare una licenza. Se sono stati specificati più criteri, il server licenze utilizza il primo criterio valido.

Nella demo, la business logic sul server controlla gli attributi effettivi delle licenze generate. Al momento della creazione del pacchetto, nel contenuto devono essere incluse solo informazioni minime sul criterio. Nello specifico, il criterio deve solo indicare se è necessaria l&#39;autenticazione per accedere al contenuto. Per abilitare tutti e quattro i modelli di utilizzo, includete un criterio che consenta l&#39;accesso anonimo (per il modello con finanziamento pubblicitario) e un criterio che richiede l&#39;autenticazione tramite nome utente/password (per gli altri 3 modelli di utilizzo). Quando si richiede una licenza, un&#39;applicazione client può determinare se richiedere all&#39;utente l&#39;autenticazione in base alle informazioni di autenticazione contenute nei criteri.

Per controllare il modello di utilizzo in base al quale un utente specifico deve ottenere una licenza, è possibile aggiungere delle voci al database di implementazione di riferimento. La `Customer` tabella contiene i nomi utente e le password per l&#39;autenticazione degli utenti. Indica inoltre se l’utente dispone di un’iscrizione. Agli utenti con iscrizioni verranno rilasciate licenze in base al modello di utilizzo *Iscrizione* . Per concedere a un utente l&#39;accesso in base ai modelli di utilizzo *Scarica su proprio* o *Video su richiesta* , è possibile aggiungere una voce alla `CustomerAuthorization` tabella, che specifica ogni contenuto a cui l&#39;utente può accedere e il modello di utilizzo. Per informazioni dettagliate sulla compilazione di ciascuna tabella, vedere [!DNL PopulateSampleDB.sql] lo script.

Quando un utente richiede una licenza, il server di implementazione di riferimento verifica i metadati inviati dal client per determinare se il contenuto è stato incluso nel pacchetto utilizzando la `RI_UsageModelDemo` proprietà. In tal caso, vengono utilizzate le seguenti regole aziendali:

* Se uno dei criteri richiede l&#39;autenticazione:

   * Se la richiesta contiene un token di autenticazione valido, cercare l&#39;utente nella tabella del database del cliente. Se l’utente è stato trovato:

      * Se la `Customer.IsSubscriber` proprietà è `true`, generate una licenza per il modello di utilizzo *Iscrizione* e inviatela all&#39;utente.

      * Cercare un record nella tabella del `CustomerAuthorization` database per l&#39;utente e l&#39;ID di contenuto. Se è stato trovato un record:

         * In caso `CustomerAuthorization.UsageType` affermativo, generate una licenza per il modello di utilizzo `DTO`Download To own ** e inviatela all&#39;utente.

         * In caso `CustomerAuthorization.UsageType` affermativo, generate una licenza per il modello di utilizzo di `VOD`Video On Demand ** e inviatela all&#39;utente.
   * Se nessuno dei criteri consente l&#39;accesso anonimo:

      * Se nella richiesta non è presente un token di autenticazione valido, restituisci un errore di tipo &quot;autenticazione richiesta&quot;.
      * In caso contrario, viene restituito un errore &quot;non autorizzato&quot;.


* Se uno dei criteri consente l&#39;accesso anonimo, genera una licenza per il modello di utilizzo finanziato tramite l&#39;annuncio e la invia all&#39;utente.

Prima che il server di implementazione di riferimento possa rilasciare licenze per la demo del modello di utilizzo, il server deve essere configurato per specificare come vengono generate le licenze per ciascuno dei quattro modelli di utilizzo. A questo scopo, specificate un criterio per ciascun modello di utilizzo. L&#39;implementazione di riferimento include quattro criteri di esempio ( [!DNL dto-policy.pol], [!DNL vod-policy.pol], [!DNL sub-policy.pol], [!DNL ad-policy.pol]) oppure potete sostituire i vostri criteri. In [!DNL flashaccess-refimpl.properties], impostate le seguenti proprietà per specificare il criterio da utilizzare per ogni modello di utilizzo e collocate i file dei criteri nella directory specificata dalla `config.resourcesDirectory` proprietà:

```
# Policy file name for Download To Own usage  
RefImpl.UsageModelDemo.Policy.DTO=dto-policy.pol  
# Policy file name for Rental usage  
RefImpl.UsageModelDemo.Policy.VOD=vod-policy.pol  
# Policy file name for Subscription usage  
RefImpl.UsageModelDemo.Policy.Subscribe=sub-policy.pol  
# Policy file name for Ad Supported (free) usage  
RefImpl.UsageModelDemo.Policy.Free=ad-policy.pol
```

