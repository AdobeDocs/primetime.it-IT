---
seo-title: Creare criteri DRM personalizzati (facoltativo)
title: Creare criteri DRM personalizzati (facoltativo)
uuid: 701b51d9-6dde-4c21-bc5b-09e612582968
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# Creare criteri DRM personalizzati (facoltativo){#create-custom-drm-policies-optional}

Il kit di protezione DRM di Primetime Cloud include alcuni criteri preconfigurati che possono essere utilizzati durante la creazione del pacchetto. Se desiderate ulteriori configurazioni del criterio, ad esempio un diritto specifico di inserimento nella whitelist SWF, il Gestore dei criteri DRM di Primetime incluso può essere utilizzato per generare criteri personalizzati.

>[!NOTE]
>
>Tutti i criteri devono utilizzare l&#39;autenticazione ANONYMOUS (non Password nome utente o Personalizzato), indipendentemente dal fatto che venga utilizzato o meno il flusso di lavoro Autenticazione/Adesione personalizzata.

In Gestione criteri è incluso il file di [!DNL flashaccesstools.properties] configurazione, che è stato modificato per esporre solo le opzioni dei criteri configurabili supportate dal servizio DRM di Primetime Cloud. L&#39;impostazione delle opzioni dei criteri non supportate dal servizio DRM di Primetime Cloud comporterà errori di acquisizione della licenza. Per informazioni sull&#39;utilizzo di Gestione criteri DRM di Primetime, fare riferimento a: Implementazioni di riferimento DRM [Primetime: Policy Manager](https://help.adobe.com/en_US/primetime/drm/5.3/reference_implementations/index.html#concept-DRM_Policy_Manager).

Per creare un nuovo criterio, aggiornate il [!DNL flashaccesstools.properties] file come desiderato, quindi utilizzate il comando:

```
java -jar libs/AdobePolicyManager.jar new myPolicy.pol
```

## Creare criteri in modo dinamico per Autenticazione personalizzata/Adesione{#create-policies-dynamically-for-custom-auth-entitlement}

Se utilizzate Autenticazione/Adesione personalizzata DRM di Primetime Cloud e desiderate creare in modo dinamico un nuovo criterio DRM per ogni richiesta di licenza (invece di estrarre i criteri da un pool pregenerato), Adobe consiglia di utilizzare direttamente l&#39;SDK Java DRM di Primetime. L&#39;utilizzo diretto di Java SDK è più rapido rispetto allo [!DNL AdobePolicyManager.jar] strumento, che trasmette automaticamente il file dei criteri sul disco, con sovraccarico I/O del disco.

Il codice di esempio che utilizza Java SDK si trova nella [!DNL /Primetime DRM PolicyManager/sampleCode/] directory, denominata [!DNL CreatePolicy.java] e [!DNL CreatePolicyWithOutputProtection.java]. Javadocs e documentazione per l&#39;SDK Java sono disponibili in [Una panoramica dell&#39;SDK DRM di Adobe Primetime](../../../digital-rights-management/drm-sdk-overview/overview.md)

Per creare ed eseguire gli esempi, copiate i file .java nella cartella ../libs/ ed eseguite:

```
javac -cp adobe-flashaccess-sdk.jar:. CreatePolicy.java
java -cp adobe-flashaccess-sdk.jar:. CreatePolicy
```
