---
description: Flash Media Rights Management Server 1.x e Adobe Primetime DRM utilizzano metadati diversi per creare pacchetti di contenuti e richiedere licenze. Affinché Primetime DRM utilizzi il contenuto FMRMS versione 1.x, è necessario convertire i metadati.
title: Garanzia di compatibilità con Flash Media Rights Management Server 1.x
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# Garanzia di compatibilità con Flash Media Rights Management Server 1.x {#ensuring-compatibility-with-flash-media-rights-management-server-x}

Flash Media Rights Management Server 1.x e Adobe Primetime DRM utilizzano metadati diversi per creare pacchetti di contenuti e richiedere licenze. Affinché Primetime DRM utilizzi il contenuto FMRMS versione 1.x, è necessario convertire i metadati.

L’SDK di Primetime DRM supporta le seguenti opzioni per la conversione dei metadati:

* Offline (consigliato)

  Generare i metadati DRM di Primetime in un processo offline e archiviarli finché non vengono richiesti da un client. Se i metadati vengono generati offline, il server licenze non ha bisogno dell&#39;accesso ai CEK 1.x o alle credenziali del packager. La conversione offline offre prestazioni migliori perché il server licenze non deve generare i metadati in tempo reale.
* On-demand

  I metadati DRM di Primetime vengono generati quando vengono richiesti da un client. Quando un client DRM Primetime scarica il contenuto versione 1.x, invia i metadati DRM all’SDK DRM Primetime. L’SDK converte i metadati DRM nel formato corrente, crittografa e incorpora la chiave di crittografia del contenuto (CEK) nei metadati e invia nuovamente il contenuto al client DRM di Primetime.

  >[!NOTE]
  >
  >I metadati di Primetime DRM 1.x non includono CEK.

  Per convertire i metadati, è necessario accedere alle chiavi di crittografia del contenuto di Primetime DRM 1.x. Quando si esegue la migrazione da Flash Media Rights Management Server 1.x, è possibile continuare a memorizzare le chiavi di crittografia del contenuto nel database LiveCycle ES o implementare una soluzione personalizzata per memorizzare in modo sicuro le chiavi di crittografia del contenuto in un&#39;altra posizione. Se si decide di memorizzare le chiavi di crittografia del contenuto nel database ES del LiveCycle, seguire le raccomandazioni descritte in *Protezione dell&#39;accesso a contenuto riservato nel database* in **Protezione avanzata per LiveCycle®2**.

Per ulteriori informazioni su come garantire la compatibilità con i contenuti inclusi nel pacchetto utilizzando Flash Media Rights Management Server 1.x, vedere API DRM di Adobe Primetime in [Riferimenti API di Adobe Primetime](https://help.adobe.com/en_US/primetime/api/index.html#api-Adobe_Primetime_API_References).
