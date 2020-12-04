---
description: 'È necessario configurare le proprietà del server in modo che riflettano il proprio ambiente. A tale scopo, potete effettuare le seguenti operazioni: '
seo-description: 'È necessario configurare le proprietà del server in modo che riflettano il proprio ambiente. A tale scopo, potete effettuare le seguenti operazioni: '
seo-title: Applicazione delle proprietà agli ambienti server
title: Applicazione delle proprietà agli ambienti server
uuid: a1ee0d6c-b5e7-4689-b7c8-b155176faf1c
translation-type: tm+mt
source-git-commit: d8e4c39c297d69b154baf0b4d67cf09b5cf0a9d4
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---


# Applicazione delle proprietà agli ambienti server{#apply-properties-to-server-environments}

È necessario configurare le proprietà del server in modo che riflettano il proprio ambiente. A questo scopo, potete effettuare le seguenti operazioni:

* [!DNL flashaccess-i15n.properties] - Esempi inclusi in ogni  [!DNL .war] file

* [!DNL AdobeInitial.properties] - Esempio presente nella  [!DNL /shared] cartella del DVD

   È possibile utilizzare questo file per ignorare le proprietà impostate nel file WAR come segue:

   1. Impostare i valori delle proprietà di sostituzione in [!DNL AdobeInitial.properties]
   1. Posizionare [!DNL AdobeInitial.properties] nel percorso di classe.

   >[!NOTE]
   >
   > Adobe consiglia di utilizzare il file [!DNL AdobeInitial.properties], in quanto questo consente di aggiornare i file WAR dell&#39;applicazione senza rischiare la perdita di qualsiasi configurazione di proprietà precedente che si potrebbe aver fatto nel file [!DNL flashaccess-i15n.properties].

* Meccanismo delle proprietà di sistema Java.

È possibile applicare singole proprietà a questi ambienti server specifici:

* *Sviluppo*
* *Staging*
* *Produzione*

Con questa funzionalità, è possibile utilizzare lo stesso file WAR per tutti gli ambienti server. Per applicare proprietà ad ambienti specifici, aggiungere due caratteri di sottolineatura (&#39; `__`&#39;) più uno dei seguenti codici di ambiente alla proprietà *name*:

    * `DEV`
    * `STAGE`
    * `PROD`

<!--<a id="example_A7A58E3EE8DA4114B4F7A9EEB69D50CA"></a>-->

Ad esempio, per impostare il livello di registro su `INFO` per i server di produzione e gestione temporanea e su `DEBUG` per il server di sviluppo:

```
log.Level=INFO  
log.Level__DEV=DEBUG 
```

Il server utilizza questo ordine di ricerca per le proprietà:

1. `propertyname_environment` in  [!DNL AdobeInitial.properties]

1. `propertyname_environment` in  [!DNL flashaccess-15n.properties]

1. `propertyname_environment` in Java System, proprietà
1. `propertyname` in  [!DNL AdobeInitial.properties]

1. `propertyname` in  [!DNL flashaccess-15n.properties]

1. `propertyname` in Java System, proprietà

>[!NOTE]
>
>È necessario specificare il nome dell&#39;ambiente del server come proprietà del sistema Java all&#39;avvio del server. Ad esempio, quando si avvia Tomcat con [!DNL catalina.bat], impostare la variabile di ambiente `CATALINA_OPTS` come segue:
>-DENVIRONMENT_NAME=[ DEV | FASE | PROD ]
