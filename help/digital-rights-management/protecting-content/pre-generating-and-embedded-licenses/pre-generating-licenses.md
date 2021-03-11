---
description: Se utilizzi Adobe Primetime DRM Professional, puoi pregenerare licenze e incorporare licenze nei contenuti. Questa funzione può essere combinata con il concatenamento licenze avanzato, in modo tale che una licenza Leaf sia pregenerata e incorporata nel contenuto, e il client può richiedere una licenza Root (associata a una macchina o a un dominio) da un server licenze. In alternativa, le applicazioni client possono implementare un flusso di lavoro in cui il dispositivo si pre-registra con un server, il server pregenera le licenze associate a tale dispositivo e il client recupera le proprie licenze da un semplice server web HTTP.
title: Licenze di pregenerazione
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%

---


# Licenze di pregenerazione {#pre-generating-licenses}

Se utilizzi Adobe Primetime DRM Professional, puoi pregenerare licenze e incorporare licenze nei contenuti. Questa funzione può essere combinata con il concatenamento licenze avanzato, in modo tale che una licenza Leaf sia pregenerata e incorporata nel contenuto, e il client può richiedere una licenza Root (associata a una macchina o a un dominio) da un server licenze. In alternativa, le applicazioni client possono implementare un flusso di lavoro in cui il dispositivo si pre-registra con un server, il server pregenera le licenze associate a tale dispositivo e il client recupera le proprie licenze da un semplice server web HTTP.

Se desideri pregenerare le licenze, devi utilizzare `com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()` per ottenere un&#39;istanza di `LicenseFactory`. È necessario specificare una credenziale del server licenze per firmare le licenze generate da questo factory. Questa classe supporta la generazione di licenze per foglia senza concatenamento licenze e licenze per foglia e radice con la [catena di licenze ottimizzata](../../protecting-content/implementing-the-license-server/license-chaining/gen-enhanced-license-chaining.md).

Quando generi una licenza Leaf, devi specificare i metadati del contenuto che si applicano a `initContentInfo()`. Se i metadati includono più criteri DRM, o se desideri utilizzare un criterio DRM non incluso nei metadati, devi utilizzare `setSelectedPolicy()` per specificare il criterio DRM per generare una licenza. Se si utilizza un elenco di aggiornamento dei criteri DRM per tenere traccia degli aggiornamenti ai criteri DRM, è possibile fornire l&#39;elenco di aggiornamento dei criteri DRM alla Fabbrica delle licenze prima di inizializzare i metadati con `setPolicyUpdateList()`.

Quando generi una licenza Root, devi specificare i metadati del contenuto come descritto sopra. In alternativa, puoi generare una licenza Root applicando un criterio DRM ( `setSelectedPolicy()`) e un URL del server licenze ( `setLicenseServerURL()`) invece dei metadati.

>[!NOTE]
>
>È necessario un URL del server licenze anche se non è presente un server licenze Adobe Primetime DRM da cui i client possono richiedere una licenza. In questo caso, l’URL del server licenze deve specificare un URL che identifichi l’emittente della licenza.

Se il criterio DRM utilizza il concatenamento licenze avanzato, è necessario specificare una credenziale del server licenze per decrittografare la chiave di crittografia radice nel criterio DRM ( `setRootKeyRetrievalInfo()`).

Se il criterio DRM richiede una licenza associata al dominio, è necessario utilizzare `setDomainCAs()` per specificare gli emittenti del dominio da cui il server licenze accetta i token di dominio. Per convalidare il destinatario della licenza, è necessario fornire uno o più certificati CA di dominio.

Se il criterio DRM richiede la consegna di chiavi remote per i dispositivi iOS, è necessario fornire il certificato del server chiavi applicando `setKeyServerCertificate()` a meno che non venga generata una foglia concatenata.

Per generare una licenza, è necessario richiamare `generateLicense()` e specificare il tipo di licenza (foglia o radice) e uno o più certificati dei destinatari. Il certificato destinatario rappresenta un certificato computer o un certificato di dominio, a seconda dei requisiti specificati nel criterio DRM. Se si genera una foglia concatenata, un destinatario non è obbligatorio. Una volta generata la licenza, puoi sovrascrivere le regole di utilizzo specificate nel criterio DRM. Infine, è necessario richiamare `signLicense()` per firmare la licenza e ottenere un&#39;istanza di `PreGeneratedLicense`. È ora possibile salvare la licenza (utilizzare `getBytes()` per recuperare la licenza serializzata o incorporata in contenuto crittografato).

Consulta [Incorporazione di licenze](../../protecting-content/pre-generating-and-embedded-licenses/embedding-licenses.md).

Per un esempio di codice su come dimostrare le licenze pre-generate, consulta `com.adobe.flashaccess.samples.licensegen.GenerateLicense` nella directory &quot;amples&quot; degli strumenti della riga di comando per l’implementazione di riferimento .
