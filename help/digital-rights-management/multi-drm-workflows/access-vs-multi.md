---
description: Per coloro che hanno familiarità con la soluzione DRM di Adobe Primetime Access, esistono alcune differenze architettoniche fondamentali tra Access e Primetime Cloud DRM, basata sulla soluzione ExpressPlay.
title: Migrazione da Access a Multi-DRM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---


# Migrazione da Access a Multi-DRM {#migrating-from-access-to-multi-drm}

Per coloro che hanno familiarità con la soluzione DRM di Adobe Primetime Access, esistono alcune differenze architettoniche fondamentali tra Access e Primetime Cloud DRM, basata sulla soluzione ExpressPlay.

## Differenze architettoniche tra accesso e Multi-DRM

|  | Accesso | Multi-DRM |
|---|---|---|
| **Pacchetto** | Il Packager è associato a un server licenze. Il Packager deve conoscere la chiave pubblica del server licenze quando il contenuto viene imballato. | Il Packager non è associato a un server licenze. |
|  | Una volta che il contenuto viene compilato, viene associato a un particolare server di licenza. | Il contenuto non è associato a un server licenze specifico. Un effetto di ciò è che è possibile creare pacchetti di tutto il contenuto prima di ottenere la licenza di produzione. |
|  | Il Packager non deve comunicare con alcuna forma di archiviazione chiave, perché le chiavi sono incorporate in modo sicuro nel contenuto stesso (nei metadati) dopo essere state crittografate. Solo il server licenze corrispondente può leggerli. | Le chiavi devono essere inviate *a* Pacchetti da un sistema di storage chiave oppure *da* un Packager a un sistema di storage chiave. Un sistema di storage chiave può essere un sistema personalizzato o un sistema di storage di riferimento ExpressPlay. |
| **Diritto** | Il client effettua una richiesta di contenuto al servizio Access Cloud. Il servizio cloud di Access invia quindi una richiesta al sistema di adesione del cliente. Il sistema di adesione del cliente risponde con le adesioni per il cliente. (Il client ha probabilmente ottenuto un cookie per l&#39;accesso dai server del cliente prima di effettuare la richiesta di licenza.) | Il cliente effettua una richiesta di un token dalla vetrina del cliente (probabilmente si tratta dello stesso flusso di lavoro in cui il cliente stava ricevendo in precedenza un cookie di autenticazione). Al momento, il cliente esegue un controllo delle adesioni. Se il controllo delle adesioni viene superato, il cliente invia una richiesta ai server ExpressPlay per generare un token per il cliente. Questo token è sempre associato a un contenuto specifico e *può* essere associato a un dispositivo specifico. La vetrina del cliente invia nuovamente il token al client. Quando il client effettua una richiesta di riproduzione DRM, il token viene incluso nella richiesta (il metodo per questo è specifico per il dispositivo) e il server DRM di ExpressPlay convalida il token senza richiamare il server del cliente. |