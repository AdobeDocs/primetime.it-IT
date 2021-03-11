---
title: Generare i metadati DRM dei locali attivi
description: Generare i metadati DRM dei locali attivi
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 1%

---


# Generare i metadati DRM dei locali in cui si trovano{#generate-the-on-premises-drm-metadata}

Un&#39;utilità [!DNL CreateMetadata.jar] è inclusa nella cartella [!DNL create_metadata]. Lo scopo di questa utility è quello di creare un metadati DRM dei locali attivi che avvierà il client a eseguire il processo di individualizzazione rispetto al server di Individualizzazione dei locali specificato.

1. Aggiorna l’implementazione di riferimento DRM di Primetime - Strumenti della riga di comando con i seguenti file:

   * [!DNL CreateMetadata.jar]
   * [!DNL commons-cli-1.2.jar]
   * [!DNL createMetadata.properties]

      I due file JAR possono risiedere nella cartella [!DNL Command Line Tools/libs] . Il file [!DNL createMetadata.properties] può trovarsi accanto al file [!DNL flashaccesstools.properties].

<!--<a id="example_2116349CA33642CD9293EAD94A532ED8"></a>-->

Incluso è uno script [!DNL examplecreate.sh] che illustra un esempio di creazione di metadati. Prima di generare i metadati, assicurati di configurare l’URL del server licenze e l’URL del server di Individualizzazione sia nei file di script che nelle proprietà.

Gli input per l&#39;utilità sono i seguenti:

* `createMetadata.properties` - File di proprietà contenente un criterio predefinito, posizioni del certificato e password, ecc.
* `indivCert` - File PKCS12 contenente il certificato di trasporto dell&#39;individuazione
* `indivURL` - URL del server di Individualization On Premises

Il file di output è un file di metadati DRM On Premises che verrà utilizzato dal client DRM. Ad esempio:

```
java -jar libs/CreateMetadata.jar -c createMetadata.properties -indivCert i15n_transport.cer
-indivURL https://[YOURINDIVSERVER:PORT] onpremdrm.metadata
```

.