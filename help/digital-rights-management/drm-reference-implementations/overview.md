---
description: 'null'
seo-description: 'null'
seo-title: Informazioni sulle implementazioni dei riferimenti
title: Informazioni sulle implementazioni dei riferimenti
uuid: f08fdb4b-aaa8-4871-bb62-1a21d5abdd8d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---


# Informazioni sulle implementazioni di riferimento{#about-the-reference-implementations}

Questa guida descrive l&#39;installazione, la configurazione e il funzionamento delle implementazioni di riferimento Adobe Primetime DRM .

>[!NOTE]
>
>Primetime DRM era precedentemente chiamato  Adobe Access e prima di tale Flash Access.

Le implementazioni di riferimento DRM di Primetime includono i seguenti componenti:

* **Strumenti**  della riga di comando: questi strumenti sono basati sullo stesso codice SDK DRM Primetime utilizzato nel server licenze DRM di Primetime. È possibile eseguire la creazione di pacchetti, la concessione di licenze e altre attività DRM dalla riga di comando e alternare facilmente tra gli strumenti della riga di comando e il server licenze.
* **Server**  licenze - Un server licenze completamente funzionale e personalizzabile (descritto di seguito come una delle opzioni del server licenze).

**Opzioni del server licenze:**

* **Implementazioni**  di riferimento DRM di Primetime - L&#39;oggetto di questa guida, questa implementazione di riferimento include un robusto server licenze DRM che mostra tutte le funzionalità fornite dall&#39;SDK DRM di Primetime. Questa implementazione viene fornita con il codice sorgente e le istruzioni per la creazione del codice. Questa implementazione non deve essere utilizzata così come è (anche se è incluso un file [!DNL .war] che può essere distribuito rapidamente). Si tratta principalmente di un riferimento che potete utilizzare per creare un vostro server licenze personalizzato.

   Funzioni del server licenze:

   * Gestisce le richieste di autenticazione utilizzando un database per convalidare nome utente/password.
   * Gestisce le richieste di licenza e determina il tipo di licenza che viene rilasciato quando si applica il concatenamento di licenze.
   * Rilascia licenze per il contenuto che include più criteri DRM di Primetime.
   * Rilascia licenze che supportano la consegna di chiavi remote ai client iOS, che richiedono DRM di Primetime.
   * Rilascia licenze che richiedono una ricerca e un recupero esterni della chiave di crittografia dei contenuti (CEK).
   * Esegue una ricerca in un database per determinare se un utente è autorizzato a visualizzare il contenuto.
   * Cerca negli elenchi degli aggiornamenti dei criteri DRM di Primetime.
   * Cerca gli elenchi di revoche dei computer.
   * Utilizza un file HSM o PKCS12 per memorizzare le credenziali.
   * Cifra le password specificate in un file delle proprietà.
   * Specifica più credenziali di licenza o trasporto dopo il rinnovo delle credenziali.

      Le vecchie credenziali vengono mantenute sul server in modo che gli utenti possano continuare a visualizzare il contenuto esistente senza dover creare nuovamente il pacchetto.
   * Limita le versioni DRM/Runtime consentite per effettuare richieste a un server licenze.
   * Imposta le preferenze relative al backback dell&#39;orologio client.
   * Limita la differenza di tempo consentita tra l&#39;ora della richiesta e l&#39;ora del server per evitare attacchi di ripetizione.
   * Gestisce le richieste dai client FMRMS 1.x

      Ad esempio, il client FMRMS 1.x viene attivato per eseguire l&#39;aggiornamento a Primetime DRM 2.0 o versione successiva.
   * Converte i metadati FMRMS 1.x in metadati DRM di Primetime su richiesta utilizzando le informazioni sulle licenze FMRMS 1.x memorizzate in un database.
   * Converte i criteri FMRMS 1.x in criteri DRM di Primetime per il codice di esempio.
   * Importa le informazioni sulla licenza FMRMS 1.x da un database esistente per gli script di esempio.
   * Ottiene la versione del server
   * Registrazione del dominio
   * Disregistrazione del dominio
   * Richieste di sincronizzazione
   * Restituzione licenza

* **Server DRM di Primetime per lo streaming**  protetto - Si tratta di un binario pronto per essere implementato rapidamente con il minimo sforzo. È una buona opzione per i clienti che desiderano mostrare rapidamente Proof of Concept, oppure *potrebbe* essere un&#39;opzione di produzione se le esigenze DRM personalizzate sono minime. Per ulteriori informazioni, consulta Informazioni correlate di seguito.

* **Servizio**  DRM di Primetime Cloud - Server di licenze ospitato  Adobe che puoi utilizzare per la trasmissione delle licenze. Per utilizzare questo servizio, è necessario essere un licenziatario di Primetime. Questo servizio cloud di  Adobe ti permette di risparmiare sulle spese, la manutenzione e la progettazione necessarie per creare il tuo servizio. Per ulteriori informazioni, consulta Informazioni correlate di seguito.

