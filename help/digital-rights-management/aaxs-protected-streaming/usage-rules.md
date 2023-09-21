---
title: Regole di utilizzo
description: Regole di utilizzo
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# Regole di utilizzo{#usage-rules}

Con Adobe Access Server for Protected Streaming, tutte le regole di utilizzo vengono specificate sul server tramite i file di configurazione. Tutte le regole di utilizzo specificate nel contenuto protetto vengono ignorate, pertanto si consiglia di utilizzare una semplice policy anonima durante la creazione del pacchetto di contenuto. Le regole di utilizzo configurabili possono essere impostate per tenant.

Adobe Access Server for Protected Streaming supporta le seguenti regole di utilizzo:

* Protezione dell&#39;output
* Limitazioni per le applicazioni Adobe® AIR®, SWF, iOS e Android
* Restrizioni per i moduli DRM e runtime
* Applicazione del rilevamento jailbreak (su piattaforme Adobe Access che supportano il rilevamento jailbreak)
* Il caching delle licenze è disattivato per impostazione predefinita. È possibile abilitare il caching delle licenze specificando la data di fine del caching o specificando un periodo di tempo in cui il caching è consentito (a partire dal momento in cui viene rilasciata la licenza).
* Più diritti di riproduzione, che consentono di specificare diverse combinazioni di protezione dell&#39;output, restrizioni dell&#39;applicazione e restrizioni DRM/runtime. Ad esempio, è possibile specificare requisiti di protezione dell&#39;output diversi per ogni piattaforma client utilizzando la limitazione del modulo DRM con protezione dell&#39;output.

>[!NOTE]
>
>Per supportare la consegna di chiavi remote ai dispositivi iOS, il criterio utilizzato al momento della creazione del pacchetto deve avere la consegna di chiavi remote abilitata. Questa impostazione non può essere modificata tramite la configurazione tenant sul server. ***Adobe Primetime è richiesto per creare applicazioni iOS in grado di riprodurre contenuti protetti dall’accesso agli Adobi.***
