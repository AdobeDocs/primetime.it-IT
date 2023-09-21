---
description: Il server di implementazione di riferimento può essere utile per creare un server licenze completamente funzionante che utilizza tutte le funzioni dell’SDK Java di Adobe Primetime DRM.
title: Server licenze
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# Server licenze {#license-server}

Il server di implementazione di riferimento può essere utile per creare un server licenze completamente funzionante che utilizza tutte le funzioni dell’SDK Java di Adobe Primetime DRM.

In questa implementazione, gli utenti vengono autenticati in base alle voci utente in un database. Il server include una dimostrazione della logica di business per il rilascio delle licenze e fornisce supporto per la compatibilità con Flash Media Rights Management Server 1.0 e 1.5.

## Requisiti del server di licenze {#license-server-requirements}

Requisiti del server licenze:

* Installare Tomcat 6.0 o versione successiva
* Installare un database, ad esempio MySQL (disponibile nel DVD, in [!DNL Third Party\MySQL])
* Verifica che Java 1.6 o versione successiva sia installato
* Per eseguire gli script di build di esempio, assicurati di disporre di Ant 1.8 o versione successiva

Dopo aver installato Tomcat e MySQL, contattare l&#39;Adobe per il set di credenziali DRM richieste.

## Creare il server licenze {#build-the-license-server}

>[!NOTE]
>
>La creazione del server licenze è necessaria solo se si desidera modificare il codice sorgente. A scopo di valutazione, è sufficiente utilizzare i file WAR come spediti.

Il server licenze di implementazione di riferimento include tutto il codice sorgente del server licenze ( `([DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\src/`), insieme a uno script di generazione della formica ( `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/build-refimpl.xml`) con cui è possibile personalizzare il server licenze in base alle proprie esigenze aziendali.

1. Modificate lo script di creazione della formica per specificare le posizioni dell&#39;SDK di Primetime DRM, Tomcat, MySQL e Log4J.

   Apri [!DNL build-refimpl.xml] in un editor di testo e impostare i seguenti valori di proprietà:

   * `sdkdir`
   * `tomcatdir`
   * `mysqldir`
   * `log4jdir`

1. Esegui lo script di generazione della formica con `all` , nella directory in cui si trova lo script di generazione Ant.

   ```
   ant -f build-refimpl.xml all
   ```

   Lo script di creazione della formica crea un [!DNL refimpl-build/wars] che include i file WAR del server.
