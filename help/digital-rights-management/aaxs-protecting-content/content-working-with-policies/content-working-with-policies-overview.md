---
seo-title: Panoramica
title: Panoramica
uuid: 7363d241-6947-4a9c-80e5-e50be71066b9
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---


# Panoramica {#overview}

Utilizzando  Adobe® Access™, i fornitori di contenuti possono applicare criteri ai file multimediali. Utilizzando le API di gestione dei criteri, gli amministratori possono creare, visualizzare i dettagli e aggiornare i criteri.

Una *policy* definisce il modo in cui gli utenti possono visualizzare il contenuto; è una raccolta di informazioni che include impostazioni di protezione, requisiti di autenticazione e diritti di utilizzo. Quando vengono applicati i criteri, la cifratura e la firma consentono ai fornitori di contenuti di mantenere il controllo dei contenuti indipendentemente dalla loro diffusione. I file protetti possono essere distribuiti utilizzando  Adobe® Flash® Media Server o un server HTTP. Possono essere scaricati e riprodotti in lettori personalizzati creati con  Adobe® AIR®,  Adobe® Flash Player e  Adobe® Primetime SDK per iOS. Il criterio è un modello che il server licenze può utilizzare quando genera una licenza. Il client può anche fare riferimento al criterio prima di richiedere una licenza per determinare se è necessario richiedere all&#39;utente di eseguire l&#39;autenticazione prima di inviare una richiesta di licenza al server.

Un criterio specifica uno o più diritti concessi al client. In genere, un criterio include almeno &quot;Play Right&quot;. È inoltre possibile specificare più diritti di riproduzione, ciascuno con diverse limitazioni. Quando il client rileva una licenza con più diritti di riproduzione, utilizza il primo per il quale soddisfa tutte le restrizioni. Ad esempio, questa funzione può essere utilizzata per applicare diverse impostazioni di protezione dell&#39;output su piattaforme diverse. Per un esempio di codice che illustra questo esempio, vedere `CreatePolicyWithOutputProtection.java` nella directory &quot;samples&quot; degli strumenti della riga di comando per l&#39;implementazione di riferimento.

Potete eseguire le seguenti attività utilizzando le API di gestione dei criteri:

* Creare e aggiornare criteri
* Visualizza dettagli criteri
* Gestire gli elenchi di aggiornamento dei criteri

Per informazioni dettagliate sulle API Java discusse in questo capitolo, consultate *Riferimento API di accesso ai Adobi*.

Per informazioni sull&#39;implementazione di riferimento di Policy Manager, vedere *Utilizzo delle implementazioni di riferimento di accesso al Adobe*.
