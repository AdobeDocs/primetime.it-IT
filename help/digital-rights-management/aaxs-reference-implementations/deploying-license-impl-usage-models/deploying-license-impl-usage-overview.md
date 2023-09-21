---
title: Panoramica sull’implementazione dei modelli di utilizzo
description: Panoramica sull’implementazione dei modelli di utilizzo
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---

# Panoramica sull’implementazione dei modelli di utilizzo {#implementing-the-usage-models-overview}

L’implementazione di riferimento include la logica di business per dimostrare come abilitare i seguenti quattro diversi modelli di utilizzo per un contenuto collocato:

* Download-to-own (DTO)
* Noleggio/Video-on-demand (VOD)
* Abbonamento (tutto ciò che puoi mangiare)
* Finanziato da annunci

Per abilitare la demo del modello di utilizzo, specifica la proprietà personalizzata `RI_UsageModelDemo=true` al momento del confezionamento. Se stai creando il pacchetto di contenuto utilizzando lo strumento per riga di comando Media Packager, specifica:

```
    java -jar AdobeMediaPackager.jar source.flv dest.flv -k RI_UsageModelDemo=true
```

>[!NOTE]
>
>Se non si attiva la modalità demo opzionale al momento del packaging, il server licenze utilizza i criteri specificati al momento del packaging per rilasciare una licenza. Se sono stati specificati più criteri, il server licenze utilizzerà il primo criterio valido.

Nella demo, la logica di business sul server controlla gli attributi effettivi delle licenze generate. Al momento della creazione del pacchetto, nel contenuto devono essere incluse solo informazioni minime sulla policy. In particolare, il criterio deve solo indicare se è necessaria l’autenticazione per accedere al contenuto. Per abilitare tutti e quattro i modelli di utilizzo, includi un criterio che consenta l’accesso anonimo (per il modello finanziato da Ad) e un criterio che richieda l’autenticazione nome utente/password (per gli altri tre modelli di utilizzo). Quando si richiede una licenza, un&#39;applicazione client può determinare se richiedere all&#39;utente l&#39;autenticazione in base alle informazioni di autenticazione contenute nei criteri.

Per controllare il modello di utilizzo in base al quale a un particolare utente deve essere rilasciata una licenza, è possibile aggiungere voci al database di implementazione di riferimento. Il `Customer` La tabella contiene nomi utente e password per l&#39;autenticazione degli utenti. Indica anche se l’utente dispone di una sottoscrizione. Agli utenti con abbonamenti verranno rilasciate licenze ai sensi del *Abbonamento* modello di utilizzo. Per concedere a un utente l&#39;accesso *Scarica su proprio* o *Video on-demand* modelli di utilizzo, è possibile aggiungere una voce al `CustomerAuthorization` , che specifica ogni elemento di contenuto a cui l&#39;utente può accedere e il modello di utilizzo. Consulta la [!DNL PopulateSampleDB.sql] script per i dettagli sul popolamento di ogni tabella.

Quando un utente richiede una licenza, il server di implementazione di riferimento controlla i metadati inviati dal client per determinare se il contenuto è stato creato utilizzando `RI_UsageModelDemo` proprietà. In tal caso, vengono utilizzate le seguenti regole aziendali:

* Se uno dei criteri richiede l’autenticazione:

   * Se la richiesta contiene un token di autenticazione valido, cerca l’utente nella tabella del database del cliente. Se l&#39;utente è stato trovato:

      * Se il `Customer.IsSubscriber` la proprietà è `true`, genera una licenza per *Abbonamento* modello di utilizzo e inviarlo all&#39;utente.

      * Cercare un record in `CustomerAuthorization` tabella di database per questo ID utente e contenuto. Se è stato trovato un record:

         * Se `CustomerAuthorization.UsageType` è `DTO`, genera una licenza per *Scarica su Proprietario* modello di utilizzo e inviarlo all&#39;utente.

         * Se `CustomerAuthorization.UsageType` è `VOD`, genera una licenza per *Video On Demand* modello di utilizzo e inviarlo all&#39;utente.

   * Se nessuno dei criteri consente l’accesso anonimo:

      * Se nella richiesta non è presente un token di autenticazione valido, viene restituito un errore di tipo &quot;autenticazione richiesta&quot;.
      * In caso contrario, viene restituito un errore &quot;non autorizzato&quot;.

* Se uno dei criteri consente l’accesso anonimo, genera una licenza per il modello di utilizzo finanziato dall’annuncio e inviala all’utente.

Prima che il server di implementazione di riferimento possa rilasciare licenze per la demo del modello di utilizzo, è necessario configurarlo per specificare la modalità di generazione delle licenze per ciascuno dei quattro modelli di utilizzo. A tale scopo, specifica un criterio per ciascun modello di utilizzo. L’implementazione di riferimento include quattro criteri di esempio ( [!DNL dto-policy.pol], [!DNL vod-policy.pol], [!DNL sub-policy.pol], [!DNL ad-policy.pol]) o sostituire le proprie policy. In entrata [!DNL flashaccess-refimpl.properties], impostare le seguenti proprietà per specificare il criterio da utilizzare per ogni modello di utilizzo e inserire i file dei criteri nella directory specificata da `config.resourcesDirectory` proprietà:

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
