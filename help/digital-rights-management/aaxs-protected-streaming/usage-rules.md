---
seo-title: Regole di utilizzo
title: Regole di utilizzo
uuid: 361d07b9-e4c8-47ab-8c45-a1de98c9fed7
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# Regole di utilizzo{#usage-rules}

Con Adobe Access Server per lo streaming protetto, tutte le regole di utilizzo vengono specificate sul server tramite i file di configurazione. Eventuali regole di utilizzo specificate nel contenuto protetto vengono ignorate, pertanto si consiglia di utilizzare un semplice criterio anonimo durante la creazione del pacchetto di contenuto. Le regole di utilizzo configurabili possono essere impostate per ogni tenant.

Adobe Access Server for Protected Streaming supporta le seguenti regole di utilizzo:

* Protezione dell&#39;output
*  limitazioni delle applicazioni Adobe® AIR®, SWF, iOS e Android
* Limitazioni per i moduli DRM e Runtime
* Applicazione del rilevamento Jailbreak (sulle piattaforme di accesso  Adobe che supportano il rilevamento Jailbreak)
* La memorizzazione della cache delle licenze è disabilitata per impostazione predefinita. Il caching delle licenze può essere attivato specificando la data di fine del caching o un periodo di tempo consentito (a partire dal momento del rilascio della licenza).
* Più diritti di riproduzione, che consentono di specificare diverse combinazioni di Protezione output, Restrizioni applicazione e Limitazioni DRM/Runtime. Ad esempio, è possibile specificare diversi requisiti di protezione dell&#39;output per ogni piattaforma client utilizzando la limitazione del modulo DRM con Protezione dell&#39;output.

>[!NOTE]
>
>Per supportare la consegna di chiavi remote ai dispositivi iOS, il criterio utilizzato al momento della creazione del pacchetto deve avere la consegna di chiavi remote abilitata. Questa impostazione non può essere modificata tramite la configurazione tenant sul server. ***Adobe Primetime è richiesto per creare applicazioni iOS in grado di riprodurre  contenuto protetto da accesso al Adobe.***

