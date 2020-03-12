---
seo-title: Criteri di memorizzazione sicura
title: Criteri di memorizzazione sicura
uuid: b1ac236f-6637-46d4-8405-a819d6093314
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Criteri di memorizzazione sicura{#securely-storing-policies}

Adobe Access SDK offre una grande flessibilità nello sviluppo di applicazioni da utilizzare per la creazione di pacchetti di contenuti e per la creazione di criteri. Quando create tali applicazioni, potete consentire ad alcuni utenti di creare e modificare i criteri e limitare altri utenti in modo che possano applicare solo i criteri esistenti al contenuto. In questo caso, è necessario implementare i controlli di accesso necessari per creare account utente con privilegi diversi per la creazione dei criteri e l&#39;applicazione dei criteri ai contenuti.

I criteri non vengono firmati o altrimenti protetti dalla modifica finché non vengono utilizzati nella creazione dei pacchetti. Se siete preoccupati per gli utenti dei vostri strumenti di imballaggio che modificano i criteri, dovreste considerare la possibilità di firmare i criteri in modo che non possano essere modificati.

Per ulteriori informazioni sulla creazione di applicazioni mediante l&#39;SDK, consulta il Riferimento *API di* Adobe Access.
