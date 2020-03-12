---
description: Flash Media Rights Management Server 1.x e Adobe Primetime DRM utilizzano metadati diversi per creare pacchetti di contenuto e richiedere licenze. Affinché DRM di Primetime utilizzi il contenuto FMRMS versione 1.x, i metadati devono essere convertiti.
seo-description: Flash Media Rights Management Server 1.x e Adobe Primetime DRM utilizzano metadati diversi per creare pacchetti di contenuto e richiedere licenze. Affinché DRM di Primetime utilizzi il contenuto FMRMS versione 1.x, i metadati devono essere convertiti.
seo-title: Garanzia di compatibilità con Flash Media Rights Management Server 1.x
title: Garanzia di compatibilità con Flash Media Rights Management Server 1.x
uuid: dd70941e-9015-4fb0-b265-557b6252e051
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Garanzia di compatibilità con Flash Media Rights Management Server 1.x {#ensuring-compatibility-with-flash-media-rights-management-server-x}

Flash Media Rights Management Server 1.x e Adobe Primetime DRM utilizzano metadati diversi per creare pacchetti di contenuto e richiedere licenze. Affinché DRM di Primetime utilizzi il contenuto FMRMS versione 1.x, i metadati devono essere convertiti.

L’SDK DRM di Primetime supporta le seguenti opzioni per la conversione dei metadati:

* Offline (consigliato)

   Generate i metadati DRM di Primetime in un processo offline e memorizzate i metadati finché non vengono richiesti da un client. Se i metadati vengono generati offline, il server delle licenze non ha bisogno di accedere ai CEK 1.x o alle credenziali del packager. La conversione offline offre prestazioni migliori perché il server licenze non deve generare i metadati in tempo reale.
* Su richiesta

   I metadati DRM di Primetime vengono generati quando i metadati vengono richiesti da un client. Quando un client DRM Primetime scarica il contenuto della versione 1.x, il client invia i metadati DRM all&#39;SDK DRM di Primetime. L’SDK converte i metadati DRM nel formato corrente, codifica e incorpora la chiave di crittografia del contenuto (CEK) nei metadati e invia nuovamente il contenuto al client DRM Primetime.

   >[!NOTE]
   >
   >I metadati DRM 1.x di Primetime non includono la CEK.

   Per convertire i metadati, Primetime DRM richiede l&#39;accesso alle chiavi di crittografia del contenuto DRM 1.x di Primetime. Quando eseguite la migrazione da Flash Media Rights Management Server 1.x, potete continuare a memorizzare le chiavi di crittografia del contenuto nel database LiveCycle ES oppure implementare una soluzione personalizzata per memorizzare in modo sicuro le chiavi di crittografia del contenuto in un&#39;altra posizione. Se si decide di archiviare le chiavi di crittografia del contenuto nel database LiveCycle ES, attenersi alle raccomandazioni descritte in *Proteggere l&#39;accesso al contenuto sensibile nel database* in **Protezione e protezione per LiveCycle® ES2**.

Per ulteriori informazioni su come garantire la compatibilità con il contenuto incluso nel pacchetto utilizzando Flash Media Rights Management Server 1.x, consultate API DRM di Adobe Primetime sui riferimenti [API di](https://help.adobe.com/en_US/primetime/api/index.html#api-Adobe_Primetime_API_References)Adobe Primetime.
