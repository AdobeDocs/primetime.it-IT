---
title: Panoramica
description: Panoramica
copied-description: true
exl-id: 15733120-b1bb-46a7-90d2-4eb11c539d62
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# Panoramica  {#overview}

Utilizzando Adobe® Access™, i provider di contenuti possono applicare policy ai file multimediali. Utilizzando le API per la gestione dei criteri, gli amministratori possono creare, visualizzare i dettagli e aggiornare i criteri.

A *policy* definisce il modo in cui gli utenti possono visualizzare il contenuto; si tratta di una raccolta di informazioni che include impostazioni di protezione, requisiti di autenticazione e diritti di utilizzo. Quando vengono applicati i criteri, la crittografia e la firma consentono ai provider di contenuto di mantenere il controllo dei contenuti indipendentemente dalla loro diffusione. I file protetti possono essere consegnati utilizzando Adobe® Flash® Media Server o un server HTTP. Possono essere scaricati e riprodotti in lettori personalizzati creati con Adobe® AIR®, Adobe® Flash® Player e Adobe® Primetime SDK per iOS. Il criterio è un modello da utilizzare per il server licenze quando genera una licenza. Il client può inoltre fare riferimento al criterio prima di richiedere una licenza per determinare se è necessario richiedere all&#39;utente di eseguire l&#39;autenticazione prima di inviare una richiesta di licenza al server.

Un criterio specifica uno o più diritti concessi al client. In genere, una policy include, come minimo, il &quot;diritto di riproduzione&quot;. È inoltre possibile specificare più diritti di riproduzione, ciascuno con restrizioni diverse. Quando il client rileva una licenza con più diritti di riproduzione, utilizza la prima licenza per la quale soddisfa tutte le restrizioni. Ad esempio, questa funzione può essere utilizzata per applicare diverse impostazioni di protezione dell’output su piattaforme diverse. Per un codice di esempio che illustra questo esempio, consulta `CreatePolicyWithOutputProtection.java` nella directory &quot;samples&quot; degli strumenti della riga di comando per l’implementazione di riferimento.

Puoi eseguire le seguenti attività utilizzando le API di gestione dei criteri:

* Creare e aggiornare i criteri
* Visualizzare i dettagli dei criteri
* Gestire gli elenchi di aggiornamento dei criteri

Per informazioni dettagliate sull’API Java descritta in questo capitolo, consulta *Riferimento API per l’accesso agli Adobi*.

Per informazioni sull’implementazione di riferimento di Policy Manager, consulta *Utilizzo delle implementazioni di riferimento di accesso Adobe*.
