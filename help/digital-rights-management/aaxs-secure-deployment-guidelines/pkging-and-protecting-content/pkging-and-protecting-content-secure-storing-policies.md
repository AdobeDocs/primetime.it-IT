---
title: Archiviazione sicura delle policy
description: Archiviazione sicura delle policy
copied-description: true
exl-id: fd335a0c-7eb1-4159-958f-7302fce98cef
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# Archiviazione sicura delle policy{#securely-storing-policies}

L’SDK per l’accesso agli Adobi offre una grande flessibilità nello sviluppo di applicazioni da utilizzare per la creazione di pacchetti di contenuti e policy. Durante la creazione di tali applicazioni, può essere utile consentire ad alcuni utenti di creare e modificare le policy e limitare altri utenti in modo che possano applicare le policy esistenti solo al contenuto. In questo caso, devi implementare i controlli di accesso necessari per creare account utente con privilegi diversi per la creazione di criteri e l’applicazione di criteri al contenuto.

I criteri non vengono firmati o protetti in altro modo da eventuali modifiche fino a quando non vengono utilizzati nel pacchetto. Se si è preoccupati degli utenti degli strumenti di creazione pacchetti che modificano i criteri, è consigliabile firmare i criteri per assicurarsi che non possano essere modificati.

Per ulteriori informazioni sulla creazione di applicazioni tramite l&#39;SDK, vedi *Riferimento API per l’accesso agli Adobi*.
