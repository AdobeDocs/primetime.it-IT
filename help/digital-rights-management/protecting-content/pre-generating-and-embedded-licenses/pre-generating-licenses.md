---
description: Se si utilizza Adobe Primetime DRM Professional, è possibile pregenerare licenze e incorporarle nel contenuto. Questa funzione può essere combinata con il Concatenamento licenze avanzato, in modo che una licenza Leaf sia pregenerata e incorporata nel contenuto e il client possa richiedere una licenza Root (associata a un computer o a un dominio) da un server licenze. In alternativa, le applicazioni client possono implementare un flusso di lavoro in cui il dispositivo si pre-registra con un server, il server pregenera le licenze associate a tale dispositivo e il client recupera le licenze da un semplice server web HTTP.
title: Pre-generazione delle licenze
exl-id: 6ced7dde-b4bb-470d-bdae-3042f5577b67
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%

---

# Pre-generazione delle licenze {#pre-generating-licenses}

Se si utilizza Adobe Primetime DRM Professional, è possibile pregenerare licenze e incorporarle nel contenuto. Questa funzione può essere combinata con il Concatenamento licenze avanzato, in modo che una licenza Leaf sia pregenerata e incorporata nel contenuto e il client possa richiedere una licenza Root (associata a un computer o a un dominio) da un server licenze. In alternativa, le applicazioni client possono implementare un flusso di lavoro in cui il dispositivo si pre-registra con un server, il server pregenera le licenze associate a tale dispositivo e il client recupera le licenze da un semplice server web HTTP.

Se si desidera pregenerare le licenze, è necessario utilizzare `com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()` per ottenere un&#39;istanza di `LicenseFactory`. È necessario specificare le credenziali del server licenze per firmare le licenze generate da questa factory. Questa classe supporta la generazione di licenze Leaf senza concatenamento licenze e licenze Leaf e Root con [Migliore concatenamento delle licenze](../../protecting-content/implementing-the-license-server/license-chaining/gen-enhanced-license-chaining.md).

Quando generi una licenza Leaf, devi specificare i metadati di contenuto applicabili `initContentInfo()`. Se i metadati includono più criteri DRM o se si desidera utilizzare un criterio DRM non incluso nei metadati, è necessario utilizzare `setSelectedPolicy()` per specificare il criterio DRM per generare una licenza. Se si utilizza un elenco di aggiornamento dei criteri DRM per tenere traccia degli aggiornamenti ai criteri DRM, è possibile fornire l&#39;elenco di aggiornamento dei criteri DRM alla License Factory prima di inizializzare i metadati con `setPolicyUpdateList()`.

Quando generi una licenza Root, devi specificare i metadati del contenuto come descritto in precedenza. In alternativa, è possibile generare una licenza Root applicando un criterio DRM ( `setSelectedPolicy()`) e un URL del server licenze ( `setLicenseServerURL()`) al posto dei metadati.

>[!NOTE]
>
>L&#39;URL del server licenze è necessario anche se non esiste un server licenze Adobe Primetime DRM dal quale i client possano richiedere una licenza. In questo caso, l’URL del server licenze deve specificare un URL che identifichi l’emittente della licenza.

Se il criterio DRM utilizza il concatenamento licenze avanzato, è necessario specificare una credenziale del server licenze per decrittografare la chiave di crittografia radice nel criterio DRM ( `setRootKeyRetrievalInfo()`).

Se il criterio DRM richiede una licenza associata al dominio, è necessario utilizzare `setDomainCAs()` per specificare gli autori del dominio da cui il server licenze accetta i token di dominio. Per convalidare il destinatario della licenza è necessario fornire uno o più certificati CA di dominio.

Se il criterio DRM richiede la consegna della chiave remota per i dispositivi iOS, è necessario fornire il certificato del server chiavi applicando `setKeyServerCertificate()` a meno che non venga generata una foglia concatenata.

Se si desidera generare una licenza, è necessario richiamare `generateLicense()` e specificare il tipo di licenza (Leaf o Root) e uno o più certificati dei destinatari. Il certificato del destinatario rappresenta un certificato del computer o di dominio, a seconda dei requisiti specificati nel criterio DRM. Se generi una foglia concatenata, non è necessario un destinatario. Una volta generata la licenza, è possibile ignorare le regole di utilizzo specificate nel criterio DRM. Infine, devi richiamare `signLicense()` per firmare la licenza e ottenere un&#39;istanza di `PreGeneratedLicense`. È ora possibile salvare la licenza (utilizzare `getBytes()` per recuperare la licenza serializzata o incorporata in contenuto crittografato.

Consulta [Incorporazione delle licenze](../../protecting-content/pre-generating-and-embedded-licenses/embedding-licenses.md).

Consulta `com.adobe.flashaccess.samples.licensegen.GenerateLicense` nella directory &quot;samples&quot; degli strumenti della riga di comando per l’implementazione di riferimento per un codice di esempio su come dimostrare le licenze pregenerate.
