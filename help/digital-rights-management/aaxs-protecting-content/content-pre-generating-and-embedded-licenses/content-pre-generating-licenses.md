---
title: Licenze di pregenerazione
description: Licenze di pregenerazione
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# Licenze di pre-generazione{#pre-generating-licenses}

Per pregenerare le licenze, utilizza `com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()` per ottenere un&#39;istanza di `LicenseFactory`. È necessario specificare una credenziale del server licenze per firmare le licenze generate da questo factory. Questa classe supporta la generazione di licenze per foglia senza concatenamento licenze e licenze per foglia e radice con la [catena di licenze ottimizzata](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-other-policy-options/content-enhanced-license-chaining.md).

Quando si genera una licenza foglia, i metadati del contenuto devono essere specificati utilizzando `initContentInfo()`. Se i metadati includono più criteri o se desideri utilizzare un criterio non presente nei metadati, utilizza `setSelectedPolicy()` per specificare il criterio da utilizzare per generare la licenza. Se utilizzi un elenco di aggiornamento dei criteri per tenere traccia degli aggiornamenti dei criteri, puoi fornire l’elenco di aggiornamento dei criteri alla Fabbrica delle licenze prima di inizializzare i metadati utilizzando `setPolicyUpdateList()`.

Quando si genera una licenza Root, è possibile specificare i metadati del contenuto come descritto sopra. In alternativa, è possibile generare una licenza Root utilizzando un criterio ( `setSelectedPolicy()`) e l’URL del server di licenza ( `setLicenseServerURL()`) invece dei metadati.

>[!NOTE]
>
>È necessario un URL del server licenze anche se non esiste un server licenze di accesso Adobe da cui i client possono richiedere una licenza. In questo caso, l’URL del server licenze deve specificare un URL che identifichi l’emittente della licenza.

Se il criterio utilizza il concatenamento licenze avanzato, è necessario specificare una credenziale del server licenze per decrittografare la chiave di crittografia radice nel criterio ( `setRootKeyRetrievalInfo()`).

Se il criterio richiede una licenza associata a un dominio, utilizza `setDomainCAs()` per specificare gli emittenti di dominio da cui il server licenze accetterà i token di dominio. Per convalidare il destinatario della licenza, è necessario fornire uno o più certificati CA di dominio.

Se il criterio richiede la consegna di chiavi remote per i dispositivi iOS, è necessario fornire il certificato del server chiavi utilizzando `setKeyServerCertificate()`, a meno che non venga generata una foglia concatenata.

Per generare una licenza, richiamare `generateLicense()` e specificare il tipo di licenza (foglia o radice) e uno o più certificati dei destinatari. Il certificato destinatario sarà un certificato computer o un certificato di dominio, a seconda dei requisiti specificati nel criterio. Se si genera una foglia concatenata, un destinatario non è obbligatorio. Dopo la generazione della licenza, è possibile ignorare le regole di utilizzo specificate nel criterio. Infine, richiamare `signLicense()` per firmare la licenza e ottenere un&#39;istanza di `PreGeneratedLicense`. È ora possibile salvare la licenza in un file (utilizzare `getBytes()` per recuperare la licenza serializzata) o incorporarla in contenuto crittografato. Consulta [Incorporazione di licenze](../../aaxs-protecting-content/content-pre-generating-and-embedded-licenses/content-embedding-licenses.md).

Per un esempio di codice che illustra le licenze pregenerate, vedi `com.adobe.flashaccess.samples.licensegen.GenerateLicense` nella directory &quot;amples&quot; degli strumenti della riga di comando per l’implementazione di riferimento.
