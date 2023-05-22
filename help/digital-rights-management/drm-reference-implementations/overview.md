---
title: Informazioni sulle implementazioni di riferimento
description: Informazioni sulle implementazioni di riferimento
copied-description: true
exl-id: fe387330-9449-4977-be15-069c814354bf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---

# Informazioni sulle implementazioni di riferimento{#about-the-reference-implementations}

Questa guida descrive l’installazione, la configurazione e il funzionamento delle implementazioni di riferimento Adobe Primetime DRM.

>[!NOTE]
>
>In precedenza, DRM Primetime era denominato accesso di Adobe e prima ancora Flash Access.

Le implementazioni di riferimento DRM di Primetime includono i seguenti componenti:

* **Strumenti della riga di comando** - Questi strumenti sono basati sullo stesso codice SDK di Primetime DRM utilizzato nel server licenze di Primetime DRM. È possibile eseguire attività di creazione pacchetti, gestione licenze e altre attività DRM dalla riga di comando e alternare in modo semplice utilizzando gli strumenti della riga di comando e il server licenze.
* **Server licenze** - Un server licenze completamente funzionale e personalizzabile (descritto di seguito come una delle opzioni del server licenze).

**Opzioni server licenze:**

* **Implementazioni di riferimento DRM di Primetime** - Oggetto di questa guida, questa implementazione di riferimento è dotata di un robusto server di licenze DRM che presenta tutte le funzioni fornite dall&#39;SDK di Primetime DRM. Questa implementazione viene fornita con il codice sorgente e le istruzioni per la creazione del codice. Questa implementazione non deve essere utilizzata così com’è (anche se un [!DNL .war] è incluso e può essere implementato rapidamente). Si tratta principalmente di un riferimento da utilizzare per creare un server licenze personalizzato.

   Funzionalità server licenze:

   * Gestisce le richieste di autenticazione utilizzando un database per convalidare nome utente/password.
   * Gestisce le richieste di licenza e determina il tipo di licenza rilasciata quando viene applicato il concatenamento licenze.
   * Rilascia licenze per contenuti che includono più criteri DRM di Primetime.
   * Rilascia licenze che supportano la distribuzione di chiavi remote ai client iOS, che richiede Primetime DRM.
   * Emette licenze che richiedono una ricerca e un recupero esterni della chiave di crittografia del contenuto (CEK).
   * Cerca in un database per determinare se un utente è autorizzato a visualizzare il contenuto.
   * Cerca gli elenchi di aggiornamento dei criteri DRM di Primetime.
   * Cerca gli elenchi di revoche di computer.
   * Utilizza un file HSM o PKCS12 per memorizzare le credenziali.
   * Crittografa le password specificate in un file di proprietà.
   * Specifica più credenziali di trasporto o server licenze dopo il rinnovo delle credenziali.

      Le vecchie credenziali vengono mantenute sul server, in modo che gli utenti possano continuare a visualizzare il contenuto esistente senza dover creare un nuovo pacchetto.
   * Limita le versioni DRM/Runtime che possono effettuare richieste a un server licenze.
   * Imposta le preferenze di ritorno a capo dell&#39;orologio del client.
   * Limita la differenza di tempo consentita tra il tempo della richiesta e quello del server per evitare attacchi di ripetizione.
   * Gestisce le richieste dei client FMRMS 1.x

      Ad esempio, il client FMRMS 1.x viene attivato per l’aggiornamento a Primetime DRM 2.0 o versione successiva.
   * Converte i metadati FMRMS 1.x in metadati DRM Primetime su richiesta utilizzando le informazioni sulla licenza FMRMS 1.x memorizzate in un database.
   * Converte i criteri FMRMS 1.x in criteri DRM di Primetime per il codice di esempio.
   * Importa le informazioni sulle licenze FMRMS 1.x da un database esistente per gli script di esempio.
   * Ottiene la versione del server
   * Registrazione del dominio
   * Annullamento della registrazione del dominio
   * Richieste di sincronizzazione
   * Restituzione licenza

* **Server DRM Primetime per lo streaming protetto** : si tratta di un binario pronto per l’uso che puoi implementare rapidamente con il minimo sforzo. Si tratta di una buona opzione per i clienti che desiderano mostrare rapidamente Proof of Concept, o *potrebbe* essere un&#39;opzione di produzione se le esigenze DRM personalizzate sono minime. Per ulteriori informazioni, consulta Informazioni correlate di seguito.

* **Servizio DRM cloud di Primetime** : questo è un server licenze ospitato da Adobi che puoi utilizzare per la gestione delle licenze. Per utilizzare questo servizio è necessario essere un licenziatario di Primetime. Questo Adobe di servizio cloud consente di ridurre i costi, la manutenzione e la progettazione necessari per creare un servizio personalizzato. Per ulteriori informazioni, consulta Informazioni correlate di seguito.
