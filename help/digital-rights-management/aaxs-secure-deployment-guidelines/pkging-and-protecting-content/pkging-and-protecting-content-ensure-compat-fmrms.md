---
seo-title: Compatibilità con Flash Media Rights Management Server 1.x
title: Compatibilità con Flash Media Rights Management Server 1.x
uuid: 0160ca02-ebe6-4090-bf32-1d1a46088844
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Compatibilità con Flash Media Rights Management Server 1.x{#ensure-compatibility-with-flash-media-rights-management-server-x}

Flash Media Rights Management Server 1.x e Adobe Access utilizzano metadati diversi per creare pacchetti di contenuti e richiedere licenze. Affinché Adobe Access possa utilizzare il contenuto FMRMS versione 1.x, i metadati devono essere convertiti.

L’SDK di Adobe Access supporta due opzioni per la conversione dei metadati:

* Offline (consigliato)

   Generare i metadati di Adobe Access in un processo offline e memorizzarli per l&#39;utilizzo quando il client li richiede. Adobe consiglia questa opzione. Se i metadati vengono generati offline, il server delle licenze non ha bisogno di accedere ai CEK 1.x o alle credenziali del packager. Inoltre, la conversione offline offre prestazioni migliori perché il server licenze non deve generare i metadati in tempo reale.

* Su richiesta

   Generare i metadati Adobe Access on-demand quando un cliente li richiede. Quando un client Adobe Access scarica il contenuto della versione 1.x, invia i metadati DRM (denominati anche intestazione DRM) all’SDK di Adobe Access. L’SDK converte i metadati DRM nel formato corrente. L’SDK codifica e incorpora la chiave di crittografia del contenuto (CEK) nei metadati e invia nuovamente il contenuto al client Adobe Access. (I metadati di Adobe Access 1.x non contengono CEK.)

   Per convertire i metadati, Adobe Access richiede l&#39;accesso alle chiavi di crittografia dei contenuti di Adobe Access 1.x. Quando eseguite la migrazione da Flash Media Rights Management Server 1.x, potete continuare a memorizzare le chiavi di crittografia del contenuto nel database LiveCycle ES oppure potete implementare una soluzione personalizzata per memorizzare in modo sicuro le chiavi di crittografia del contenuto altrove. Se si sceglie di continuare a memorizzare le chiavi di crittografia del contenuto nel database LiveCycle ES, attenersi alle raccomandazioni descritte in &quot;Proteggere l&#39;accesso al contenuto sensibile nel database&quot; in *Protezione e protezione per LiveCycle ES*.

Per ulteriori informazioni su come garantire la compatibilità con il contenuto incluso in un pacchetto utilizzando Flash Media Rights Management Server 1.x, consultate il documento di riferimento per le API di *Adobe Access*.
