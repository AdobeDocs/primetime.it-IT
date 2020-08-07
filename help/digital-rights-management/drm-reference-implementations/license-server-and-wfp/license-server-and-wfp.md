---
description: Il server di implementazione di riferimento può essere utile per creare un server di licenze completamente funzionante che utilizza tutte le funzionalità dell'SDK Java  Adobe Primetime DRM.
seo-description: Il server di implementazione di riferimento può essere utile per creare un server di licenze completamente funzionante che utilizza tutte le funzionalità dell'SDK Java  Adobe Primetime DRM.
seo-title: Server licenze
title: Server licenze
uuid: 39cb0d0f-f3dc-48e9-b6fd-6960a9ade291
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---


# Server licenze {#license-server}

Il server di implementazione di riferimento può essere utile per creare un server di licenze completamente funzionante che utilizza tutte le funzionalità dell&#39;SDK Java  Adobe Primetime DRM.

In questa implementazione, gli utenti vengono autenticati in base alle voci degli utenti in un database. Il server include logica aziendale dimostrativa per il rilascio delle licenze e fornisce supporto per la compatibilità con Flash Media Rights Management Server 1.0 e 1.5.

## Requisiti del server di licenze {#license-server-requirements}

Requisiti del server licenze:

* Installare Tomcat 6.0 o versione successiva
* Installare un database, ad esempio MySQL (disponibile sul DVD, in [!DNL Third Party\MySQL])
* Verificare che sia installato Java 1.6 o versione successiva
* Per eseguire gli script di compilazione di esempio, verificare di disporre di Ant 1.8 o versione successiva

Dopo aver installato Tomcat e MySQL, contattate  Adobe per il set di credenziali DRM richieste.

## Creare il server licenze {#build-the-license-server}

>[!NOTE]
>
>La creazione del server licenze è necessaria solo se si intende modificare il codice sorgente. A scopo di valutazione, è possibile semplicemente utilizzare i file WAR come spedito.

Il server licenze di implementazione di riferimento include tutto il codice sorgente del server licenze ( `([DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\src/`), insieme a uno script di creazione Ant ( `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/build-refimpl.xml`) con cui è possibile personalizzare il server licenze in base alle proprie esigenze aziendali.

1. Modificate lo script di build Ant per specificare le posizioni dell&#39;SDK DRM Primetime, Tomcat, MySQL e Log4J.

   Aprite il [!DNL build-refimpl.xml] file in un editor di testo e impostate i seguenti valori di proprietà:

   * `sdkdir`
   * `tomcatdir`
   * `mysqldir`
   * `log4jdir`

1. Eseguire lo script Ant build con la `all` proprietà, nella directory in cui si trova lo script Ant build.

   ```
   ant -f build-refimpl.xml all
   ```

   Lo script Ant build crea una [!DNL refimpl-build/wars] directory che include i file WAR del server.
