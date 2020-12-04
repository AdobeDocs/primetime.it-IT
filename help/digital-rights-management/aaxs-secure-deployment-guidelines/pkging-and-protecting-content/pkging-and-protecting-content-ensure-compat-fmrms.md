---
seo-title: Compatibilità con Flash Media Rights Management Server 1.x
title: Compatibilità con Flash Media Rights Management Server 1.x
uuid: 0160ca02-ebe6-4090-bf32-1d1a46088844
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---


# Compatibilità con Flash Media Rights Management Server 1.x{#ensure-compatibility-with-flash-media-rights-management-server-x}

Flash Media Rights Management Server 1.x e  Accesso Adobe utilizzano metadati diversi per la creazione di pacchetti di contenuto e per la richiesta di licenze. Per  Adobe Accesso all&#39;uso del contenuto FMRMS versione 1.x, i metadati devono essere convertiti.

L&#39;SDK di accesso al Adobe  supporta due opzioni per la conversione dei metadati:

* Offline (consigliato)

   Generare i metadati di accesso al Adobe  in un processo offline e memorizzarli per l&#39;utilizzo quando il client li richiede.  Adobe consiglia questa opzione. Se i metadati vengono generati offline, il server delle licenze non ha bisogno di accedere ai CEK 1.x o alle credenziali del packager. Inoltre, la conversione offline offre prestazioni migliori perché il server licenze non deve generare i metadati in tempo reale.

* Su richiesta

   Generare i metadati di accesso al Adobe  su richiesta quando un cliente lo richiede. Quando un client di accesso  Adobe scarica il contenuto della versione 1.x, invia i metadati DRM (noti anche come intestazione DRM) all&#39;SDK di accesso al Adobe . L’SDK converte i metadati DRM nel formato corrente. L’SDK codifica e incorpora la chiave di crittografia del contenuto (CEK) nei metadati e invia nuovamente il contenuto al client di accesso al Adobe . (I metadati di Access 1.x del Adobe  non contengono CEK.)

   Per convertire i metadati,  Accesso Adobe richiede l&#39;accesso alle chiavi di crittografia del contenuto  Adobe Access 1.x. Quando eseguite la migrazione da Media Rights Management Server 1.x di Flash, potete continuare a memorizzare le chiavi di crittografia del contenuto nel database LiveCycle ES oppure potete implementare una soluzione personalizzata per memorizzare in modo sicuro le chiavi di crittografia del contenuto altrove. Se si sceglie di continuare a memorizzare le chiavi di crittografia del contenuto nel database di LiveCycle ES, seguire le raccomandazioni descritte in &quot;Proteggere l&#39;accesso al contenuto sensibile nel database&quot; in *Protezione e protezione per il LiveCycle ES*.

Per ulteriori informazioni su come garantire la compatibilità con il contenuto incluso nel pacchetto utilizzando Flash Media Rights Management Server 1.x, vedere la *Guida di riferimento alle API per l&#39;accesso Adobe*.
