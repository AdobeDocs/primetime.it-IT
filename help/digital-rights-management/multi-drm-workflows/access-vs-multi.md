---
description: Per coloro che hanno familiarità con  soluzione DRM di accesso  Primetime, esistono alcune differenze architettoniche fondamentali tra Access e Primetime Cloud DRM, basata sulla soluzione ExpressPlay.
seo-description: Per coloro che hanno familiarità con  soluzione DRM di accesso  Primetime, esistono alcune differenze architettoniche fondamentali tra Access e Primetime Cloud DRM, basata sulla soluzione ExpressPlay.
seo-title: Migrazione dall'accesso a Multi-DRM
title: Migrazione dall'accesso a Multi-DRM
uuid: 3e33ca9a-867e-46b8-bf88-8dbfe14ff786
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---


# Migrazione da Access a Multi-DRM {#migrating-from-access-to-multi-drm}

Per coloro che hanno familiarità con  soluzione DRM di accesso  Primetime, esistono alcune differenze architettoniche fondamentali tra Access e Primetime Cloud DRM, basata sulla soluzione ExpressPlay.

## Differenze architettoniche tra accesso e Multi-DRM

|  | Access | Multi-DRM |
|---|---|---|
| **Creazione pacchetto** | Packager è associato a un server licenze. Il Packager deve conoscere la chiave pubblica del server licenze quando viene creato il pacchetto del contenuto. | Packager non è associato a un server licenze. |
|  | Una volta creato il pacchetto, il contenuto viene associato a un particolare server licenze. | Il contenuto non è associato a un server licenze specifico. Uno degli effetti di ciò è che potete creare pacchetti per tutti i contenuti prima di ottenere la licenza di produzione. |
|  | Non è necessario che Packager comunichi con alcuna forma di memorizzazione di chiavi, perché le chiavi vengono incorporate in modo sicuro nel contenuto stesso (nei metadati) dopo essere state crittografate. Solo il server licenze corrispondente può leggerli. | Le chiavi devono essere inviate *a* Packager da un sistema di storage chiave oppure inviate *da* un Packager a un sistema di storage chiave. Un sistema di storage chiave può essere un sistema personalizzato o un sistema di storage ExpressPlay. |
| **Adesione** | Il client effettua una richiesta di contenuto al servizio Access Cloud. Il servizio cloud di Access invia quindi una richiesta al sistema di adesione del cliente. Il sistema di adesione del cliente risponde con le adesioni per il cliente. (Il client ha probabilmente ottenuto un cookie per l&#39;accesso dai server del cliente prima di effettuare la richiesta di licenza.) | Il cliente fa una richiesta per un token dallo storefront del cliente (probabilmente si tratta dello stesso flusso di lavoro in cui il cliente in precedenza riceveva un cookie di autenticazione). Al momento, il cliente esegue un controllo delle adesioni. Se il controllo delle adesioni viene superato, il cliente invia una richiesta ai server ExpressPlay per generare un token per il cliente. Questo token è sempre associato a un contenuto specifico e *può* essere associato a un dispositivo specifico. Lo storefront del cliente invia il token al client. Quando il client effettua una richiesta di riproduzione DRM, il token viene incluso nella richiesta (il metodo per questa operazione è specifico del dispositivo) e il server DRM di ExpressPlay convalida il token senza chiamare il server del cliente. |