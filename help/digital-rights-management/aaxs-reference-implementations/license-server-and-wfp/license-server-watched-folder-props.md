---
title: Proprietà delle cartelle controllate
description: Proprietà delle cartelle controllate
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# Proprietà delle cartelle controllate {#watched-folder-properties}

Ogni cartella controllata contiene un file denominato [!DNL properties/watchfolder.properties]. Questo file contiene le opzioni di pacchetto per il contenuto inserito in questa cartella, tra cui cosa cifrare e quali criteri applicare. Tutte le modifiche apportate ai valori nel file di proprietà hanno effetto alla successiva esecuzione del gestore di cartelle controllate (non è necessario riavviare il server).

Se si verifica un errore di configurazione nel file delle proprietà del packager, il thread del packager si arresta. Per riprendere il gestore cartelle controllate, riavviare il server. Se si verifica un errore di configurazione in un file delle proprietà della cartella controllata, la cartella controllata viene temporaneamente rimossa dall&#39;elenco delle cartelle che il packager elabora. Per aggiungere nuovamente la cartella controllata all&#39;elenco, riavviare il server o modificare il file delle proprietà del packager. Se si verifica un errore durante la creazione del pacchetto di un particolare file (ad esempio, perché il file è danneggiato), il file viene ignorato e i file rimanenti nella cartella vengono elaborati.
