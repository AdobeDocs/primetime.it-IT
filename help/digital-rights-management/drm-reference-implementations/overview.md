---
title: Informazioni sulle implementazioni di riferimento
description: Informazioni sulle implementazioni di riferimento
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---


# Informazioni sulle implementazioni di riferimento{#about-the-reference-implementations}

Questa guida descrive l’installazione, la configurazione e il funzionamento delle implementazioni di riferimento Adobe Primetime DRM.

>[!NOTE]
>
>Primetime DRM era precedentemente chiamato Adobe Access e prima di questo, Flash Access.

Le implementazioni di riferimento DRM di Primetime includono questi componenti:

* **Strumenti da riga di comando** : questi strumenti si basano sullo stesso codice SDK DRM di Primetime utilizzato nel server di licenze DRM di Primetime. È possibile eseguire operazioni di packaging, licenze e altre attività DRM dalla riga di comando e alternare senza soluzione di continuità tra l&#39;utilizzo degli strumenti della riga di comando e il server licenze.
* **Server licenze** : un server licenze completamente funzionale e personalizzabile (descritto di seguito come una delle opzioni del server licenze).

**Opzioni del server licenze:**

* **Implementazioni di riferimento DRM di Primetime**  - Oggetto di questa guida, questa implementazione di riferimento presenta un robusto server di licenze DRM che mostra tutte le funzioni fornite dall&#39;SDK DRM di Primetime. Questa implementazione viene fornita con il codice sorgente e le istruzioni per la creazione del codice. Questa implementazione non deve essere utilizzata così com’è (anche se è incluso un file [!DNL .war] che puoi distribuire rapidamente). È progettato principalmente come riferimento da utilizzare per creare un server licenze personalizzato.

   Funzioni del server licenze:

   * Gestisce le richieste di autenticazione utilizzando un database per convalidare nome utente/password.
   * Gestisce le richieste di licenza e determina il tipo di licenza che viene rilasciata al momento dell&#39;applicazione della catena di licenze.
   * Rilascia licenze per contenuti che includono più criteri DRM di Primetime.
   * Rilascia licenze che supportano la consegna di chiavi remote ai client iOS, che richiede Primetime DRM.
   * Rilascia licenze che richiedono una ricerca e un recupero esterni della chiave di crittografia dei contenuti (CEK).
   * Esegue la ricerca in un database per determinare se un utente è autorizzato a visualizzare il contenuto.
   * Cerca negli elenchi degli aggiornamenti dei criteri DRM di Primetime.
   * Cerca negli elenchi di revoche dei computer.
   * Utilizza un file HSM o PKCS12 per memorizzare le credenziali.
   * Cifra le password specificate in un file di proprietà.
   * Specifica più credenziali di licenza o trasporto dopo il rinnovo delle credenziali.

      Le vecchie credenziali vengono mantenute sul server in modo che gli utenti possano continuare a visualizzare il contenuto esistente senza dover eseguire nuovamente il pacchetto.
   * Limita le versioni DRM/Runtime consentite per effettuare richieste a un server licenze.
   * Imposta le preferenze del ripristino a comparsa dell’orologio client.
   * Limita la differenza di tempo consentita tra il tempo di richiesta e il tempo del server per evitare attacchi di ripetizione.
   * Gestisce le richieste dai client FMRMS 1.x

      Ad esempio, il client FMRMS 1.x viene attivato per l&#39;aggiornamento a Primetime DRM 2.0 o versione successiva.
   * Converte i metadati FMRMS 1.x in metadati DRM di Primetime su richiesta utilizzando le informazioni di licenza FMRMS 1.x memorizzate in un database.
   * Converte i criteri FMRMS 1.x in criteri DRM di Primetime per il codice di esempio.
   * Importa le informazioni sulla licenza FMRMS 1.x da un database esistente per gli script di esempio.
   * Ottiene la versione del server
   * Registrazione del dominio
   * Deregistrazione del dominio
   * Richieste di sincronizzazione
   * Restituzione della licenza

* **Server DRM di Primetime per lo streaming**  protetto - Si tratta di un binario pronto all&#39;uso che puoi implementare rapidamente con il minimo sforzo. È una buona opzione per i clienti che desiderano mostrare rapidamente Proof of Concept, oppure *potrebbe* essere un&#39;opzione di produzione se le tue esigenze DRM personalizzate sono minime. Per ulteriori informazioni, consulta Informazioni correlate di seguito.

* **Servizio DRM di Primetime Cloud** : server con licenza ospitato da Adobi che puoi utilizzare per il servizio delle licenze. Per utilizzare questo servizio, devi essere un licenziatario di Primetime. Questo servizio cloud di Adobe ti libera dalle spese, dalla manutenzione e dall’ingegneria necessarie per creare il tuo servizio. Per ulteriori informazioni, consulta Informazioni correlate di seguito.

