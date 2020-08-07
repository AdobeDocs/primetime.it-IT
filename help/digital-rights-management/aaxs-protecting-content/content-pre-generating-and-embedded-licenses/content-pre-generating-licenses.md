---
seo-title: Licenze di pre-generazione
title: Licenze di pre-generazione
uuid: 31430753-11f1-4ce5-b402-cf4279119a05
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# Licenze di pre-generazione{#pre-generating-licenses}

Per pre-generare le licenze, utilizzare `com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()` per ottenere un&#39;istanza di `LicenseFactory`. Per firmare le licenze generate da questo factory, è necessario specificare una credenziale Server licenze. Questa classe supporta la generazione di licenze Leaf senza concatenamento licenze e licenze Leaf e Root con concatenamento [Enhanced](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-other-policy-options/content-enhanced-license-chaining.md).

Durante la generazione di una licenza Leaf, i metadati del contenuto devono essere specificati utilizzando `initContentInfo()`. Se i metadati includono più criteri, o se desiderate utilizzare un criterio che non era presente nei metadati, utilizzate `setSelectedPolicy()` per specificare il criterio da utilizzare per generare la licenza. Se utilizzate un elenco di aggiornamento criteri per tenere traccia degli aggiornamenti ai criteri, potete fornire l&#39;elenco di aggiornamento criteri al License Factory prima di inizializzare i metadati utilizzando `setPolicyUpdateList()`.

Quando si genera una licenza Root, i metadati del contenuto possono essere specificati come descritto sopra. In alternativa, è possibile generare una licenza radice utilizzando un criterio ( `setSelectedPolicy()`) e l&#39;URL del server della licenza ( `setLicenseServerURL()`) invece dei metadati.

>[!NOTE]
>
>È necessario un URL del server licenze anche se non è presente  server licenze di accesso Adobe dal quale i client possono richiedere una licenza. In questo caso, l&#39;URL del server licenze deve specificare un URL che identifica l&#39;emittente della licenza.

Se il criterio utilizza il concatenamento licenze avanzato, è necessario specificare una credenziale del server licenze per decrittografare la chiave di crittografia principale nel criterio ( `setRootKeyRetrievalInfo()`).

Se il criterio richiede una licenza associata a un dominio, utilizzare `setDomainCAs()` per specificare gli emittenti di dominio da cui il server licenze accetterà i token di dominio. Per convalidare il destinatario della licenza, è necessario specificare uno o più certificati CA di dominio.

Se il criterio richiede la consegna di chiavi remote per i dispositivi iOS, è necessario fornire il certificato Server chiavi utilizzando `setKeyServerCertificate()`, a meno che non venga generata una foglia concatenata.

Per generare una licenza, richiamare `generateLicense()` e specificare il tipo di licenza (foglia o radice) e uno o più certificati del destinatario. Il certificato destinatario sarà un certificato computer o un certificato di dominio, a seconda dei requisiti specificati nel criterio. Se si genera una foglia concatenata, il destinatario non è obbligatorio. Una volta generata la licenza, è possibile ignorare le regole di utilizzo specificate nel criterio. Infine, invocare `signLicense()` per firmare la licenza e ottenere un&#39;istanza di `PreGeneratedLicense`. È ora possibile salvare la licenza in un file (da utilizzare `getBytes()` per recuperare la licenza serializzata) o incorporarla in contenuto crittografato. Consultate, [Incorporazione di licenze](../../aaxs-protecting-content/content-pre-generating-and-embedded-licenses/content-embedding-licenses.md).

Per un esempio di codice che illustra le licenze pregenerate, vedere `com.adobe.flashaccess.samples.licensegen.GenerateLicense` nella directory &quot;samples&quot; degli strumenti della riga di comando per l’implementazione di riferimento.
