---
title: Creare l’implementazione di riferimento API
description: Creare l’implementazione di riferimento API
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---


# Creare l’implementazione di riferimento BEES {#build-the-bees-reference-implementation}

Assicurati di utilizzare Java 1.6.0_24 o versione successiva.
1. Compila i percorsi vuoti necessari, ad esempio `tomcatdir` e `fasterxmldir` in [!DNL build-bees.xml]

   XML/Jackson è incluso. Puoi anche scaricarlo da [https://jar-download.com/artifacts/com.fasterxml.jackson.core](https://jar-download.com/artifacts/com.fasterxml.jackson.core).
1. Aggiorna i nomi dei file jar effettivi in [!DNL build.common.xml] se desideri utilizzare una versione diversa delle librerie Jackson.
1. Esegui la destinazione `all` di [!DNL build-bees.xml]:

   ```
   ant -f build-bees.xml
   ```

La cartella [!DNL bees.war] verrà creata nella cartella [!DNL bees-build/wars].