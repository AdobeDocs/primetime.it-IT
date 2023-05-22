---
description: Per chi conosce la soluzione DRM di accesso Primetime di Adobe, esistono alcune differenze fondamentali a livello di architettura tra Access e Primetime Cloud DRM, con tecnologia ExpressPlay.
title: Migrazione dall'accesso a Multi-DRM
exl-id: f5e4cd88-091d-4049-933d-1c72ceeb2efb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---

# Migrazione dall&#39;accesso a Multi-DRM {#migrating-from-access-to-multi-drm}

Per chi conosce la soluzione DRM di accesso Primetime di Adobe, esistono alcune differenze fondamentali a livello di architettura tra Access e Primetime Cloud DRM, con tecnologia ExpressPlay.

## Differenze di architettura tra Access e Multi-DRM

|  | Accesso | Multi-DRM |
|---|---|---|
| **Imballaggio** | Packager è associato a un server licenze. Il Packager deve conoscere la chiave pubblica del server licenze quando il contenuto viene collocato. | Packager non è associato a un server licenze. |
|  | Una volta creato il pacchetto, il contenuto viene associato a un server licenze specifico. | Il contenuto non è associato a un server licenze specifico. Un effetto di questo è che è possibile creare un pacchetto di tutti i contenuti prima di ottenere la licenza di produzione. |
|  | Il Packager non deve comunicare con nessun tipo di archiviazione delle chiavi, poiché queste sono incorporate in modo sicuro nel contenuto stesso (nei metadati) dopo essere state crittografate. Solo il server licenze corrispondente è in grado di leggerli. | Le chiavi devono essere inviate *a* Packagers da un sistema di storage chiave o inviati *da* un Packager a un sistema di storage chiave. Un sistema di storage chiave può essere un sistema proprio del cliente o un sistema di storage ExpressPlay. |
| **Diritto** | Il client invia una richiesta di contenuto al servizio Access Cloud. Il servizio cloud Access invia quindi una richiesta al sistema di adesione del cliente. Il sistema di adesione del cliente risponde con le adesioni per il cliente. Il client probabilmente ha ottenuto un cookie per l’accesso dai server del cliente prima di effettuare la richiesta di licenza. | Il client richiede un token dalla vetrina del cliente (si tratta probabilmente dello stesso flusso di lavoro in cui il cliente riceveva in precedenza un cookie di autenticazione). In questo momento, il cliente esegue un controllo dei diritti. Se il controllo dei diritti viene superato, il cliente invia una richiesta ai server ExpressPlay per generare un token per il cliente. Questo token è sempre associato a un contenuto specifico e *maggio* essere associato a un dispositivo specifico. La vetrina del cliente invia nuovamente il token al client. Quando il client effettua una richiesta di riproduzione DRM, il token viene incluso nella richiesta (il metodo è specifico per il dispositivo) e il server DRM di ExpressPlay convalida il token senza chiamare il server del cliente. |
