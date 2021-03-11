---
title: File delle proprietà del pacchetto
description: File delle proprietà del pacchetto
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---


# File delle proprietà del pacchetto {#packager-properties-file}

Utilizza il file [!DNL flashaccess-refimpl-packager.properties] per configurare il componente Pacchetto cartelle controllate dell&#39;implementazione di riferimento. Come minimo, assicurati di impostare l’URL del server di licenza, il certificato del server di licenza, le credenziali del packager e le opzioni di protezione chiave. Questo file contiene anche il percorso di ogni cartella controllata (packager.watchfolder.source. `n`). Eventuali modifiche apportate ai valori in questo file di proprietà avranno effetto al successivo avvio del gestore di cartelle controllate (non è necessario riavviare il server). Tuttavia, se si verifica un errore di configurazione nel packager, il thread del packager di cartelle controllate verrà chiuso e il server dovrà essere riavviato per riavviare il thread del packager.
