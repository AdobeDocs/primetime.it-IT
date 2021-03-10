---
title: Configurare il percorso e il percorso di classe
description: Configurare il percorso e il percorso di classe
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 1%

---


# Configura il percorso e il percorso classico{#configure-the-path-and-classpath}

Il [!DNL flashaccess.war] contiene [!DNL jsafeWithNative.jar], che è la libreria Crypto-J. Quest&#39;ultima richiede una libreria nativa aggiuntiva per eseguire operazioni di crittografia.

1. Aggiungi la libreria [!DNL jsafe] nativa al percorso.

   * **Linux /  [!DNL libjsafe.so] -** La directory contenente  [!DNL libjsafe.so] deve trovarsi sul percorso (le librerie native Crypto-J sono disponibili anche per altre piattaforme). Ad esempio, impostare [!DNL libjsafe.so] su `LD_LIBRARY_PATH`.

   * **Windows /  [!DNL jsafe.dll] -** La controparte su Windows  [!DNL libjsafe.so] è la appropriata  [!DNL jsafe.dll].
   Queste librerie sono disponibili nella cartella della libreria [!DNL thirdparty] .
1. Inserisci uno dei file jar [!DNL adobe-flashaccess-certs] nel percorso di classe.

       Questo file JAR non è incluso nel file WAR; devi aggiungerlo esplicitamente al percorso classe.
   
   * Server di sviluppo - Deve utilizzare solo [!DNL adobe-flashaccess-certs-prerelease.jar].
   * Server di produzione - Utilizza solo [!DNL adobe-flashaccess- certs.jar]

La distribuzione include una cartella [!DNL shared] che include sia il file jar che un file [!DNL AdobeInitial.properties] preconfigurato. Adobe consiglia di aggiungere questi elementi al file `common.loader` tramite il file [!DNL catalina.properties]. Ad esempio:

```
common.loader=<Any Pre-Existing Values>,${catalina.home}/shared/classes,${catalina.home}/shared/lib/*.jar
```


