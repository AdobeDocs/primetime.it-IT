---
seo-title: Configurare il percorso e il percorso di classe
title: Configurare il percorso e il percorso di classe
uuid: cf10fafa-125e-450c-83ae-60b990dab6b5
translation-type: tm+mt
source-git-commit: d8e4c39c297d69b154baf0b4d67cf09b5cf0a9d4
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 1%

---


# Configurare il percorso e il percorso di classe{#configure-the-path-and-classpath}

La [!DNL flashaccess.war] contiene [!DNL jsafeWithNative.jar], ovvero la libreria Crypto-J. Quest&#39;ultima richiede una libreria nativa aggiuntiva per eseguire operazioni di crittografia.

1. Aggiungete la libreria [!DNL jsafe] nativa al percorso.

   * **Linux /  [!DNL libjsafe.so] -** La directory che contiene  [!DNL libjsafe.so] deve trovarsi sul Percorso (le librerie Crypto-J native sono disponibili anche per altre piattaforme). Ad esempio, impostare [!DNL libjsafe.so] su `LD_LIBRARY_PATH`.

   * **Windows /  [!DNL jsafe.dll] -** La controparte di Windows a  [!DNL libjsafe.so] è la  [!DNL jsafe.dll]soluzione appropriata.
   Queste librerie sono disponibili nella cartella [!DNL thirdparty] della libreria.
1. Inserire uno dei file [!DNL adobe-flashaccess-certs] jar nel percorso di classe.

       Questo file JAR non è incluso nel file WAR; è necessario aggiungerlo esplicitamente al percorso di classe.
   
   * Server di sviluppo - Utilizzare solo [!DNL adobe-flashaccess-certs-prerelease.jar].
   * Server di produzione - Utilizzate solo [!DNL adobe-flashaccess- certs.jar]

La distribuzione include una cartella [!DNL shared] che include sia il file jar che un file [!DNL AdobeInitial.properties] preconfigurato.  Adobe consiglia di aggiungere questi elementi al file `common.loader` tramite il file [!DNL catalina.properties]. Ad esempio:

```
common.loader=<Any Pre-Existing Values>,${catalina.home}/shared/classes,${catalina.home}/shared/lib/*.jar
```


