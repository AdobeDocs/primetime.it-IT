---
description: 'È necessario configurare le proprietà del server in modo che riflettano il proprio ambiente. Puoi eseguire questa operazione utilizzando uno dei seguenti '
title: Applicazione delle proprietà agli ambienti server
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# Applicare proprietà agli ambienti server{#apply-properties-to-server-environments}

È necessario configurare le proprietà del server in modo che riflettano il proprio ambiente. Puoi eseguire questa operazione utilizzando una delle seguenti opzioni:

* [!DNL flashaccess-i15n.properties] - Esempi inclusi in ciascuno dei  [!DNL .war] file

* [!DNL AdobeInitial.properties] - Campione situato nella  [!DNL /shared] cartella del DVD

   È possibile utilizzare questo file per ignorare le proprietà impostate nel file WAR come segue:

   1. Imposta i valori delle proprietà di override in [!DNL AdobeInitial.properties]
   1. Posiziona [!DNL AdobeInitial.properties] sul percorso di classe.

   >[!NOTE]
   >
   >L&#39;Adobe consiglia di utilizzare il file [!DNL AdobeInitial.properties], in quanto questo consente di aggiornare i file WAR dell&#39;applicazione senza rischiare la perdita di eventuali impostazioni di configurazione delle proprietà precedenti che si possono aver eseguito nel file [!DNL flashaccess-i15n.properties].

* Meccanismo delle proprietà del sistema Java.

È possibile applicare singole proprietà a questi specifici ambienti server:

* *Sviluppo*
* *Staging*
* *Produzione*

Con questa funzionalità, è possibile utilizzare lo stesso file WAR per tutti gli ambienti server. Per applicare proprietà a ambienti specifici, aggiungi due caratteri di sottolineatura (&#39; `__`&#39;) più uno dei seguenti codici di ambiente alla proprietà *name*:

    * `DEV`
    * `STAGE`
    * `PROD`

<!--<a id="example_A7A58E3EE8DA4114B4F7A9EEB69D50CA"></a>-->

Ad esempio, per impostare il livello di registro su `INFO` per i server di produzione e di staging e su `DEBUG` per il server di sviluppo:

```
log.Level=INFO  
log.Level__DEV=DEBUG 
```

Il server utilizza questo ordine di ricerca per le proprietà:

1. `propertyname_environment` in  [!DNL AdobeInitial.properties]

1. `propertyname_environment` in  [!DNL flashaccess-15n.properties]

1. `propertyname_environment` in Java System properties
1. `propertyname` in  [!DNL AdobeInitial.properties]

1. `propertyname` in  [!DNL flashaccess-15n.properties]

1. `propertyname` in Java System properties

>[!NOTE]
>
>È necessario specificare il nome dell&#39;ambiente del server come proprietà di sistema Java all&#39;avvio del server. Ad esempio, quando si avvia Tomcat con [!DNL catalina.bat], impostare la variabile di ambiente `CATALINA_OPTS` come segue:
>-DENVIRONMENT_NAME=[ DEV | FASE | PROD ]
