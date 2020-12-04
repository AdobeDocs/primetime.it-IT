---
description: Esistono alcuni modi per determinare l'inserimento e il posizionamento degli annunci.
seo-description: Esistono alcuni modi per determinare l'inserimento e il posizionamento degli annunci.
seo-title: Inserimento e posizionamento di annunci
title: Inserimento e posizionamento di annunci
uuid: 1d4d6364-1c49-402b-9b72-8c185b1c94e1
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---


# Inserimento annunci e posizionamento{#ad-insertion-and-placement}

Esistono alcuni modi per determinare l&#39;inserimento e il posizionamento degli annunci.

## Inserimento annunci {#section_1F7581B987704E318E064082190E8243}

Di seguito viene fornita una panoramica del processo utilizzato per determinare l&#39;inserimento di annunci:

1. **Rilevamento** opportunità: TVSDK utilizza le informazioni sul flusso per rilevare le posizioni possibili e desiderate per gli annunci.
1. **Risoluzione** annuncio: TVSDK comunica con un server di annunci per recuperare gli annunci da unire nel contenuto.
1. **Posizionamento** annuncio: Il TVSDK carica gli annunci specificati e li inserisce nella cronologia del contenuto nelle posizioni specificate e ricalcola la timeline virtuale, se necessario.

## Posizionamento annunci {#section_B9D63F7409A2447F9FF209289BE5D3D5}

TVSDK può ottenere posizioni per possibili inserimenti pubblicitari dalle seguenti origini:

* **Manifesto di metadati/suggerimenti**

   Il TVSDK rileva i segnali, estrae le informazioni necessarie da questi suggerimenti e comunica con un server pubblicitario per ottenere gli annunci corrispondenti. Questa fonte è comune per i flussi live/lineari.

   TVSDK sostituisce di solito il contenuto principale con gli annunci nella posizione indicata dai metadati/suggerimenti; in caso contrario, il client cadrebbe sempre di più dietro il punto attivo effettivo.

* **La mappa del server pubblicitario**

   Solitamente, i metadati relativi a questi flussi vengono registrati nel server pubblicitario prima della riproduzione. TVSDK recupera la cronologia degli annunci e gli annunci corrispondenti dal server. Questa fonte è comune per i flussi VOD.

   TVSDK in genere inserisce gli annunci risolti nel contenuto principale come indicato dalla mappa del server.

>[!NOTE]
>
>Per impostazione predefinita, TVSDK utilizza segnali manifest per flussi live/lineari e mappe del server pubblicitario per flussi VOD. Tuttavia, per supportare la riproduzione completa degli eventi per gli eventi in diretta, l&#39;applicazione deve effettuare ulteriori passi.

