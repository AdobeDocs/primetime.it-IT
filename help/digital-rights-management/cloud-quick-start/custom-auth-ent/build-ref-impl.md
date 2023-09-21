---
title: Creare l’implementazione di riferimento BEES
description: Creare l’implementazione di riferimento BEES
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---

# Creare l’implementazione di riferimento BEES {#build-the-bees-reference-implementation}

Assicurati di utilizzare Java 1.6.0_24 o versione successiva.
1. Compila i percorsi vuoti necessari, ad esempio `tomcatdir` e `fasterxmldir` in [!DNL build-bees.xml]

   FasterXML/Jackson è incluso. Puoi anche scaricarlo da [https://jar-download.com/artifacts/com.fasterxml.jackson.core](https://jar-download.com/artifacts/com.fasterxml.jackson.core).
1. Aggiorna i nomi file JAR effettivi in [!DNL build.common.xml] se desideri utilizzare una versione diversa delle librerie Jackson.
1. Esegui il `all` target di [!DNL build-bees.xml]:

   ```
   ant -f build-bees.xml
   ```

Il [!DNL bees.war] verrà creato in [!DNL bees-build/wars] cartella.
