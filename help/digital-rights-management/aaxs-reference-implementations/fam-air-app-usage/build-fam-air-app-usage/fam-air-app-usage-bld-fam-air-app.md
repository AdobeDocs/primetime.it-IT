---
title: Creazione dell’applicazione AIR di Flash Access Manager
description: Creazione dell’applicazione AIR di Flash Access Manager
copied-description: true
exl-id: f15fe9d2-d5e8-43ef-a1d5-1211752d54da
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# Creazione dell’applicazione AIR di Flash Access Manager {#building-the-flash-access-manager-air-application}

Per generare il file AIR di Flash Access Manager dal codice sorgente, è necessario che nel computer siano installati Flex e AIR SDK. Prima di creare un pacchetto ed eseguire l&#39;applicazione, è necessario compilare il codice MXML in un file SWF utilizzando [!DNL amxmlc] compilatore. Il [!DNL amxmlc] il compilatore si trova nella sezione [!DNL bin] directory dell’SDK di Flex 4 o versione successiva. Se lo desideri, puoi impostare la variabile di ambiente del percorso in modo da includere la directory bin dell’SDK di Flex per semplificare l’esecuzione delle utility sulla riga di comando.

Per generare il file AIR di Flash Access Manager, attenersi alla procedura descritta di seguito.

1. Apri una shell dei comandi o un terminale e passa alla cartella dei progetti dell’applicazione AIR di Flash Access Manager ( [!DNL UI Tools\Flash Access Manager] nella directory Reference Implementation).
1. Immetti il comando seguente:

   ```
   amxmlc src\FlashAccessmanager.mxml
   ```

   In esecuzione [!DNL amxmlc] produce [!DNL FlashAccessManager.swf], che contiene il codice compilato dell&#39;applicazione.

L’SDK di Adobe AIR include l’utility AIR Developer Tool (ADT) per creare pacchetti di applicazioni AIR e generare certificati. Le applicazioni AIR devono disporre di firma digitale. Gli utenti riceveranno un avviso durante l&#39;installazione di applicazioni non firmate correttamente o non firmate affatto. Per generare un certificato utilizzando la riga di comando, apri una finestra della console nella stessa cartella dell’applicazione AIR e digita quanto segue:

```
adt -certificate -cn SelfSigned 1024-RSA testCert.pfx  
<i class="+ topic ph hi-d="" i "="">
  some_password 
</i class="+ topic>
```

Sostituisci *some_password* con una password di tua scelta. Dopo alcuni secondi, l’ADT dovrebbe completare il processo di generazione del certificato e dovrebbe essere disponibile un nuovo [!DNL testCert.pfx] nella directory dell&#39;applicazione.

Quindi, utilizzare ADT per creare il pacchetto dell&#39;applicazione in un [!DNL .air] mediante il comando:

```
adt -package -storetype pkcs12 -keystore testCert.pfx FlashAccessManager.air src\FlashAccessManager-app.xml . -C src assets
```

Questo comando indica ad ADT di creare un pacchetto dell&#39;applicazione utilizzando il file di chiave in [!DNL testCert.pfx]. Nella riga precedente, configura ADT per creare un pacchetto dell’intera applicazione in un file denominato [!DNL FlashAccessManager.air], e per includere i file [!DNL FlashAccessManager-app.xml] e [!DNL FlashAccessManager.swf] e le immagini dalla directory assets.

Durante questo processo verrà richiesta la password impostata per il nuovo file di certificato. Immettilo, aspetta un attimo, e un [!DNL FlashAccessManager.air] deve trovarsi nella stessa directory dei file di progetto.
