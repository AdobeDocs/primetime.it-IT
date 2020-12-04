---
seo-title: Proprietà delle cartelle esaminate
title: Proprietà delle cartelle esaminate
uuid: fc204bb4-033a-46fe-8642-737f6a4cd1f1
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# Proprietà cartella esaminata {#watched-folder-properties}

Ogni cartella esaminata contiene un file denominato [!DNL properties/watchfolder.properties]. Questo file contiene le opzioni di package per il contenuto inserito in questa cartella, compresi gli elementi da cifrare e i criteri da applicare. Eventuali modifiche apportate ai valori nel file delle proprietà avranno effetto alla successiva esecuzione del packager delle cartelle esaminate (non è necessario riavviare il server).

Se si verifica un errore di configurazione nel file delle proprietà del packager, il thread del packager si interrompe. Per riprendere il packager delle cartelle controllato, riavviate il server. Se si verifica un errore di configurazione in un file delle proprietà della cartella esaminata, la cartella esaminata viene temporaneamente rimossa dall&#39;elenco delle cartelle elaborate dal packager. Per aggiungere nuovamente la cartella esaminata all&#39;elenco, riavviate il server o modificate il file delle proprietà del packager. Se si verifica un errore durante la creazione di un pacchetto di un particolare file (ad esempio, perché il file è danneggiato), il file viene ignorato e i file rimanenti nella cartella vengono elaborati.
