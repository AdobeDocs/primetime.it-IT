---
description: Potete creare facilmente un'interfaccia utente personalizzata basata sul framework di implementazione di riferimento.
seo-description: Potete creare facilmente un'interfaccia utente personalizzata basata sul framework di implementazione di riferimento.
seo-title: Creare un'interfaccia utente personalizzata
title: Creare un'interfaccia utente personalizzata
uuid: b785f6a4-3ef8-4f7a-a087-0d6551da9750
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---


# Creare un&#39;interfaccia utente personalizzata {#build-a-custom-user-interface}

Potete creare un&#39;interfaccia utente personalizzata basata sul framework di implementazione di riferimento.

I componenti dell’interfaccia utente delle seguenti funzioni sono già integrati:

* Annunci cliccabili
* Sovrapposizioni di annunci
* Connessione audio ritardata
* Sottotitoli codificati
* Listener per tutti i componenti di cui sopra

1. Modificate il file [!DNL PlayerFragment.java] per inizializzare i componenti dell&#39;interfaccia che desiderate utilizzare nel lettore.

1. Modificate il file [!DNL res/player/player_fragment.xml] per personalizzare l&#39;interfaccia utente.
1. Create il progetto.

>[!NOTE]
>
>Per apportare modifiche all&#39;interfaccia utente della barra di ricerca, è possibile modificare la classe MarkableSeekBar. La classe [MarkableSeekBar](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/player/MarkableSeekBar.html) gestisce il cursore, il pollice del dispositivo di scorrimento, il portautensili, i marcatori cue, l&#39;intervallo del buffer e gli sfondi dell&#39;intervallo di ricerca.