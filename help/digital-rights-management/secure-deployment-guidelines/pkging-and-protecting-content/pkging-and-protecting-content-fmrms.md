---
description: Flash Media Rights Management Server 1.x e Adobe Primetime DRM utilizzano metadati diversi per creare pacchetti di contenuti e richiedere licenze. Affinché Primetime DRM possa utilizzare il contenuto FMRMS versione 1.x, i metadati devono essere convertiti.
title: Compatibilità con Flash Media Rights Management Server 1.x
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---


# Compatibilità con Flash Media Rights Management Server 1.x {#ensuring-compatibility-with-flash-media-rights-management-server-x}

Flash Media Rights Management Server 1.x e Adobe Primetime DRM utilizzano metadati diversi per creare pacchetti di contenuti e richiedere licenze. Affinché Primetime DRM possa utilizzare il contenuto FMRMS versione 1.x, i metadati devono essere convertiti.

L&#39;SDK DRM di Primetime supporta le seguenti opzioni per la conversione dei metadati:

* Offline (consigliato)

   Genera i metadati DRM di Primetime in un processo offline e archivia i metadati finché non vengono richiesti da un cliente. Se i metadati vengono generati offline, il server di licenza non ha bisogno dell&#39;accesso ai CEK 1.x o alle credenziali del packager. La conversione offline offre prestazioni migliori perché il server licenze non deve generare i metadati in tempo reale.
* On-demand

   I metadati DRM di Primetime vengono generati quando i metadati sono richiesti da un client. Quando un client DRM di Primetime scarica il contenuto della versione 1.x, il client invia i metadati DRM all&#39;SDK DRM di Primetime. L’SDK converte i metadati DRM nel formato corrente, crittografa e incorpora la chiave di crittografia del contenuto (CEK) nei metadati e invia di nuovo il contenuto al client DRM di Primetime.

   >[!NOTE]
   >
   >I metadati DRM 1.x di Primetime non includono la CEK.

   Per convertire i metadati, Primetime DRM richiede l&#39;accesso alle chiavi di crittografia dei contenuti DRM 1.x di Primetime. Quando esegui la migrazione da Flash Media Rights Management Server 1.x, puoi continuare a memorizzare le chiavi di crittografia del contenuto nel database di LiveCycle ES o implementare una soluzione personalizzata per memorizzare in modo sicuro le chiavi di crittografia del contenuto in un&#39;altra posizione. Se decidi di memorizzare le chiavi di crittografia del contenuto nel database LiveCycle ES, segui le raccomandazioni descritte in *Protezione dell&#39;accesso a contenuti sensibili nel database* in **Hardening and Security for LiveCycle® ES2**.

Per ulteriori informazioni su come garantire la compatibilità con i contenuti inclusi nel pacchetto utilizzando Flash Media Rights Management Server 1.x, consulta API DRM di Adobe Primetime in [Riferimenti API di Adobe Primetime](https://help.adobe.com/en_US/primetime/api/index.html#api-Adobe_Primetime_API_References).
