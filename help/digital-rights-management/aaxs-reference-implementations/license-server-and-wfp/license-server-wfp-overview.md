---
title: Panoramica del server licenze e del pacchetto cartelle controllato
description: Panoramica del server licenze e del pacchetto cartelle controllato
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---


# Panoramica del server licenze e del pacchetto cartelle controllato {#license-server-and-watched-folder-packager-overview}

Il server di implementazione di riferimento può essere utile per creare un server licenze utilizzando Adobe Access SDK. In questa implementazione, gli utenti vengono autenticati in base alle voci utente in un database. Il server include la logica aziendale dimostrativa per il rilascio delle licenze. Implementa anche il supporto per la compatibilità per Flash Media Rights Management Server 1.0 e 1.5.

Il server di implementazione di riferimento include anche un&#39;implementazione controllata della cartella del packager. Questo componente può essere distribuito insieme al server licenze o su un computer separato. Con questa implementazione di packager, è possibile creare più cartelle controllate. Quando il contenuto viene rilasciato nella cartella controllata, il packager automaticamente lo compila.

Il server licenze e il packager sono distribuiti come file WAR separati, in modo da poter scegliere se eseguirli su server separati o in un&#39;unica istanza Apache Tomcat®. Il server licenze si trova in [!DNL flashaccess.war] e il packager si trova in [!DNL flashaccess-packager.war]. L&#39;opzione opzionale [!DNL edcws.war] contiene il supporto per le richieste di licenza da parte dei client FMRMS 1.x.

Il codice di esempio di implementazione di riferimento illustra le seguenti funzioni:

* Server licenze:

   * Gestione delle richieste di autenticazione, utilizzo di un database per convalidare nome utente/password
   * Gestione delle richieste di licenza e determinazione del tipo di licenza da rilasciare quando si utilizza la catena di licenze.
   * Rilascio di licenze per contenuti contenenti più criteri
   * Rilasciare licenze che supportano la consegna di chiavi remote ai client iOS (richiede Adobe Primetime)
   * Rilascio di licenze che richiedono una ricerca/recupero esterni della chiave di crittografia dei contenuti (CEK)
   * Utilizzo del database per determinare se l’utente è autorizzato a visualizzare il contenuto
   * Utilizzo degli elenchi di aggiornamento dei criteri
   * Utilizzo degli elenchi di revoche dei computer
   * Utilizzo di un file HSM o PKCS12 per memorizzare le credenziali
   * Crittografia delle password specificate nel file delle proprietà
   * Specifica di più server licenze o credenziali di trasporto (dopo il rinnovo delle credenziali, le vecchie credenziali vengono mantenute sul server in modo che il contenuto esistente possa essere utilizzato senza dover ripetere il pacchetto)
   * Limitazione delle versioni DRM/Runtime consentite per effettuare richieste al server licenze
   * Impostazione delle preferenze per la finestra dell&#39;orologio del client
   * Limitazione della differenza di tempo consentita tra il tempo di richiesta e il tempo del server (per evitare attacchi di ripetizione)
   * Gestione delle richieste dai client FMRMS 1.x (attiva il client FMRMS 1.x per l’aggiornamento ad Adobe Access 2.0 o successivo)
   * Conversione rapida dei metadati FMRMS 1.x in metadati di accesso Adobe, utilizzando le informazioni di licenza FMRMS 1.x memorizzate in un database
   * Codice di esempio per la conversione dei criteri FMRMS 1.x in criteri di accesso Adobe
   * Script di esempio per l&#39;importazione di informazioni sulla licenza FMRMS 1.x da un database esistente
   * Scarica versione server
   * Registrazione del dominio
   * Deregistrazione del dominio
   * Richieste di sincronizzazione
   * Restituzione della licenza

* Server Packager:

   * Implementazione di un’implementazione di packager che pacchetti automaticamente il contenuto aggiunto a una cartella controllata
   * Utilizzo di un file HSM o PKCS12 per memorizzare le credenziali
   * Crittografia delle password specificate nel file delle proprietà
   * Configurazione del packager, creazione di criteri e creazione di elenchi di aggiornamento dei criteri utilizzando un&#39;applicazione AIR

