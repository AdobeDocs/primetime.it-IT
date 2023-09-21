---
title: Compatibilità con Flash Media Rights Management Server 1.x
description: Compatibilità con Flash Media Rights Management Server 1.x
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# Compatibilità con Flash Media Rights Management Server 1.x{#ensure-compatibility-with-flash-media-rights-management-server-x}

Flash Media Rights Management Server 1.x e Adobe Access utilizzano metadati diversi per la creazione di pacchetti di contenuti e la richiesta di licenze. Ad Adobe, per utilizzare il contenuto FMRMS versione 1.x, è necessario convertire i metadati.

L’SDK di accesso di Adobe supporta due opzioni per la conversione dei metadati:

* Offline (consigliato)

  Generare i metadati di accesso Adobe in un processo non in linea e archiviarli per l&#39;utilizzo quando un client lo richiede. L’Adobe consiglia questa opzione. Se i metadati vengono generati offline, il server licenze non ha bisogno dell&#39;accesso ai CEK 1.x o alle credenziali del packager. Inoltre, la conversione offline offre prestazioni migliori perché il server licenze non deve generare i metadati in tempo reale.

* On-demand

  Genera i metadati di accesso Adobe on-demand quando un client lo richiede. Quando un client Adobe Access scarica il contenuto versione 1.x, invia i metadati DRM (noti anche come intestazione DRM) all’SDK Adobe Access. L&#39;SDK converte i metadati DRM nel formato corrente. L’SDK crittografa e incorpora la chiave di crittografia del contenuto (CEK) nei metadati e invia nuovamente il contenuto al client Adobe Access. I metadati di Access 1.x di Adobe non contengono il valore CEK.

  Per convertire i metadati, Adobe Access richiede l&#39;accesso alle chiavi di crittografia del contenuto Adobe Access 1.x. Quando si esegue la migrazione da Flash Media Rights Management Server 1.x, è possibile continuare a memorizzare le chiavi di crittografia del contenuto nel database LiveCycle ES oppure implementare una soluzione personalizzata per memorizzare in modo sicuro le chiavi di crittografia del contenuto altrove. Se si sceglie di continuare a memorizzare le chiavi di crittografia del contenuto nel database ES di LiveCycle, seguire le raccomandazioni descritte in &quot;Protezione dell&#39;accesso a contenuto sensibile nel database&quot; in *Protezione avanzata e protezione per il LiveCycle ES*.

Per ulteriori informazioni su come garantire la compatibilità con i contenuti inclusi nel pacchetto utilizzando Flash Media Rights Management Server 1.x, vedere *Riferimento API per l’accesso agli Adobi*.
