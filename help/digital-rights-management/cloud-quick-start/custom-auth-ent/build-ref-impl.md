---
seo-title: Creare l'implementazione di riferimento API
title: Creare l'implementazione di riferimento API
uuid: c9358188-e626-4f99-a02c-4928b06d6ae2
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---


# Creare l&#39;implementazione di riferimento BEES {#build-the-bees-reference-implementation}

Assicurarsi di utilizzare Java 1.6.0_24 o versione successiva.
1. Compilare i percorsi vuoti necessari, ad esempio `tomcatdir` e `fasterxmldir` in [!DNL build-bees.xml]

   Più veloceXML/Jackson è incluso. È inoltre possibile scaricarlo da [https://jar-download.com/artifacts/com.fasterxml.jackson.core](https://jar-download.com/artifacts/com.fasterxml.jackson.core).
1. Aggiornate i nomi dei file jar effettivi in [!DNL build.common.xml] se desiderate utilizzare una versione diversa delle librerie Jackson.
1. Eseguire la destinazione `all` di [!DNL build-bees.xml]:

   ```
   ant -f build-bees.xml
   ```

La cartella [!DNL bees.war] verrà creata nella cartella [!DNL bees-build/wars].