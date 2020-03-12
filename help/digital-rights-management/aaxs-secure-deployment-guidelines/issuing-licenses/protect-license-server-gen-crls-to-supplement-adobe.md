---
seo-title: Generare CRL per completare quelli pubblicati da Adobe
title: Generare CRL per completare quelli pubblicati da Adobe
uuid: 4e93f6d3-5a04-44e9-9e6b-e878798b68f5
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Generare CRL per completare quelli pubblicati da Adobe{#generate-crls-to-supplement-those-published-by-adobe}

Adobe Access consente di creare CRL per completare il computer CRL pubblicato da Adobe. L&#39;SDK di Adobe Access verifica e applica gli Adobe CRL, tuttavia, è possibile rifiutare computer client aggiuntivi creando un CRL che revoca credenziali computer aggiuntive. A tal fine, è necessario passare il CRL all&#39;SDK di Adobe Access, quindi, al momento del rilascio di una licenza, l&#39;SDK verifica sia l&#39;Adobe CRL che il proprio CRL.

Per ulteriori informazioni sulla generazione dei CRL, vedere `RevocationListFactory` in Riferimento *API di* Adobe Access.
