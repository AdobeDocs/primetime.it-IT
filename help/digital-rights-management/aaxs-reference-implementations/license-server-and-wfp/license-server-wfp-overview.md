---
title: Panoramica del server licenze e del packager cartelle controllate
description: Panoramica del server licenze e del packager cartelle controllate
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# Panoramica del server licenze e del packager cartelle controllate {#license-server-and-watched-folder-packager-overview}

Il server di implementazione di riferimento può essere utile per creare un server licenze utilizzando l’SDK di accesso di Adobe. In questa implementazione, gli utenti vengono autenticati in base alle voci utente in un database. Il server include una dimostrazione della logica di business per il rilascio delle licenze. Implementa inoltre il supporto della compatibilità per Flash Media Rights Management Server 1.0 e 1.5.

Il server di implementazione di riferimento include anche un&#39;implementazione di cartella controllata del packager. Questo componente può essere distribuito insieme al server licenze o in un computer separato. Con questa implementazione di Packager è possibile creare più cartelle controllate. Quando il contenuto viene rilasciato nella cartella controllata, il packager crea automaticamente un pacchetto del contenuto.

Il server licenze e il packager vengono distribuiti come file WAR separati, in modo da poter scegliere se eseguirli su server separati o in una singola istanza Apache Tomcat®. Il server licenze si trova in [!DNL flashaccess.war] e il confezionatore è in [!DNL flashaccess-packager.war]. L&#39;opzione [!DNL edcws.war] contiene il supporto per le richieste di licenza dai client FMRMS 1.x.

Il codice di esempio per l’implementazione di riferimento illustra le seguenti funzioni:

* Server licenze:

   * Gestione delle richieste di autenticazione, utilizzo di un database per convalidare nome utente/password
   * Gestione delle richieste di licenza e determinazione del tipo di licenza da rilasciare quando viene utilizzato il concatenamento delle licenze.
   * Rilascio di licenze per contenuti contenenti più criteri
   * Rilasciare licenze che supportano la distribuzione di chiavi remote ai client iOS (richiede Adobe Primetime)
   * Rilascio di licenze che richiedono una ricerca/recupero esterna della chiave di crittografia del contenuto (CEK)
   * Utilizzo del database per determinare se l&#39;utente è autorizzato a visualizzare il contenuto
   * Utilizzo degli elenchi di aggiornamento dei criteri
   * Utilizzo di elenchi di revoche di computer
   * Utilizzo di un file HSM o PKCS12 per l&#39;archiviazione delle credenziali
   * Crittografia delle password specificate nel file delle proprietà
   * Specifica di più credenziali del server licenze o del trasporto (dopo il rinnovo delle credenziali, le vecchie credenziali vengono mantenute nel server in modo da poter utilizzare il contenuto esistente senza dover creare un nuovo pacchetto)
   * Limitazione delle versioni DRM/Runtime consentite per effettuare richieste al server licenze
   * Impostazione delle preferenze di ripristino dell&#39;orologio del client
   * Limitazione della differenza di tempo consentita tra il tempo della richiesta e il tempo del server (per evitare attacchi di ripetizione)
   * Gestione delle richieste dai client FMRMS 1.x (attiva il client FMRMS 1.x per l’aggiornamento ad Adobe Access 2.0 o versione successiva)
   * Conversione immediata di metadati FMRMS 1.x in metadati di Access di Adobe, utilizzando le informazioni sulla licenza FMRMS 1.x memorizzate in un database
   * Codice di esempio per la conversione dei criteri FMRMS 1.x in criteri di accesso Adobe
   * Script di esempio per importare informazioni sulle licenze FMRMS 1.x da un database esistente
   * Ottieni versione server
   * Registrazione del dominio
   * Annullamento della registrazione del dominio
   * Richieste di sincronizzazione
   * Restituzione licenza

* Server Packager:

   * Implementazione di un’implementazione packager che crea automaticamente pacchetti di contenuti aggiunti a una cartella controllata
   * Utilizzo di un file HSM o PKCS12 per l&#39;archiviazione delle credenziali
   * Crittografia delle password specificate nel file delle proprietà
   * Configurazione del packager, creazione di policy e creazione di elenchi di aggiornamento delle policy tramite un’applicazione AIR
