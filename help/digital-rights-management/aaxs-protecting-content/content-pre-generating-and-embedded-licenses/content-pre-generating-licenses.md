---
title: Pre-generazione delle licenze
description: Pre-generazione delle licenze
copied-description: true
exl-id: 2be8674c-736f-4ed3-b952-f661bf3ff48f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# Pre-generazione delle licenze{#pre-generating-licenses}

Per pregenerare le licenze, utilizza `com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()` per ottenere un&#39;istanza di `LicenseFactory`. È necessario specificare le credenziali del server licenze per firmare le licenze generate da questa factory. Questa classe supporta la generazione di licenze Leaf senza concatenamento licenze e licenze Leaf e Root con [Migliore concatenamento delle licenze](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-other-policy-options/content-enhanced-license-chaining.md).

Quando si genera una licenza Leaf, i metadati del contenuto devono essere specificati utilizzando `initContentInfo()`. Se i metadati includono più criteri o se desideri utilizzare un criterio che non era incluso nei metadati, utilizza `setSelectedPolicy()` per specificare il criterio da utilizzare per generare la licenza. Se si utilizza un Elenco aggiornamenti criteri per tenere traccia degli aggiornamenti ai criteri, è possibile fornire l&#39;Elenco aggiornamenti criteri alla License Factory prima di inizializzare i metadati utilizzando `setPolicyUpdateList()`.

Durante la generazione di una licenza Root, i metadati del contenuto possono essere specificati come descritto in precedenza. In alternativa, è possibile generare una licenza Root utilizzando un criterio ( `setSelectedPolicy()`) e URL del server licenze ( `setLicenseServerURL()`) al posto dei metadati.

>[!NOTE]
>
>L&#39;URL del server licenze è necessario anche se non esiste un Adobe di server licenze di accesso dal quale i client possano richiedere una licenza. In questo caso, l’URL del server licenze deve specificare un URL che identifichi l’emittente della licenza.

Se il criterio utilizza il concatenamento licenze avanzato, è necessario specificare una credenziale del server licenze per decrittografare la chiave di crittografia radice nel criterio ( `setRootKeyRetrievalInfo()`).

Se il criterio richiede una licenza associata al dominio, utilizzare `setDomainCAs()` per specificare gli autori del dominio da cui il server licenze accetterà i token di dominio. Per convalidare il destinatario della licenza, è necessario fornire uno o più certificati CA di dominio.

Se il criterio richiede la consegna della chiave remota per i dispositivi iOS, è necessario fornire il certificato del server chiavi utilizzando `setKeyServerCertificate()`, a meno che non venga generata una foglia concatenata.

Per generare una licenza, richiama `generateLicense()` e specificare il tipo di licenza (Leaf o Root) e uno o più certificati dei destinatari. Il certificato del destinatario sarà un certificato del computer o di dominio, a seconda dei requisiti specificati nel criterio. Se generi una foglia concatenata, non è necessario un destinatario. Dopo la generazione della licenza, è possibile ignorare le regole di utilizzo specificate nel criterio. Infine, richiamare `signLicense()` per firmare la licenza e ottenere un&#39;istanza di `PreGeneratedLicense`. È ora possibile salvare la licenza in un file (utilizzare `getBytes()` per recuperare la licenza serializzata) o incorporati in contenuto crittografato. Vedi, [Incorporazione delle licenze](../../aaxs-protecting-content/content-pre-generating-and-embedded-licenses/content-embedding-licenses.md).

Per un codice di esempio che illustra le licenze pregenerate, consulta `com.adobe.flashaccess.samples.licensegen.GenerateLicense` nella directory &quot;samples&quot; degli strumenti della riga di comando per l’implementazione di riferimento.
