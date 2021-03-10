---
description: Puoi creare facilmente un’interfaccia utente personalizzata basata sul framework di implementazione di riferimento.
title: Creare un’interfaccia utente personalizzata
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---


# Creare un’interfaccia utente personalizzata {#build-a-custom-user-interface}

Puoi creare un’interfaccia utente personalizzata basata sul framework di implementazione di riferimento.

I componenti dell’interfaccia utente delle seguenti funzioni sono già integrati:

* Annunci cliccabili
* Sovrapposizioni annunci
* Audio con associazione ritardata
* Sottotitoli codificati
* Listener per tutti i componenti di cui sopra

1. Modifica il file [!DNL PlayerFragment.java] per inizializzare i componenti dell’interfaccia utente che desideri utilizzare nel lettore.

1. Modifica il file [!DNL res/player/player_fragment.xml] per personalizzare l’interfaccia utente.
1. Crea il progetto.

>[!NOTE]
>
>Per apportare modifiche all&#39;interfaccia utente della barra di ricerca, puoi modificare la classe MarkableSeekBar . La classe [MarkableSeekBar](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/player/MarkableSeekBar.html) gestisce il cursore, il pollice del dispositivo di scorrimento, il supporto per gli indicatori di annunci, i marcatori di cue, l&#39;intervallo di buffer e gli sfondi dell&#39;intervallo di ricerca.