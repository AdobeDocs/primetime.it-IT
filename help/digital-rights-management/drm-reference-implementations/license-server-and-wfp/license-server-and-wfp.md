---
description: Il server di implementazione di riferimento può essere utile per creare un server di licenza completamente funzionale che utilizzi tutte le funzioni dell’SDK Java DRM di Adobe Primetime.
title: Server licenze
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---


# Server licenze {#license-server}

Il server di implementazione di riferimento può essere utile per creare un server di licenza completamente funzionale che utilizzi tutte le funzioni dell’SDK Java DRM di Adobe Primetime.

In questa implementazione, gli utenti vengono autenticati in base alle voci utente in un database. Il server include logica di business dimostrativa per il rilascio delle licenze e fornisce supporto di compatibilità per Flash Media Rights Management Server 1.0 e 1.5.

## Requisiti del server licenze {#license-server-requirements}

Requisiti del server licenze:

* Installa Tomcat 6.0 o versione successiva
* Installa un database, ad esempio MySQL (disponibile sul DVD, in [!DNL Third Party\MySQL])
* Assicurati di aver installato Java 1.6 o versione successiva
* Per eseguire gli script di build di esempio, assicurati di disporre della versione 1.8 o successiva

Dopo aver installato Tomcat e MySQL, contattare l&#39;Adobe per il set di credenziali DRM richieste.

## Creare il server licenze {#build-the-license-server}

>[!NOTE]
>
>La creazione del server licenze è necessaria solo se si intende modificare il codice sorgente. A scopo di valutazione, è possibile semplicemente utilizzare i file WAR come spedito.

Il server licenze di implementazione di riferimento include tutto il codice sorgente del server licenze ( `([DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\src/`), insieme a uno script Ant build ( `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/build-refimpl.xml`) con cui è possibile personalizzare il server licenze in base alle proprie esigenze aziendali.

1. Modifica lo script della build Ant per specificare le posizioni dell&#39;SDK DRM di Primetime, Tomcat, MySQL e Log4J.

   Apri il file [!DNL build-refimpl.xml] in un editor di testo e imposta i seguenti valori di proprietà:

   * `sdkdir`
   * `tomcatdir`
   * `mysqldir`
   * `log4jdir`

1. Esegui lo script Ant build con la proprietà `all` nella directory in cui si trova lo script Ant build.

   ```
   ant -f build-refimpl.xml all
   ```

   Lo script Ant build crea una directory [!DNL refimpl-build/wars] che include i file WAR del server.
