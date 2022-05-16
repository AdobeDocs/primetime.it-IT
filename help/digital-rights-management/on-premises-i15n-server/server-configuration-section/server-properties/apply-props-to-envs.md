---
description: 'È necessario configurare le proprietà del server in modo che riflettano il proprio ambiente. Puoi eseguire questa operazione utilizzando uno dei seguenti '
title: Applicazione delle proprietà agli ambienti server
exl-id: 0c78011a-e8c8-43a8-8c2d-a5c4ed54a8d7
source-git-commit: 0019a95fa9ca6d21249533d559ce844897ab67cf
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Applicazione delle proprietà agli ambienti server{#apply-properties-to-server-environments}

È necessario configurare le proprietà del server in modo che riflettano il proprio ambiente. Puoi eseguire questa operazione utilizzando uno dei seguenti elementi:

* [!DNL flashaccess-i15n.properties] - Campioni inclusi in ciascuno dei [!DNL .war] file

* [!DNL AdobeInitial.properties] - Campione situato nel [!DNL /shared] cartella del DVD

   È possibile utilizzare questo file per ignorare le proprietà impostate nel file WAR come segue:

   1. Imposta i valori delle proprietà di override in [!DNL AdobeInitial.properties]
   1. Luogo [!DNL AdobeInitial.properties] sul percorso di classe.

   >[!NOTE]
   >
   >L&#39;Adobe consiglia di utilizzare [!DNL AdobeInitial.properties] file, poiché questo consente di aggiornare i file WAR dell&#39;applicazione senza rischiare la perdita di qualsiasi configurazione di configurazione della proprietà precedente che si può aver fatto nel [!DNL flashaccess-i15n.properties] file.

* Meccanismo delle proprietà del sistema Java.

È possibile applicare singole proprietà a questi specifici ambienti server:

* *Sviluppo*
* *Staging*
* *Produzione*

Con questa funzionalità, è possibile utilizzare lo stesso file WAR per tutti gli ambienti server. Per applicare proprietà a ambienti specifici, aggiungi due caratteri di sottolineatura (&#39; `__`&quot;) più uno dei seguenti codici dell&#39;ambiente alla proprietà *name*:

* `DEV`
* `STAGE`
* `PROD`

<!--<a id="example_A7A58E3EE8DA4114B4F7A9EEB69D50CA"></a>-->

Ad esempio, per impostare il livello di log su `INFO` per i server di produzione e di staging e `DEBUG` per il server di sviluppo:

```
log.Level=INFO  
log.Level__DEV=DEBUG 
```

Il server utilizza questo ordine di ricerca per le proprietà:

1. `propertyname_environment` in [!DNL AdobeInitial.properties]

1. `propertyname_environment` in [!DNL flashaccess-15n.properties]

1. `propertyname_environment` in Java System properties
1. `propertyname` in [!DNL AdobeInitial.properties]

1. `propertyname` in [!DNL flashaccess-15n.properties]

1. `propertyname` in Java System properties

>[!NOTE]
>
>È necessario specificare il nome dell&#39;ambiente del server come proprietà di sistema Java all&#39;avvio del server. Ad esempio, quando si avvia Tomcat con [!DNL catalina.bat], imposta le `CATALINA_OPTS` variabile di ambiente come segue:
>-DENVIRONMENT_NAME=[ DEV | FASE | PROD ]
