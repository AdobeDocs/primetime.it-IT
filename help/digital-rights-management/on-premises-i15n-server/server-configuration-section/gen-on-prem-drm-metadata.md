---
seo-title: Genera i metadati DRM dei locali attivati
title: Genera i metadati DRM dei locali attivati
uuid: 89d53924-1a8d-42d4-a716-ce4f4566b6bf
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Genera i metadati DRM dei locali attivati{#generate-the-on-premises-drm-metadata}

Un&#39; [!DNL CreateMetadata.jar] utilità è inclusa nella [!DNL create_metadata] cartella. Lo scopo di questa utility è quello di creare un Metadati DRM su richiesta che avvii il client a eseguire il processo di individualizzazione rispetto al server di individuazione locale specificato.

1. Aggiorna l&#39;implementazione di riferimento DRM di Primetime - Strumenti della riga di comando con i file seguenti:

   * [!DNL CreateMetadata.jar]
   * [!DNL commons-cli-1.2.jar]
   * [!DNL createMetadata.properties]

      I due file JAR possono risiedere nella [!DNL Command Line Tools/libs] cartella. Il [!DNL createMetadata.properties] file può risiedere accanto al [!DNL flashaccesstools.properties] file.

<!--<a id="example_2116349CA33642CD9293EAD94A532ED8"></a>-->

Included è uno [!DNL examplecreate.sh] script che illustra una creazione di metadati di esempio. Prima di generare i metadati, accertatevi di configurare l’URL del server licenze e dell’URL del server di individuazione sia nello script che nei file delle proprietà.

Gli input per l&#39;utilità sono i seguenti:

* `createMetadata.properties` - File delle proprietà contenente un Criterio predefinito, le posizioni del certificato e le password, ecc.
* `indivCert` - File PKCS12 contenente il certificato di trasporto dell&#39;individuazione
* `indivURL` - URL del server On Premises Individualization Server

Il file di output è un file di metadati DRM su richiesta che verrà utilizzato dal client DRM. Ad esempio:

```
java -jar libs/CreateMetadata.jar -c createMetadata.properties -indivCert i15n_transport.cer
-indivURL https://[YOURINDIVSERVER:PORT] onpremdrm.metadata
```

.