---
title: Preparare le password per i file delle proprietà del server
description: Preparare le password per i file delle proprietà del server
copied-description: true
exl-id: b613d43d-17ec-44e9-bd14-81f9bb9a7f62
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# Preparare le password per i file delle proprietà del server{#prepare-passwords-for-the-server-properties-files}

L’implementazione di riferimento fornisce `ScrambleUtil.class`, classe che garantisce la protezione della password delle credenziali.

Utilizzare questo strumento per crittografare la password prima di includerla nel [!DNL flashaccess-refimpl.properties] file.

Per eseguire lo strumento, puoi utilizzare uno script di Ant o Java.

L&#39;utility genera la password crittografata, che è necessario copiare in [!DNL flashaccess-refimpl.properties] file.

>[!NOTE]
>
>Password codificate con `ScrambleUtil.class` che è stato fornito con l’implementazione di riferimento non funzionano con il server DRM Primetime per lo streaming protetto.
