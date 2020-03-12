---
seo-title: Regole di utilizzo
title: Regole di utilizzo
uuid: 361d07b9-e4c8-47ab-8c45-a1de98c9fed7
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Regole di utilizzo{#usage-rules}

Con Adobe Access Server for Protected Streaming, tutte le regole di utilizzo vengono specificate nel server tramite i file di configurazione. Eventuali regole di utilizzo specificate nel contenuto protetto vengono ignorate, pertanto si consiglia di utilizzare un semplice criterio anonimo durante la creazione dei contenuti. Le regole di utilizzo configurabili possono essere impostate per ogni tenant.

Adobe Access Server for Protected Streaming supporta le seguenti regole di utilizzo:

* Protezione dell&#39;output
* Restrizioni per applicazioni Adobe® AIR®, SWF, iOS e Android
* Limitazioni per i moduli DRM e Runtime
* Applicazione del rilevamento Jailbreak (sulle piattaforme Adobe Access che supportano il rilevamento delle interruzioni di chiamata)
* La memorizzazione della cache delle licenze è disabilitata per impostazione predefinita. Il caching delle licenze può essere attivato specificando la data di fine del caching o un numero di cache di tempo consentito (a partire dal momento in cui viene rilasciata la licenza).
* Più diritti di riproduzione, che consentono di specificare diverse combinazioni di Protezione output, Restrizioni applicazione e Limitazioni DRM/Runtime. Ad esempio, è possibile specificare diversi requisiti di protezione dell&#39;output per ogni piattaforma client utilizzando la limitazione del modulo DRM con Protezione dell&#39;output.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Per supportare la consegna di chiavi remote ai dispositivi iOS, il criterio utilizzato al momento della creazione del pacchetto deve avere la consegna di chiavi remote abilitata. Questa impostazione non può essere modificata tramite la configurazione tenant sul server. ***Adobe Primetime è richiesto per creare applicazioni iOS in grado di riprodurre contenuto protetto da Adobe Access.***

