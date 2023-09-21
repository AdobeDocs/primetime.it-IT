---
title: Proprietà cartella controllata
description: Proprietà cartella controllata
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# Proprietà cartella controllata {#watched-folder-properties}

Ogni cartella controllata contiene un file denominato [!DNL properties/watchfolder.properties]. Questo file contiene le opzioni di creazione pacchetti per il contenuto inserito in questa cartella, inclusi gli elementi da crittografare e i criteri da applicare. Qualsiasi modifica apportata ai valori nel file delle proprietà avrà effetto alla successiva esecuzione di Packager (non è necessario riavviare il server).

Se si verifica un errore di configurazione nel file delle proprietà del packager, il thread del packager si arresta. Per riprendere il programma di creazione pacchetti cartelle controllato, riavviare il server. Se si verifica un errore di configurazione in un file delle proprietà della cartella controllata, la cartella controllata viene temporaneamente rimossa dall&#39;elenco delle cartelle elaborate dal packager. Per aggiungere nuovamente la cartella controllata all&#39;elenco, riavviare il server o modificare il file delle proprietà del pacchetto. Se si verifica un errore durante la creazione del pacchetto di un determinato file (ad esempio, perché il file è danneggiato), il file viene ignorato e vengono elaborati i file rimanenti nella cartella.
