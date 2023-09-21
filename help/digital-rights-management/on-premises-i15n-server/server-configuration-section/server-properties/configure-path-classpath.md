---
title: Configurare il percorso e il percorso di classe
description: Configurare il percorso e il percorso di classe
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# Configurare il percorso e il percorso di classe{#configure-the-path-and-classpath}

Il [!DNL flashaccess.war] contiene [!DNL jsafeWithNative.jar], che è la libreria Crypto-J. Quest&#39;ultimo richiede una libreria nativa aggiuntiva per eseguire operazioni di crittografia.

1. Aggiungi il nativo [!DNL jsafe] nel percorso.

   * **Linux/ [!DNL libjsafe.so] -** La directory contenente [!DNL libjsafe.so] deve trovarsi sul percorso (le librerie Crypto-J native sono disponibili anche per altre piattaforme). Ad esempio, imposta [!DNL libjsafe.so] il `LD_LIBRARY_PATH`.

   * **Windows / [!DNL jsafe.dll] -** La controparte di Windows a [!DNL libjsafe.so] è appropriato [!DNL jsafe.dll].

   Queste librerie sono disponibili nel [!DNL thirdparty] cartella della libreria.
1. Inserisci uno dei [!DNL adobe-flashaccess-certs] file jar nel percorso di classe.

       Questo file JAR non è incluso nel file WAR; devi aggiungerlo esplicitamente al classpath.
   
   * Server di sviluppo - Da utilizzare solo [!DNL adobe-flashaccess-certs-prerelease.jar].
   * Server di produzione - Da utilizzare solo [!DNL adobe-flashaccess- certs.jar]

La distribuzione include [!DNL shared] che include sia il file jar che una cartella preconfigurata [!DNL AdobeInitial.properties] file. L’Adobe consiglia di aggiungere questi elementi al `common.loader` tramite [!DNL catalina.properties] file. Ad esempio:

```
common.loader=<Any Pre-Existing Values>,${catalina.home}/shared/classes,${catalina.home}/shared/lib/*.jar
```
