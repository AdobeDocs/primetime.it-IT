---
description: Devi configurare le proprietà del server in modo che riflettano il tuo ambiente. Puoi eseguire questa operazione utilizzando uno dei seguenti elementi
title: Applicare le proprietà agli ambienti server
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# Applicare le proprietà agli ambienti server{#apply-properties-to-server-environments}

Devi configurare le proprietà del server in modo che riflettano il tuo ambiente. Puoi eseguire questa operazione utilizzando uno dei seguenti elementi:

* [!DNL flashaccess-i15n.properties] - Campioni inclusi in ciascuno dei [!DNL .war] file

* [!DNL AdobeInitial.properties] - Campione situato nella [!DNL /shared] cartella sul DVD

  È possibile utilizzare questo file per sostituire le proprietà impostate nel file WAR nel modo seguente:

   1. Impostare i valori delle proprietà di sostituzione in [!DNL AdobeInitial.properties]
   1. Luogo [!DNL AdobeInitial.properties] nel percorso di classe.

  >[!NOTE]
  >
  >L’Adobe consiglia di utilizzare [!DNL AdobeInitial.properties] , poiché questo consente di aggiornare i file WAR dell&#39;applicazione senza rischiare di perdere eventuali configurazioni di proprietà precedenti eseguite in [!DNL flashaccess-i15n.properties] file.

* Meccanismo di proprietà del sistema Java.

Puoi applicare singole proprietà a questi ambienti server specifici:

* *Sviluppo*
* *Staging*
* *Produzione*

Con questa funzionalità, è possibile utilizzare lo stesso file WAR per tutti gli ambienti server. Per applicare le proprietà a ambienti specifici, aggiungi due caratteri di sottolineatura (&#39; `__`&#39;) più uno dei seguenti codici di ambiente alla proprietà *nome*:

* `DEV`
* `STAGE`
* `PROD`

<!--<a id="example_A7A58E3EE8DA4114B4F7A9EEB69D50CA"></a>-->

Ad esempio, per impostare il livello di registro su `INFO` per i server di produzione e di staging e per `DEBUG` per il server di sviluppo:

```
log.Level=INFO  
log.Level__DEV=DEBUG 
```

Il server utilizza questo ordine di ricerca per le proprietà:

1. `propertyname_environment` in [!DNL AdobeInitial.properties]

1. `propertyname_environment` in [!DNL flashaccess-15n.properties]

1. `propertyname_environment` nelle proprietà del sistema Java
1. `propertyname` in [!DNL AdobeInitial.properties]

1. `propertyname` in [!DNL flashaccess-15n.properties]

1. `propertyname` nelle proprietà del sistema Java

>[!NOTE]
>
>All’avvio del server è necessario specificare il nome dell’ambiente del server come proprietà del sistema Java. Ad esempio, quando si avvia Tomcat con [!DNL catalina.bat], imposta `CATALINA_OPTS` variabile di ambiente come segue:
>-DENVIRONMENT_NAME=[DEV | FASE PROD]
