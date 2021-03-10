---
title: Regole di utilizzo
description: Regole di utilizzo
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# Regole di utilizzo{#usage-rules}

Con Adobe Access Server per lo streaming protetto, tutte le regole di utilizzo vengono specificate sul server tramite i file di configurazione. Tutte le regole di utilizzo specificate nel contenuto protetto vengono ignorate, pertanto si consiglia di utilizzare una semplice policy anonima durante la creazione dei contenuti. Le regole di utilizzo configurabili possono essere impostate per tenant.

Adobe Access Server per lo streaming protetto supporta le seguenti regole di utilizzo:

* Protezione dell&#39;uscita
* Restrizioni per applicazioni Adobe® AIR®, SWF, iOS e Android
* Restrizioni al modulo DRM e runtime
* Applicazione del rilevamento Jailbreak (su piattaforme di accesso Adobe che supportano il rilevamento jailbreak)
* Il caching delle licenze è disattivato per impostazione predefinita. È possibile abilitare il caching delle licenze specificando la data di fine del caching o una quantità di tempo di memorizzazione nella cache consentita (a partire dal momento del rilascio della licenza).
* Diritti di riproduzione multipli, che consentono di specificare diverse combinazioni di Protezione output, Restrizioni applicazione e Restrizioni DRM/Runtime. Ad esempio, è possibile specificare diversi requisiti di protezione dell&#39;output per ciascuna piattaforma client utilizzando la limitazione del modulo DRM con protezione dell&#39;output.

>[!NOTE]
>
>Per supportare la consegna di chiavi remote ai dispositivi iOS, i criteri utilizzati al momento del packaging devono avere la consegna di chiavi remote abilitata. Impossibile modificare questa impostazione tramite la configurazione tenant sul server. ***Adobe Primetime è necessario per creare applicazioni iOS in grado di riprodurre contenuti protetti da Adobe Access.***

