---
description: Se utilizzate  Adobe Primetime DRM Professional, potete pregenerare licenze e incorporare licenze nel contenuto. Questa funzione può essere combinata con la Concatenazione licenza avanzata, in modo che una licenza Leaf sia pregenerata e incorporata nel contenuto, e il client possa richiedere una licenza Root (associata a un computer o a un dominio) da un server licenze. In alternativa, le applicazioni client possono implementare un flusso di lavoro in cui il dispositivo si preregistra con un server, il server pre-genera licenze associate a tale dispositivo e il client recupera le licenze da un semplice server Web HTTP.
seo-description: Se utilizzate  Adobe Primetime DRM Professional, potete pregenerare licenze e incorporare licenze nel contenuto. Questa funzione può essere combinata con la Concatenazione licenza avanzata, in modo che una licenza Leaf sia pregenerata e incorporata nel contenuto, e il client possa richiedere una licenza Root (associata a un computer o a un dominio) da un server licenze. In alternativa, le applicazioni client possono implementare un flusso di lavoro in cui il dispositivo si preregistra con un server, il server pre-genera licenze associate a tale dispositivo e il client recupera le licenze da un semplice server Web HTTP.
seo-title: Licenze di pre-generazione
title: Licenze di pre-generazione
uuid: aa7d5038-5a9b-40a2-a240-266622158b43
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 0%

---


# Licenze di pre-generazione {#pre-generating-licenses}

Se utilizzate  Adobe Primetime DRM Professional, potete pregenerare licenze e incorporare licenze nel contenuto. Questa funzione può essere combinata con la Concatenazione licenza avanzata, in modo che una licenza Leaf sia pregenerata e incorporata nel contenuto, e il client possa richiedere una licenza Root (associata a un computer o a un dominio) da un server licenze. In alternativa, le applicazioni client possono implementare un flusso di lavoro in cui il dispositivo si preregistra con un server, il server pre-genera licenze associate a tale dispositivo e il client recupera le licenze da un semplice server Web HTTP.

Per generare in anticipo le licenze, è necessario utilizzare `com.adobe.flashaccess.sdk.license.pregen.LicenseFactory.getInstance()` per ottenere un&#39;istanza di `LicenseFactory`. È necessario specificare una credenziale Server licenze per firmare le licenze generate da questo factory. Questa classe supporta la generazione di licenze Leaf senza concatenamento licenze e licenze Leaf e Root con concatenamento [Enhanced](../../protecting-content/implementing-the-license-server/license-chaining/gen-enhanced-license-chaining.md).

Quando generate una licenza Foglia, dovete specificare i metadati di contenuto applicabili `initContentInfo()`. Se i metadati includono più criteri DRM, o se desiderate utilizzare un criterio DRM non incluso nei metadati, dovete utilizzare `setSelectedPolicy()` per specificare il criterio DRM per generare una licenza. Se si utilizza un elenco di aggiornamento criteri DRM per tenere traccia degli aggiornamenti ai criteri DRM, è possibile fornire l&#39;elenco di aggiornamento criteri DRM al License Factory prima di inizializzare i metadati con `setPolicyUpdateList()`.

Quando generate una licenza Root, dovete specificare i metadati del contenuto come descritto sopra. In alternativa, potete generare una licenza Root applicando un criterio DRM ( `setSelectedPolicy()`) e un URL del server delle licenze ( `setLicenseServerURL()`) invece dei metadati.

>[!NOTE]
>
>È richiesto un URL del server licenze anche se non è presente  server licenze Adobe Primetime DRM dal quale i client possono richiedere una licenza. In questo caso, l&#39;URL del server licenze deve specificare un URL che identifica l&#39;emittente della licenza.

Se il criterio DRM utilizza il concatenamento licenze avanzato, è necessario specificare una credenziale Server licenze per decrittografare la chiave di crittografia principale nel criterio DRM ( `setRootKeyRetrievalInfo()`).

Se il criterio DRM richiede una licenza associata a un dominio, è necessario utilizzare `setDomainCAs()` per specificare gli emittenti di dominio da cui il server licenze accetta i token di dominio. Per convalidare il destinatario della licenza è necessario specificare uno o più certificati CA di dominio.

Se il criterio DRM richiede la consegna di chiavi remote per i dispositivi iOS, è necessario fornire il certificato Server chiavi applicando `setKeyServerCertificate()` a meno che non venga generata una foglia concatenata.

Se si desidera generare una licenza, è necessario richiamare `generateLicense()` e specificare il tipo di licenza (foglia o radice) e uno o più certificati del destinatario. Il certificato del destinatario rappresenta un certificato computer o un certificato di dominio, a seconda dei requisiti specificati nel criterio DRM. Se si genera una foglia concatenata, il destinatario non è obbligatorio. Una volta generata la licenza, potete ignorare le regole di utilizzo specificate nel criterio DRM. Infine, è necessario invocare `signLicense()` per firmare la licenza e ottenere un&#39;istanza di `PreGeneratedLicense`. È ora possibile salvare la licenza (da utilizzare `getBytes()` per recuperare la licenza serializzata o incorporarla in contenuto crittografato).

Consultate [Incorporazione di licenze](../../protecting-content/pre-generating-and-embedded-licenses/embedding-licenses.md).

Consultate `com.adobe.flashaccess.samples.licensegen.GenerateLicense` nella directory &quot;samples&quot; degli strumenti della riga di comando Implementazione di riferimento per un esempio di codice che illustra come dimostrare le licenze pregenerate.
