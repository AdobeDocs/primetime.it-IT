---
title: Panoramica sull’implementazione dei modelli di utilizzo
description: Panoramica sull’implementazione dei modelli di utilizzo
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---


# Panoramica sull’implementazione dei modelli di utilizzo {#implementing-the-usage-models-overview}

L’implementazione di riferimento include la logica di business per dimostrare come abilitare i seguenti quattro diversi modelli di utilizzo per un contenuto in pacchetto:

* Download-to-own (DTO)
* Affitto/Video-on-demand (VOD)
* Abbonamento (all-you-can-eat)
* Finanziato con annunci

Per abilitare la demo del modello di utilizzo, specifica la proprietà personalizzata `RI_UsageModelDemo=true` al momento della creazione del pacchetto. Se si crea un pacchetto di contenuto utilizzando lo strumento a riga di comando Media Packager, specificare:

```
    java -jar AdobeMediaPackager.jar source.flv dest.flv -k RI_UsageModelDemo=true
```

>[!NOTE]
>
>Se non si attiva la modalità demo opzionale al momento della creazione del pacchetto, il server licenze utilizza i criteri specificati al momento della creazione del pacchetto per rilasciare una licenza. Se sono stati specificati più criteri, il server licenze utilizza il primo criterio valido.

Nella demo, la logica di business sul server controlla gli attributi effettivi delle licenze generate. Al momento dell&#39;imballaggio, nel contenuto devono essere incluse solo informazioni minime sulla politica. In particolare, il criterio deve solo indicare se è necessaria l’autenticazione per accedere al contenuto. Per abilitare tutti e quattro i modelli di utilizzo, includi un criterio che consenta l’accesso anonimo (per il modello finanziato dall’Ad) e un criterio che richiede l’autenticazione tramite nome utente/password (per gli altri 3 modelli di utilizzo). Quando si richiede una licenza, un&#39;applicazione client può determinare se richiedere all&#39;utente l&#39;autenticazione in base alle informazioni di autenticazione contenute nei criteri.

Per controllare il modello di utilizzo in base al quale un utente deve essere autorizzato a ottenere una licenza, è possibile aggiungere voci al database di implementazione di riferimento. La tabella `Customer` contiene nomi utente e password per l&#39;autenticazione degli utenti. Indica inoltre se l’utente dispone di una sottoscrizione. Agli utenti con abbonamenti verranno rilasciate licenze nel modello di utilizzo *Subscription*. Per concedere a un utente l&#39;accesso ai modelli di utilizzo *Download to own* o *Video on Demand*, è possibile aggiungere una voce alla tabella `CustomerAuthorization`, che specifica ogni elemento di contenuto a cui l&#39;utente può accedere e il modello di utilizzo. Per ulteriori informazioni sulla compilazione di ciascuna tabella, vedere lo script [!DNL PopulateSampleDB.sql] .

Quando un utente richiede una licenza, il server di implementazione dei riferimenti controlla i metadati inviati dal client per determinare se il contenuto è stato compilato utilizzando la proprietà `RI_UsageModelDemo` . In tal caso, vengono utilizzate le seguenti regole aziendali:

* Se uno dei criteri richiede l’autenticazione:

   * Se la richiesta contiene un token di autenticazione valido, cercare l&#39;utente nella tabella del database del cliente. Se l&#39;utente è stato trovato:

      * Se la proprietà `Customer.IsSubscriber` è `true`, genera una licenza per il modello di utilizzo *Subscription* e inviala all’utente.

      * Cerca un record nella tabella di database `CustomerAuthorization` per l&#39;utente e l&#39;ID di contenuto. Se è stato trovato un record:

         * Se `CustomerAuthorization.UsageType` è `DTO`, genera una licenza per il modello di utilizzo *Download To own* e inviala all’utente.

         * Se `CustomerAuthorization.UsageType` è `VOD`, genera una licenza per il modello di utilizzo *Video on Demand* e inviala all’utente.
   * Se nessuno dei criteri consente l&#39;accesso anonimo:

      * Se nella richiesta non è presente un token di autenticazione valido, restituire un errore di autenticazione richiesta.
      * In caso contrario, restituisce un errore &quot;non autorizzato&quot;.


* Se uno dei criteri consente l&#39;accesso anonimo, genera una licenza per il modello di utilizzo finanziato dall&#39;Ad e la invia all&#39;utente.

Prima che il server di implementazione di riferimento possa rilasciare licenze per la demo del modello di utilizzo, è necessario configurare il server per specificare come vengono generate le licenze per ciascuno dei quattro modelli di utilizzo. A tale scopo, specifica un criterio per ciascun modello di utilizzo. L&#39;implementazione di riferimento include quattro criteri di esempio ( [!DNL dto-policy.pol], [!DNL vod-policy.pol], [!DNL sub-policy.pol], [!DNL ad-policy.pol]) oppure puoi sostituirli. In [!DNL flashaccess-refimpl.properties], imposta le seguenti proprietà per specificare il criterio da utilizzare per ogni modello di utilizzo e inserire i file dei criteri nella directory specificata dalla proprietà `config.resourcesDirectory` :

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

