---
seo-title: Panoramica del server licenze e del pacchetto cartelle controllato
title: Panoramica del server licenze e del pacchetto cartelle controllato
uuid: 3dd6f699-a5c0-44c4-897a-34e06abe3d71
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---


# Panoramica del server licenze e del packager cartelle controllato {#license-server-and-watched-folder-packager-overview}

Il server di implementazione di riferimento può essere utile per creare un server licenze tramite l’SDK di accesso al Adobe . In questa implementazione, gli utenti vengono autenticati in base alle voci degli utenti in un database. Il server include logica aziendale dimostrativa per il rilascio delle licenze. Implementa inoltre il supporto della compatibilità per Flash Media Rights Management Server 1.0 e 1.5.

Il server di implementazione di riferimento include anche un’implementazione controllata della cartella del packager. Questo componente può essere distribuito insieme al server licenze o su un computer separato. Con questa implementazione del packager, è possibile creare più cartelle esaminate. Quando il contenuto viene rilasciato nella cartella esaminata, il packager crea automaticamente il pacchetto.

Il server licenze e il packager sono distribuiti come file WAR separati, in modo da poter scegliere se eseguirli su server separati o in una singola istanza Apache Tomcat®. Il server licenze si trova in [!DNL flashaccess.war] e il packager si trova in [!DNL flashaccess-packager.war]. L&#39;opzione opzionale [!DNL edcws.war] contiene il supporto per le richieste di licenza da parte dei client FMRMS 1.x.

Il codice di esempio di implementazione di riferimento illustra le seguenti funzionalità:

* Server licenze:

   * Gestione delle richieste di autenticazione, utilizzo di un database per convalidare nome utente/password
   * Gestione delle richieste di licenza e determinazione del tipo di licenza da rilasciare quando viene utilizzato il concatenamento della licenza.
   * Rilascio di licenze per il contenuto contenente più criteri
   * Rilascio di licenze che supportano la fornitura di chiavi remote ai client iOS (richiede  Adobe Primetime)
   * Rilascio di licenze che richiedono una ricerca/recupero esterni della chiave di crittografia dei contenuti (CEK)
   * Utilizzo del database per determinare se l&#39;utente è autorizzato a visualizzare il contenuto
   * Utilizzo degli elenchi di aggiornamento dei criteri
   * Uso degli elenchi di revoche dei computer
   * Utilizzo di un file HSM o PKCS12 per memorizzare le credenziali
   * Cifratura delle password specificate nel file delle proprietà
   * Specifica di più server licenze o credenziali di trasporto (dopo il rinnovo delle credenziali, le vecchie credenziali vengono conservate sul server in modo che il contenuto esistente possa essere utilizzato senza la necessità di eseguire nuovamente il pacchetto)
   * Limitazione delle versioni DRM/Runtime consentite per effettuare richieste al server licenze
   * Impostazione delle preferenze del blocco del client
   * Limitazione della differenza di tempo consentita tra l&#39;ora della richiesta e l&#39;ora del server (per evitare attacchi di ripetizione)
   * Gestione delle richieste dai client FMRMS 1.x (attiva il client FMRMS 1.x per effettuare l&#39;aggiornamento  Adobe Access 2.0 o successivo)
   * Conversione rapida dei metadati FMRMS 1.x in  metadati di accesso al Adobe, utilizzando le informazioni di licenza FMRMS 1.x memorizzate in un database
   * Codice di esempio per la conversione dei criteri FMRMS 1.x in criteri di accesso  Adobe
   * Script di esempio per l&#39;importazione di informazioni sulle licenze FMRMS 1.x da un database esistente
   * Ottieni versione server
   * Registrazione del dominio
   * Disregistrazione del dominio
   * Richieste di sincronizzazione
   * Restituzione licenza

* Server Packager:

   * Implementazione di un&#39;implementazione di packager che crea automaticamente un pacchetto per il contenuto aggiunto a una cartella esaminata
   * Utilizzo di un file HSM o PKCS12 per memorizzare le credenziali
   * Cifratura delle password specificate nel file delle proprietà
   * Configurazione del packager, creazione di criteri e creazione di elenchi di aggiornamenti tramite un&#39;applicazione AIR

