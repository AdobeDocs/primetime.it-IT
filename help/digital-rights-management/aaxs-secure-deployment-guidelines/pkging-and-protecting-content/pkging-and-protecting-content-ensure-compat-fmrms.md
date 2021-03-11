---
title: Compatibilità con Flash Media Rights Management Server 1.x
description: Compatibilità con Flash Media Rights Management Server 1.x
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---


# Garantire la compatibilità con Flash Media Rights Management Server 1.x{#ensure-compatibility-with-flash-media-rights-management-server-x}

Flash Media Rights Management Server 1.x e Adobe Access utilizzano metadati diversi per la creazione di pacchetti di contenuti e la richiesta di licenze. Ad Adobe, Access per utilizzare il contenuto FMRMS versione 1.x, i metadati devono essere convertiti.

L&#39;SDK per Adobe Access supporta due opzioni per la conversione dei metadati:

* Offline (consigliato)

   Generare i metadati di accesso agli Adobi in un processo offline e memorizzarli per l&#39;utilizzo quando un client li richiede. Adobe consiglia questa opzione. Se i metadati vengono generati offline, il server di licenza non ha bisogno dell&#39;accesso ai CEK 1.x o alle credenziali del packager. Inoltre, la conversione offline offre prestazioni migliori perché il server licenze non deve generare i metadati in tempo reale.

* On-demand

   Genera i metadati di accesso Adobe on-demand quando un cliente li richiede. Quando un client Adobe Access scarica il contenuto versione 1.x, invia i metadati DRM (noti anche come intestazione DRM) all’SDK di Adobe Access. L’SDK converte i metadati DRM nel formato corrente. L’SDK crittografa e incorpora la chiave di crittografia del contenuto (CEK) nei metadati e restituisce il contenuto al client di Adobe Access. (I metadati di Adobe Access 1.x non contengono il CEK.)

   Per convertire i metadati, Adobe Access richiede l&#39;accesso alle chiavi di crittografia dei contenuti di Adobe Access 1.x. Quando esegui la migrazione da Flash Media Rights Management Server 1.x, puoi continuare a memorizzare le chiavi di crittografia del contenuto nel database di LiveCycle ES oppure implementare una soluzione personalizzata per memorizzare in modo sicuro le chiavi di crittografia del contenuto altrove. Se scegli di continuare a memorizzare le chiavi di crittografia del contenuto nel database LiveCycle ES, segui le raccomandazioni descritte in &quot;Proteggere l&#39;accesso a contenuti sensibili nel database&quot; in *Hardening and Security for LiveCycle ES*.

Per ulteriori informazioni su come garantire la compatibilità con i contenuti inclusi nel pacchetto utilizzando Flash Media Rights Management Server 1.x, consulta la sezione *Riferimento API di accesso agli Adobi*.
