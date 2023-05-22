---
title: File delle proprietà del Packager
description: File delle proprietà del Packager
copied-description: true
exl-id: 7d78576b-fd77-460d-92d9-c2e69e37006e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---

# File delle proprietà del Packager {#packager-properties-file}

Utilizza il [!DNL flashaccess-refimpl-packager.properties] per configurare il componente Packager delle cartelle controllate dell’implementazione di riferimento. Impostare almeno l&#39;URL del server licenze, il certificato del server licenze, le credenziali del packager e le opzioni di protezione delle chiavi. Questo file contiene anche il percorso di ogni cartella controllata (packager.watchfolder.source. `n`). Eventuali modifiche apportate ai valori di questo file di proprietà avranno effetto alla successiva esecuzione del programma di creazione pacchetti cartelle controllato (non è necessario riavviare il server). Tuttavia, se si verifica un errore di configurazione nel packager, il thread del packager della cartella controllata verrà chiuso e il server dovrà essere riavviato per riavviare il thread del packager.
