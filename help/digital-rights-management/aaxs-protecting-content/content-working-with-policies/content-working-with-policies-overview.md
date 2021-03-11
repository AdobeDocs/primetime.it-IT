---
title: Panoramica
description: Panoramica
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---


# Panoramica {#overview}

Utilizzando Adobe® Access™, i fornitori di contenuti possono applicare criteri ai file multimediali. Utilizzando le API di gestione dei criteri, gli amministratori possono creare, visualizzare i dettagli e aggiornare i criteri.

Una *policy* definisce come gli utenti possono visualizzare il contenuto; è una raccolta di informazioni che include impostazioni di protezione, requisiti di autenticazione e diritti di utilizzo. Quando vengono applicati i criteri, la crittografia e la firma consentono ai fornitori di contenuti di mantenere il controllo dei contenuti indipendentemente dalla loro diffusione. I file protetti possono essere consegnati utilizzando Adobe® Flash® Media Server o un server HTTP. Possono essere scaricati e riprodotti in lettori personalizzati costruiti con Adobe® AIR®, Adobe® Flash® Player e Adobe® Primetime SDK per iOS. Il criterio è un modello per il server licenze da utilizzare quando genera una licenza. Il client può anche fare riferimento al criterio prima di richiedere una licenza per determinare se è necessario richiedere all&#39;utente di eseguire l&#39;autenticazione prima di emettere una richiesta di licenza al server.

Un criterio specifica uno o più diritti concessi al client. In genere, un criterio include almeno il &quot;diritto di riproduzione&quot;. È inoltre possibile specificare più diritti di riproduzione, ciascuno con diverse restrizioni. Quando il cliente trova una licenza con più diritti di riproduzione, utilizza la prima per la quale soddisfa tutte le restrizioni. Ad esempio, questa funzione può essere utilizzata per applicare diverse impostazioni di protezione dell’output su piattaforme diverse. Per un esempio di codice che illustra questo esempio, vedi `CreatePolicyWithOutputProtection.java` nella directory &quot;amples&quot; degli strumenti della riga di comando per l’implementazione di riferimento.

Puoi eseguire le seguenti attività utilizzando le API di gestione dei criteri:

* Creare e aggiornare i criteri
* Visualizza dettagli criteri
* Gestisci elenchi di aggiornamenti dei criteri

Per informazioni dettagliate sull&#39;API Java discussa in questo capitolo, consulta *Riferimento API di accesso agli Adobi*.

Per informazioni sull&#39;implementazione di riferimento di Policy Manager, consulta *Utilizzo delle implementazioni di riferimento di accesso Adobe*.
