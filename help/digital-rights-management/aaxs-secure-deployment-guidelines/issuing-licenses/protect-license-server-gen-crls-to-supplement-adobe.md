---
seo-title: 'Generare CRL per completare quelli pubblicati dal Adobe '
title: 'Generare CRL per completare quelli pubblicati dal Adobe '
uuid: 4e93f6d3-5a04-44e9-9e6b-e878798b68f5
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# Generare CRL per completare quelli pubblicati da  Adobe{#generate-crls-to-supplement-those-published-by-adobe}

 Accesso Adobe consente di creare CRL per completare il computer CRL pubblicato da  Adobe.  Adobe Access SDK verifica e applica i CRL del Adobe , tuttavia, è possibile rifiutare computer client aggiuntivi creando un CRL che revoca credenziali computer aggiuntive. A tal fine, è necessario passare il CRL a  Adobe Access SDK, quindi, al momento del rilascio di una licenza, l&#39;SDK verifica sia l&#39; CRL che il proprio CRL.

Per ulteriori informazioni sulla generazione di CRL, vedere `RevocationListFactory` in *Guida di riferimento delle API per l&#39;accesso ai Adobi*.
