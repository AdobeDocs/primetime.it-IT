---
title: Guida rapida per programmatori
description: Guida rapida per programmatori
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 0%

---


# Guida rapida per programmatori {#programmer-kickstart-guide}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

## Introduzione {#prog-kickstart-guide-intro}

Benvenuti nell&#39;autenticazione Adobe Primetime per TV Everywhere. Siamo ansiosi di lavorare con voi.

>[!NOTE]
>
>Guida di Kickstart per programmatori (fornitori di contenuti). Se hai un MVPD (Multi-channel Video Programming Distributor), assicurati di vedere il [Guida rapida MVPD](/help/authentication/mvpd-kickstart-guide.md).


Contatti di autenticazione Adobe Primetime:

* Supporto : per tutte le domande, gli incidenti o le richieste di funzioni, `tve-support@adobe.com`
* Un contatto di abilitazione verrà assegnato al progetto al momento del kickoff del progetto.

Le informazioni seguenti illustrano alcuni importanti primi passi per arrivare a un inizio solido ed efficiente. L&#39;obiettivo è quello di fornire una spiegazione e un&#39;aspettativa su come lavoreremo con i partner per raggiungere le integrazioni. Si prega di notare le sezioni &quot;Lei fornirà&quot; / &quot;Adobe fornirà&quot; sotto per ogni elemento. Questi vengono elencati tramite una lista di controllo o una guida durante l’elaborazione del progetto.

Questo documento presuppone che i programmatori siano registrati per lavorare con un partner MVPD scelto.

## Pianificazione del rilascio {#release-schedule}

Il ciclo di sviluppo della velocità di Adobe è pianificato in modo da poter vedere quando sono programmate le nostre versioni e come ogni versione viene promossa tramite il nostro sistema di sviluppo.

Una volta completato ogni sprint, è disponibile per il QE, o per vedere nuove implementazioni sul nostro server UAT.

Circa ogni 6 settimane verrà rilasciata al server di pre-qualificazione Adobe. (Questo è il server in cui si tiene la prossima versione proposta mentre si esegue il QE finale.) Queste build includeranno tutto il lavoro completato in sprint dall&#39;ultima goccia. Al momento è disponibile una finestra QE di due settimane per consentire ai partner di testare questa versione.

Presupponendo che non siano sorti problemi critici durante la precedente finestra di test di due settimane, il rilascio verrà promosso alla produzione live. Ciò significa che l’integrazione sarà disponibile nell’ambiente di rilascio di Adobe, ma i partner scelgono quando rendere pubblico il rilascio.

<!--For the latest release schedule information, see the Release Calendar.-->

## Documentazione del supporto {#supp-doc}

L’Adobe fornisce:

* Guida alla distribuzione: **`https://tve.zendesk.com/entries/498741-tve-deployment-guide`**
* Accesso al sistema di assistenza clienti Zendesk. È inoltre possibile trovare campioni, informazioni ed esercitazioni video su alcuni dei processi. Per accedere a questo documento su Zendesk, insieme ad altri documenti pubblicati lì, dovrai registrarti e creare un account all&#39;indirizzo `https://tve.zendesk.com/home`. Non esiste alcun limite alla quantità di utenti che è possibile registrare.  Puoi vedere e condividere i commenti su qualsiasi biglietto archiviato. Tutte le domande di assistenza devono essere rivolte a `tve-support@adobe.com`.
* [Guida all&#39;integrazione dei programmatori](/help/authentication/programmer-integration-guide-overview.md)
* Libreria di verificatori di token multimediali: `https://tve.zendesk.com/entries/471323-media-token-validator-library`.

## Configurazione dell’ambiente di test {#test-env-setup}

Adobe ti configurerà innanzitutto con il sito di test Adobe, dove l’Adobe funge da MVPD a scopo di test. Il team può quindi impostare un sito web di prova che chiama l’API Adobe. Utilizza il selettore MVPD predefinito e seleziona &quot;Adobe&quot; come idP.

Fornirai:

1. ID richiedente. Si tratta di una stringa che identificherà in modo univoco il marchio del sito web o dell’applicazione che sta effettuando richieste di autenticazione Adobe Primetime. La stringa stessa è arbitraria ma deve essere concordata tra l&#39;Adobe e il programmatore
1. Informazioni sul canale. Si tratta di un set di stringhe che identifica i canali di contenuto richiesti dal requestor ID. In molti casi il canale e l’ID del richiedente sono gli stessi. Tuttavia, puoi avere più canali di contenuto che possono essere richiesti dallo stesso ID. Le stringhe del nome del canale devono corrispondere ai canali TV via cavo. Alcuni MVPD convalideranno questo valore sul protocollo AuthN e/o AuthZ.
1. Nomi di dominio (da consentire per l&#39;ID richiedente). Si tratta di un elenco di nomi di dominio effettivi che verranno elencati per Adobe per accettare il requestor ID. In questo modo, solo i domini approvati avranno accesso all’autenticazione Adobe Primetime con i tuoi metadati. NOTA: i nomi di dominio validi per la produzione possono essere diversi per la prova/staging e devono essere entrambi forniti e identificati.

L’Adobe configurerà l’account e l’Adobe fornirà:

* Accesso e password per accedere al sito di prova

## Configurazione con MVPD {#setup-mvpd}

Questa sezione descrive cosa ti serve quando esegui la migrazione dal sito di test Adobe per lavorare con un MVPD.

Fornirai (via MVPD):

* **Due set di credenziali**:
   * AuthN + AuthZ : login/password per un utente autenticato e autorizzato
   * AuthN + Non-AuthZ : login/password per un utente autenticato ma non autorizzato
* **ID risorsa**. Si tratta di un identificatore di contenuto specifico che verrà convalidato con un MVPD sul protocollo AuthZ. Può trovarsi a livello di canale, show, episodio o risorsa; dovrebbe essere concordato con il tuo MVPD.

L’autenticazione Adobe Primetime supporta uno schema di metadati basato su MRSS, il che significa che gli ID risorsa possono essere specifici a seconda delle esigenze, e possono includere identificatori che possono essere univoci per un MVPD specifico.

**Nuova integrazione MVPD**: È importante ricordare che l&#39;MVPD scelto svolge una parte integrante nel completamento di qualsiasi integrazione. L&#39;Adobe deve scrivere il codice per ogni MVPD in base alle proprie specifiche. Finché questi passaggi non saranno completati, non potrai selezionare tale MVPD dalla finestra di dialogo o completare il test del prodotto. L&#39;Adobe deve pianificare questo lavoro in anticipo per adattarsi al prossimo sprint disponibile. (Per informazioni sulla pianificazione corrente, consulta Calendario delle versioni).

**Integrazioni MVPD esistenti**: Se l&#39;MVPD scelto è già configurato con l&#39;Adobe, i passaggi di connettività dovrebbero essere molto più semplici (più veloci) e spesso la connettività può essere ottenuta tramite modifiche alla configurazione.

>[!NOTE]
>
>L&#39;MVPD dovrà ancora abilitare il Programmatore e sottoscrivere qualsiasi accordo commerciale pertinente.

**QE con MVPD**: Tutte le integrazioni coinvolgeranno il QE congiunto, e dato che l&#39;utente finale è in definitiva un cliente del MVPD, molti hanno impostato cicli di test prima di spingere &quot;live&quot;. Poiché ciò comporta la programmazione di risorse MVPD, questa è un&#39;area potenziale per ritardi.

<!--
>[RELATEDINFORMATION]
>[MVPD Kickstart Guide](help\authentication\mvpd-kickstart-guide.md)
-->

