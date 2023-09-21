---
title: Generare i metadati DRM locali
description: Generare i metadati DRM locali
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# Generare i metadati DRM locali{#generate-the-on-premises-drm-metadata}

A [!DNL CreateMetadata.jar] l&#39;utilità è inclusa nel [!DNL create_metadata] cartella. Lo scopo di questa utility è quello di creare un Metadati DRM On Premises che avvierà il client nell&#39;esecuzione del processo di individualizzazione sul server di individualizzazione On Premises specificato.

1. Aggiornare Primetime DRM Reference Implementation - Command Line Tools con i file seguenti:

   * [!DNL CreateMetadata.jar]
   * [!DNL commons-cli-1.2.jar]
   * [!DNL createMetadata.properties]

     I due file JAR possono risiedere nel [!DNL Command Line Tools/libs] cartella. Il [!DNL createMetadata.properties] il file può trovarsi accanto al file [!DNL flashaccesstools.properties] file.

<!--<a id="example_2116349CA33642CD9293EAD94A532ED8"></a>-->

Incluso è un [!DNL examplecreate.sh] script che illustra un esempio di creazione di metadati. Prima di tentare di generare i metadati, è necessario configurare l&#39;URL del server licenze e l&#39;URL del server di personalizzazione sia nel file di script che in quello delle proprietà.

Gli input per l&#39;utilità sono i seguenti:

* `createMetadata.properties` : file di proprietà contenente un criterio predefinito, posizioni e password dei certificati, ecc.
* `indivCert` - File PKCS12 contenente il certificato di trasporto per l&#39;individuazione
* `indivURL` - URL del server di personalizzazione locale

Il file di output è un file di metadati DRM locale che verrà utilizzato dal client DRM. Ad esempio:

```
java -jar libs/CreateMetadata.jar -c createMetadata.properties -indivCert i15n_transport.cer
-indivURL https://[YOURINDIVSERVER:PORT] onpremdrm.metadata
```

.
